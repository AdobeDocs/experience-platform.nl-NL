---
keywords: inzichten;attributie ai;attributie ai inzichten;AAI vraagdienst;attributie vragen;attributie scores
feature: Attribution AI
title: Kenmerkscores analyseren met Query-service
description: Leer hoe u Adobe Experience Platform Query Service gebruikt om AI-scores voor kenmerken te analyseren.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Kenmerkscores analyseren met gebruik van Query-service

Elke rij in de gegevens vertegenwoordigt een conversie, waarbij informatie voor verwante aanraakpunten wordt opgeslagen als een array van structs onder de kolom `touchpointsDetail` .

| Informatie over aanraakpunten | Kolom |
| ---------------------- | ------ |
| Naam aanraakpunt | `touchpointsDetail. touchpointName` |
| Aanraakpuntkanaal | `touchpointsDetail.touchPoint.mediaChannel` |
| Attributie AI-algoritmische scores van aanraakpunt | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Gegevenspaden zoeken

Selecteer **[!UICONTROL Datasets]** in de gebruikersinterface van Adobe Experience Platform in de linkernavigatie. De pagina **[!UICONTROL Datasets]** wordt weergegeven. Selecteer vervolgens het tabblad **[!UICONTROL Browse]** en zoek de uitvoergegevensset voor uw Attribution AI-scores.

![ Toegang hebbend tot uw model ](./images/aai-query/datasets_browse.png)

Selecteer uw uitvoerdataset. De pagina met gegevenssetactiviteiten wordt weergegeven.

![ de activiteitenpagina van de dataset ](./images/aai-query/select_preview.png)

Selecteer **[!UICONTROL Preview dataset]** in de rechterbovenhoek van de activiteitenpagina van de gegevensset om een voorvertoning van uw gegevens weer te geven en ervoor te zorgen dat de gegevens op de verwachte manier zijn opgenomen.

![ voorproefdataset ](./images/aai-query/preview_dataset.JPG)

Nadat u een voorvertoning van uw gegevens hebt weergegeven, selecteert u het schema in de rechtertrack. Er verschijnt een pop-up met de schemanaam en de beschrijving. Selecteer de hyperlink naar de schemanaam om deze om te leiden naar het scoreschema.

![ selecteer het schema ](./images/aai-query/select_schema.png)

Met het scoreschema kunt u een waarde selecteren of zoeken. Als deze optie is geselecteerd, wordt de **[!UICONTROL Field properties]** side-rail geopend, waarmee u het pad kunt kopiëren en query&#39;s kunt maken.

![ kopieer de weg ](./images/aai-query/copy_path.png)

## Access Query Service

Als u Query Service wilt openen vanuit de gebruikersinterface van Experience Platform, selecteert u **[!UICONTROL Queries]** in de linkernavigatie en selecteert u vervolgens het tabblad **[!UICONTROL Browse]** . Er wordt een lijst met eerder opgeslagen query&#39;s geladen.

![ doorbladeren van de vraagdienst ](./images/aai-query/query_tab.png)

Selecteer vervolgens **[!UICONTROL Create query]** in de rechterbovenhoek. De Query-editor wordt geladen. Met behulp van de Query-editor kunt u query&#39;s maken met behulp van uw score-gegevens.

![ vraagredacteur ](./images/aai-query/query_example.png)

Voor meer informatie over de Redacteur van de Vraag, bezoek de [ gebruikersgids van de Redacteur van de Vraag ](../../query-service/ui/user-guide.md).

## Zoeksjablonen voor analyse van de toewijzingsscore

De hieronder vragen kunnen als malplaatje voor verschillende scenario&#39;s van de scoreanalyse worden gebruikt. U moet de waarden `_tenantId` en `your_score_output_dataset` vervangen door de juiste waarden in het schema voor het uitvoeren van scores.

>[!NOTE]
>
> Afhankelijk van de manier waarop uw gegevens zijn ingevoerd, hebben de hieronder gebruikte waarden, zoals `timestamp` , mogelijk een andere indeling.

### Validatievoorbeelden

**Totaal aantal omzettingen door omzettingsgebeurtenis (binnen in een omzettingsvenster)**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**Totaal aantal conversie-slechts gebeurtenissen (binnen in een omzettingsvenster)**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### Voorbeeld van trendanalyse

**Aantal omzettingen per dag**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### Voorbeeld van distributie-analyse

**Hoeveelheid touchpoints op omzettingswegen door bepaald type (binnen in een omzettingsvenster)**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Insight-voorbeelden

**Incrementele eenheden onderbreking door touchpoint en omzettingsdatum (binnen in een omzettingsvenster)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**Incrementele eenheden onderbreking door touchpoint en touchpoint datum (binnen in een omzettingsvenster)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**Geaggregeerde scores voor een bepaald type van touchpoint voor alle het scoren modellen (binnen in een omzettingsvenster)**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**Geavanceerd - de analyse van de weglengte**

Hiermee wordt een verdeling over padlengte opgehaald voor elk type conversiegebeurtenis:

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**Geavanceerd - verschillend aantal aanraakpunten op de analyse van omzettingswegen**

Hiermee wordt de distributie voor het aantal verschillende aanraakpunten op een conversiepad opgehaald voor elk conversiegebeurtenistype:

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

### Voorbeeld van afvlakking en explosie

Met deze query wordt de struct-kolom samengevoegd tot meerdere aparte kolommen en worden arrays samengevoegd tot meerdere rijen. Dit helpt bij het omzetten van attributiescore in een CSV-indeling. De uitvoer van deze query heeft één conversie en een van de aanraakpunten die overeenkomen met die conversie in elke rij.

>[!TIP]
>
> In dit voorbeeld moet u `{COLUMN_NAME}` vervangen in aanvulling op `_tenantId` en `your_score_output_dataset` . De variabele `COLUMN_NAME` kan de waarden van optionele pass through kolomnamen (die kolommen melden) nemen die tijdens het vormen van uw model van Attribution AI werden toegevoegd. Controleer het uitvoerschema voor de score om de `{COLUMN_NAME}` -waarden te vinden die nodig zijn om deze query uit te voeren.

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
