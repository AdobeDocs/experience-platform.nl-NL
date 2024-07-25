---
title: Ontdek, los problemen op en verifieer Batchverwerking met SQL
description: Leer hoe u het proces voor gegevensinvoer in Adobe Experience Platform begrijpt en beheert. In dit document wordt beschreven hoe u batches kunt verifiëren en ingesloten gegevens kunt opvragen.
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: 692a061e3b2facbfafc65f966832230187f5244d
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# Onderzoek, los problemen op, en verifieer partijingestie met SQL

In dit document wordt uitgelegd hoe u records in ingesloten batches met SQL kunt verifiëren en valideren. In dit document wordt uitgelegd hoe u:

- Batchmetagegevens voor toegang
- Los en verzeker gegevensintegriteit door partijen te vragen problemen op

>[!NOTE]
>
>Sommige schermafbeeldingen in deze handleiding worden genomen vanuit [!DNL DBVisualizer] . Leren hoe te [ de Dienst van de Vraag met DBVisualizer ](../clients/dbvisulaizer.md) of andere [ hulpmiddelen van derdeBI ](../clients/overview.md) verbinden, zie de verbonden documentatie.

## Vereisten

Om uw begrip van de concepten te helpen die in dit document worden besproken, zou u kennis van de volgende onderwerpen moeten hebben:

- **Inname van Gegevens**: Zie het [ overzicht van de gegevensopname ](../../ingestion/home.md) om de grondbeginselen te leren van hoe het gegeven in het Platform, met inbegrip van de verschillende methodes en processen in kwestie wordt opgenomen.
- **Inname van de Partij**: Zie [ partij ingestition API overzicht ](../../ingestion/batch-ingestion/overview.md) om de basisconcepten van partijingestitie te leren. Specifiek, wat een &quot;partij&quot;is en hoe het binnen het proces van de gegevensopname van Platform functioneert.
- **meta-gegevens van het Systeem in datasets**: Zie het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md) leren hoe de gebieden van systeemmeta-gegevens worden gebruikt om opgenomen gegevens te volgen en te vragen.
- **Model van de Gegevens van de Ervaring (XDM)**: Zie het [ schema&#39;s overzicht UI ](../../xdm/ui/overview.md) en de [ basisbeginselen van schemacompositie&#39; ](../../xdm/schema/composition.md) om over XDM schema&#39;s te leren en hoe zij de structuur en het formaat van gegevens vertegenwoordigen en bevestigen die in Platform worden opgenomen.

## Batchmetagegevens voor toegang {#access-dataset-batch-metadata}

Om ervoor te zorgen dat de systeemkolommen (meta-gegevenskolommen) in de vraagresultaten worden omvat, gebruik het SQL bevel `set drop_system_columns=false` in uw Redacteur van de Vraag. Hierdoor wordt het gedrag van uw SQL-querysessie geconfigureerd. Deze invoer moet worden herhaald als u een nieuwe sessie start.

Als u vervolgens de systeemvelden van de gegevensset wilt weergeven, voert u een instructie SELECT all uit om de resultaten van de gegevensset weer te geven, bijvoorbeeld `select * from movie_data` . De resultaten omvatten twee nieuwe kolommen aan de rechterkant `_acp_system_metadata` en `_ACP_BATCHID`. Met de kolommen met metagegevens `_acp_system_metadata` en `_ACP_BATCHID` kunt u de logische en fysieke partities van opgenomen gegevens identificeren.

![ DBVisualizer UI met de film_data lijst en zijn meta-gegevenskolommen die en worden benadrukt.](../images/use-cases/movie_data-table-with-metadata-columns.png)

Wanneer het gegeven in Platform wordt opgenomen, wordt het toegewezen een logische verdeling die op de inkomende gegevens wordt gebaseerd. Deze logische partitie wordt vertegenwoordigd door `_acp_system_metadata.sourceBatchId` . Met deze id kunt u de gegevensbatches logisch groeperen en identificeren voordat ze worden verwerkt en opgeslagen.

Nadat de gegevens worden verwerkt en in het gegevenspeer worden opgenomen, wordt het toegewezen een fysieke verdeling die door `_ACP_BATCHID` wordt vertegenwoordigd. Deze id weerspiegelt de werkelijke opslagpartitie in het datumpeer waar de ingesloten gegevens zich bevinden.

### Gebruik SQL om logische en fysieke verdelingen te begrijpen {#understand-partitions}

Helpen begrijpen hoe het gegeven na opname wordt gegroepeerd en verdeeld, gebruik de volgende vraag om het aantal verschillende fysieke verdelingen (`_ACP_BATCHID`) voor elke logische verdeling (`_acp_system_metadata.sourceBatchId`) te tellen.

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

De resultaten van deze zoekopdracht worden weergegeven in de onderstaande afbeelding.

![ de resultaten van een vraag om het aantal afzonderlijke fysieke verdelingen voor elke logische verdeling te tonen.](../images/use-cases/logical-and-physical-partition-count.png)

Deze resultaten tonen aan dat het aantal inputpartijen niet noodzakelijk het aantal outputpartijen aanpast, aangezien het systeem de meest efficiënte manier bepaalt om de gegevens in het gegevensmeer in batch te slaan en op te slaan.

In dit voorbeeld wordt aangenomen dat u een CSV-bestand hebt ingesloten in Platform en een gegevensset met de naam `drug_checkout_data` hebt gemaakt.

Het `drug_checkout_data` -bestand is een diepgeneste set van 35.000 records. Gebruik de SQL-instructie `SELECT * FROM drug_orders;` om een voorvertoning weer te geven van de eerste set records in de op JSON gebaseerde `drug_orders` -dataset.

In de onderstaande afbeelding ziet u een voorvertoning van het bestand en de records.

![ A voorproef van de eerste reeks verslagen in de op JSON-Gebaseerde drug_orders dataset.](../images/use-cases/drug-orders-preview.png)

### SQL gebruiken om inzichten te genereren over het proces van batchopname {#sql-insights-on-batch-ingestion}

Gebruik de SQL-instructie hieronder om inzicht te verschaffen in de manier waarop de gegevensinvoer is gegroepeerd en verwerkt in batches.

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

De zoekresultaten worden weergegeven in de onderstaande afbeelding.

![ een lijst die van A de distributie van toont hoe de inputpartijen in een tijd met verslagtellingen werden beheerst.](../images/use-cases/distribution-of-input-batches.png)

De resultaten tonen de efficiëntie en het gedrag van het gegevensinvoeringsproces aan. Hoewel er drie invoerbatches zijn gemaakt — elk met 2000, 24000 en 9000 records — toen de records werden gecombineerd en gededupliceerd, bleef er slechts één unieke batch over.

>[!NOTE]
>
>Alle verslagen die binnen een dataset zichtbaar zijn zijn die met succes werden opgenomen. Een geslaagde batch-opname betekent niet dat alle records aanwezig zijn die uit de broninvoer zijn verzonden. U moet controleren op fouten bij het invoeren van gegevens om de batches/records te vinden waarin de gegevens niet zijn verwerkt.

## Een batch valideren met SQL {#validate-a-batch-with-SQL}

Daarna, bevestig en verifieer de verslagen die in de dataset met SQL zijn opgenomen.

>[!TIP]
>
>Als u de batch-id en queryrecords wilt ophalen die aan die batch-id zijn gekoppeld, moet u eerst een batch maken in Platform. Als u het proces zelf wilt testen, kunt u CSV-gegevens invoeren in Platform. Lees de gids op hoe te [ een Csv- dossier aan een bestaand schema in kaart brengen XDM gebruikend AI-Gegenereerde aanbevelingen ](../../ingestion/tutorials/map-csv/recommendations.md).

Nadat u een batch hebt ingepakt, moet u naar de [!UICONTROL Datasets activity tab] navigeren voor de gegevensset waarin u gegevens hebt ingevoerd.

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Datasets]** in de linkernavigatie om het dashboard van [!UICONTROL Datasets] te openen. Selecteer vervolgens de naam van de gegevensset op het tabblad [!UICONTROL Browse] voor toegang tot het scherm [!UICONTROL Dataset activity] .

