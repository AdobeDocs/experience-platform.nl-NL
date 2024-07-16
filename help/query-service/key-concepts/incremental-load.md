---
title: Incrementele belasting in Query-service
description: De stijgende ladingseigenschap gebruikt zowel anonieme blok als momentopnamefuncties om een dichtbij oplossing in real time te verstrekken voor het bewegen van gegevens van het gegevensholoader aan uw gegevenspakhuis terwijl het negeren van passende gegevens.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Incrementele belasting in Query-service

Het patroon van het stijgende ladingsontwerp is een oplossing voor het beheren van gegevens. Het patroon verwerkt slechts informatie in de dataset die sinds de laatste ladingsuitvoering is gecreeerd of gewijzigd.

De stijgende lading gebruikt diverse eigenschappen die door de Dienst van de Vraag van Adobe Experience Platform zoals anonieme blok en momentopnamen worden verstrekt. Dit ontwerppatroon verhoogt de verwerkingsefficiëntie omdat alle gegevens die al uit de bron zijn verwerkt, worden overgeslagen. Deze kan zowel bij streaming- als batchgegevensverwerking worden gebruikt.

Dit document bevat een aantal instructies voor het maken van een ontwerppatroon voor incrementele verwerking. Deze stappen kunnen als malplaatje worden gebruikt om uw eigen stijgende vragen van de gegevenslading tot stand te brengen.

## Aan de slag

De SQL-voorbeelden in dit document vereisen dat u een goed inzicht hebt in de anonieme mogelijkheden voor blokken en momentopnamen. Het wordt geadviseerd dat u de [ steekproef anonieme blokvragen ](./anonymous-block.md) documentatie en ook de [ momentopnameclausule ](../sql/syntax.md#snapshot-clause) documentatie leest.

Voor begeleiding op om het even welke die terminologie binnen deze gids wordt gebruikt, verwijs naar de [ SQL syntaxisgids ](../sql/syntax.md).

## Gegevens stapsgewijs laden

In de onderstaande stappen wordt getoond hoe u gegevens kunt maken en incrementeel kunt laden met behulp van momentopnamen en de anonieme blokfunctie. Het ontwerppatroon kan als malplaatje voor uw eigen opeenvolging van vragen worden gebruikt.

1. Maak een `checkpoint_log` -tabel waarin de meest recente opname wordt bijgehouden die is gebruikt om gegevens te verwerken. De volgende lijst (`checkpoint_log` in dit voorbeeld) moet eerst aan `null` worden geïnitialiseerd om een dataset stapsgewijs te verwerken.

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. Vul de `checkpoint_log` lijst met één leeg verslag voor de dataset die stijgende verwerking vereist. `DIM_TABLE_ABC` is de gegevensset die in het onderstaande voorbeeld moet worden verwerkt. Bij de eerste keer dat `DIM_TABLE_ABC` wordt verwerkt, wordt `last_snapshot_id` geïnitialiseerd als `null` . Dit staat u toe om de volledige dataset bij de eerste gelegenheid en incrementeel daarna te verwerken.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. Start vervolgens `DIM_TABLE_ABC_Incremental` om verwerkte uitvoer van `DIM_TABLE_ABC` te bevatten. Het anonieme blok in de **vereiste** uitvoeringssectie van het SQL hieronder voorbeeld, zoals die in stap één tot vier wordt beschreven, wordt opeenvolgend uitgevoerd om gegevens incrementeel te verwerken.

   1. Stel de `from_snapshot_id` in die aangeeft vanaf welk punt de verwerking begint. De `from_snapshot_id` in het voorbeeld wordt vanuit de `checkpoint_log` -tabel opgevraagd voor gebruik met `DIM_TABLE_ABC` . Bij de eerste uitvoering zal de opname-id `null` zijn, wat betekent dat de volledige gegevensset wordt verwerkt.
   1. Stel de `to_snapshot_id` in als de huidige opname-id van de brontabel (`DIM_TABLE_ABC` ). In het voorbeeld wordt dit gevraagd vanuit de metagegevenstabel van de brontabel.
   1. Gebruik het trefwoord `CREATE` om `DIM_TABLE_ABC_Incremenal` te maken als de doeltabel. De bestemmingslijst voortduurt de verwerkte gegevens van de brondataset (`DIM_TABLE_ABC`). Hierdoor kunnen de verwerkte gegevens van de brontabel tussen `from_snapshot_id` en `to_snapshot_id` incrementeel aan de doeltabel worden toegevoegd.
   1. Werk de `checkpoint_log` tabel bij met de `to_snapshot_id` voor de brongegevens die `DIM_TABLE_ABC` correct heeft verwerkt.
   1. Als om het even welke opeenvolgend uitgevoerde vragen van het anonieme blok ontbreken, wordt de **facultatieve** uitzonderingssectie uitgevoerd. Dit retourneert een fout en beëindigt het proces.

   >[!NOTE]
   >
   >`history_meta('source table name')` is een geschikte methode die wordt gebruikt om toegang tot beschikbare momentopname in een dataset te krijgen.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. Gebruik de stijgende logica van de gegevenslading in het anonieme blokvoorbeeld hieronder om het even welke nieuwe gegevens van de brondataset (sinds meest recente timestamp) toe te staan om aan de bestemmingstabel bij een regelmatige kadentie worden verwerkt en worden toegevoegd. In het voorbeeld worden gegevenswijzigingen in `DIM_TABLE_ABC` verwerkt en toegevoegd aan `DIM_TABLE_ABC_incremental` .

   >[!NOTE]
   >
   > `_ID` is de primaire sleutel in zowel `DIM_TABLE_ABC_Incremental` als `SELECT history_meta('DIM_TABLE_ABC')` .

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

Deze logica kan op om het even welke lijst worden toegepast om stijgende lasten uit te voeren.

## Verlopen momentopnamen

>[!IMPORTANT]
>
>De meta-gegevens van de momentopname verlopen na **twee** dagen. Een verlopen momentopname maakt de logica van het hierboven verstrekte manuscript ongeldig.

Om de kwestie van een verlopen momentopname identiteitskaart op te lossen, neem het volgende bevel aan het begin van het anonieme blok op. De volgende coderegel overschrijft de `@from_snapshot_id` met de oudste beschikbare `snapshot_id` op basis van metagegevens.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

Het volledige codeblok ziet er als volgt uit:

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## Volgende stappen

Door dit document te lezen, zou u een beter inzicht in moeten hebben hoe te om anonieme blok en momentopnamefuncties te gebruiken om stijgende ladingen uit te voeren en kan deze logica op uw eigen specifieke vragen toepassen. Voor algemene begeleiding bij vraaguitvoering, te lezen gelieve de [ gids op vraaguitvoering in de Dienst van de Vraag ](../best-practices/writing-queries.md).
