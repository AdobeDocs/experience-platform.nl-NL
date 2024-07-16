---
title: Anoniem blok in Query-service
description: Het anonieme blok is een SQL syntaxis die door de Dienst van de Vraag van Adobe Experience Platform wordt gesteund, die u toestaat om een opeenvolging van vragen efficiënt uit te voeren
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 9193ba821409806cd7b4667c5de73a0cf2660c66
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Anoniem blok in Query-service

Adobe Experience Platform Query Service ondersteunt anonieme blokken. Met de functie voor anonieme blokken kunt u een of meer SQL-instructies ketenen die op volgorde worden uitgevoerd. Zij bieden ook de mogelijkheid om uitzonderingen af te handelen.

De anonieme blokeigenschap is een efficiënte manier om een opeenvolging van verrichtingen of vragen uit te voeren. De keten van vragen binnen het blok kan als malplaatje worden bewaard en gepland om bij een bepaald tijd of interval te lopen. Deze vragen kunnen worden gebruikt om gegevens te schrijven en toe te voegen om een nieuwe gegevensreeks tot stand te brengen en typisch gebruikt waar u een gebiedsdeel hebt.

De tabel bevat een uitsplitsing van de belangrijkste secties van het blok: uitvoering en afhandeling van uitzonderingen. De secties worden gedefinieerd door de trefwoorden `BEGIN` , `END` en `EXCEPTION` .

| sectie | beschrijving |
|---|---|
| executie | Een uitvoerbare sectie begint met het trefwoord `BEGIN` en eindigt met het trefwoord `END` . Elke set instructies die in de trefwoorden `BEGIN` en `END` zijn opgenomen, wordt op volgorde uitgevoerd en zorgt ervoor dat volgende query&#39;s pas worden uitgevoerd nadat de vorige query in de reeks is voltooid. |
| uitzonderingsbehandeling | De optionele sectie voor het afhandelen van uitzonderingen begint met het trefwoord `EXCEPTION` . Het bevat de code om uitzonderingen af te vangen en te behandelen als om het even welke SQL verklaringen in de uitvoeringssectie ontbreken. Als om het even welke vragen ontbreken, wordt het volledige blok tegengehouden. |

Er moet op worden gewezen dat een blok een uitvoerbare verklaring is en daarom binnen andere blokken kan worden genesteld.

>[!NOTE]
>
> Het wordt sterk geadviseerd om uw vragen op kleinere datasets te testen en ervoor te zorgen dat zij zoals verwacht werken. Als een query een syntaxisfout heeft, wordt de uitzondering gegenereerd en wordt het gehele blok afgebroken. Zodra u de integriteit van de vragen hebt geverifieerd kunt u beginnen hen te ketenen. Dit zorgt ervoor dat het blok zoals verwacht werkt alvorens u hen in werking stelt.

## Voorbeeld van anonieme vragen over blokken

De volgende query toont een voorbeeld van het koppelen van SQL-instructies. Zie de [ SQL syntaxis in het document van de Dienst van de Vraag ](../sql/syntax.md) voor meer informatie over om het even welke SQL gebruikte syntaxis.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

In het onderstaande voorbeeld blijft `SET` het resultaat van een `SELECT` -query in de opgegeven lokale variabele behouden. De variabele is scoped aan het anonieme blok.

De momentopname-id wordt opgeslagen als een lokale variabele (`@current_sid`). Het wordt dan gebruikt in de volgende vraag om resultaten terug te keren die op SNAPSHOT van de zelfde dataset/de lijst worden gebaseerd.

Een gegevensbestandmomentopname is een read-only, statische mening van een SQL gegevensbestand van de Server. Voor meer [ informatie over de momentopnameclausule ](../sql/syntax.md#SNAPSHOT-clause) zie de SQL syntaxisdocumentatie.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Anoniem blok met externe klanten {#third-party-clients}

Bepaalde derdecliënten kunnen een afzonderlijke herkenningsteken vóór en na een SQL blok vereisen om erop te wijzen dat een deel van het manuscript als één enkele verklaring zou moeten worden behandeld. Als u een foutenmelding ontvangt wanneer het gebruiken van de Dienst van de Vraag met een derdecliënt, zou u naar de documentatie van de derdecliënt betreffende het gebruik van een SQL blok moeten verwijzen.

Bijvoorbeeld, **DbVisualizer** vereist dat het scheidingsteken de enige tekst op de lijn moet zijn. In DbVisualizer, is de standaardwaarde voor Begin Identifier `--/` en voor het Eind - Herkenningsteken is het `/`. Een voorbeeld van een anoniem blok in DbVisualizer is hieronder te zien:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

Voor DbVisualizer in het bijzonder, is er ook een optie in UI aan &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Zie de [ documentatie DbVisualizer ](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) voor meer informatie.

## Volgende stappen

Door dit document te lezen, hebt u nu een duidelijk inzicht in anonieme blokken en hoe ze gestructureerd zijn. Gelieve te lezen de [ gids van de vraaguitvoering ](../best-practices/writing-queries.md) voor meer informatie bij het schrijven van vragen.

U zou ook over [ moeten lezen hoe de anonieme blokken met het stijgende patroon van het ladingsontwerp ](./incremental-load.md) worden gebruikt om vraagefficiency te verhogen.