![ het dashboard van Datasets UI van het Platform met Datasets die in linkernavigatie worden benadrukt.](../images/use-cases/datasets-workspace.png)

De weergave [!UICONTROL Dataset activity] wordt weergegeven. Deze mening bevat details van uw geselecteerde dataset. Het omvat om het even welke ingebedde partijen die in een lijstformaat worden getoond.

Selecteer een batch in de lijst met beschikbare batches en kopieer de [!UICONTROL Batch ID] in het deelvenster Details aan de rechterkant.

![ de Datasets UI van het Experience Platform die de ingebedde verslagen met een benadrukte partijidentiteitskaart tonen.](../images/use-cases/batch-id.png)

Daarna, gebruik de volgende vraag om alle verslagen terug te winnen die in de dataset als deel van die partij werden omvat:

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

Het trefwoord `_ACP_BATCHID` wordt gebruikt om het filter [!UICONTROL Batch ID] uit te voeren.

>[!TIP]
>
>De component `LIMIT` is handig als u het aantal weergegeven rijen wilt beperken, maar een filtervoorwaarde is wenselijker.

Wanneer u deze vraag in de Redacteur van de Vraag uitvoert, zijn de resultaten beknot aan 100 rijen. De redacteur van de Vraag wordt ontworpen voor snelle voorproeven en onderzoek. Om tot 50.000 rijen terug te winnen, kunt u een derdehulpmiddel zoals DBVisualizer of DBeaver gebruiken.

## Volgende stappen {#next-steps}

Door dit document te lezen hebt u de belangrijkste elementen geleerd van het controleren en valideren van records in ingebedde batches als onderdeel van het gegevensinvoerproces. U verwierf ook inzichten in de toegang tot van de meta-gegevens van de gegevenssetpartij, begrip logische en fysieke verdelingen, en het vragen van specifieke partijen gebruikend SQL bevelen. Deze kennis kan u helpen de gegevensintegriteit te waarborgen en uw gegevensopslag op het platform te optimaliseren.

Daarna, zou u gegevensopname moeten oefenen om de geleerde concepten toe te passen. Maak een voorbeeld van een gegevensset in Platform met de voorbeeldbestanden of uw eigen gegevens. Als u dit niet reeds hebt gedaan, lees het leerprogramma op hoe te [ gegevens in Adobe Experience Platform ](../../ingestion/tutorials/ingest-batch-data.md) innemen.

Alternatief, kon u leren hoe te [ de Dienst van de Vraag met een verscheidenheid van de toepassingen van de Desktopcliënt ](../clients/overview.md) verbinden en verifiëren om uw mogelijkheden van de gegevensanalyse te verbeteren.
