---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: Profielvoorvertoning - Real-time API voor klantprofiel
description: Met Adobe Experience Platform kunt u klantgegevens uit meerdere bronnen invoeren om robuuste, uniforme profielen voor individuele klanten te maken. Aangezien gegevens die voor het Profiel van de Klant in real time worden toegelaten in Platform worden opgenomen, wordt het opgeslagen binnen de gegevensopslag van het Profiel. Aangezien het aantal verslagen in de opslag van het Profiel stijgt of vermindert, wordt een steekproefbaan in werking gesteld die informatie betreffende hoeveel profielfragmenten en samengevoegde profielen in de gegevensopslag omvat. Met behulp van de profiel-API kunt u een voorvertoning weergeven van het meest recente voorbeeld en van de distributie van het lijstprofiel via gegevensset en naamruimte.
topic: guide
translation-type: tm+mt
source-git-commit: 75a07abd27f74bcaa2c7348fcf43820245b02334
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---


# Voorvertoning voorbeeldstatuseindpunt (voorvertoning profiel)

Met Adobe Experience Platform kunt u klantgegevens uit meerdere bronnen invoeren om robuuste, uniforme profielen voor individuele klanten te maken. Aangezien gegevens die voor het Profiel van de Klant in real time worden toegelaten in worden opgenomen [!DNL Platform], wordt het opgeslagen binnen de gegevensopslag van het Profiel.

Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 5% verhoogt of verlaagt, wordt een taak geactiveerd om het aantal bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om de telling bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal bij te werken als aan de drempel van 5% voor verhogen of verlagen is voldaan. Met behulp van de profiel-API kunt u een voorvertoning weergeven van de meest recente voorbeeldtaak en de distributie van het lijstprofiel via gegevensset en naamruimte op naam.

Deze cijfers zijn ook beschikbaar in de sectie [!UICONTROL Profielen] van de gebruikersinterface van het Experience Platform. Ga naar de [[!DNL Profile] gebruikershandleiding](../ui/user-guide.md)voor informatie over hoe u toegang kunt krijgen tot profielgegevens via de gebruikersinterface.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Lees voordat u verdergaat de gids [Aan de](getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Laatste voorbeeldstatus weergeven {#view-last-sample-status}

U kunt een verzoek van de GET aan het `/previewsamplestatus` eindpunt uitvoeren om de details voor de laatste succesvolle steekproefbaan te bekijken die voor uw IMS Organisatie werd in werking gesteld. Dit omvat het totale aantal profielen in de steekproef, evenals de metrische profieltelling, of het totale aantal profielen uw organisatie binnen Experience Platform heeft. Het aantal profielen wordt gegenereerd na het samenvoegen van profielfragmenten om één profiel voor elke afzonderlijke klant te vormen. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. De voorbeeldtaak wordt regelmatig vernieuwd terwijl Profielgegevens worden opgenomen om een up-to-date totaal aantal profielen in Platform te bieden.

**API-indeling**

```http
GET /previewsamplestatus
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat de details voor de laatste geslaagde voorbeeldtaak die voor de IMS-organisatie is uitgevoerd.

>[!NOTE]
>
>In dit voorbeeld is de reactie `numRowsToRead` en `totalRows` is deze gelijk aan elkaar. Afhankelijk van het aantal profielen dat uw organisatie in Experience Platform heeft, kan dit het geval zijn. Over het algemeen verschillen deze twee getallen echter, waarbij `numRowsToRead` het getal kleiner is omdat het de steekproef vertegenwoordigt als een subset van het totale aantal profielen (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `numRowsToRead` | Het totale aantal samengevoegde profielen in de steekproef. |
| `cosmosDocCount` | Het totale aantal documenten in Cosmos. |
| `totalFragmentCount` | Het totale aantal profielfragmenten in het profielarchief. |
| `lastSuccessfulBatchTimestamp` | Laatste succesvolle tijdstempel voor batch-opname. |
| `streamingDriven` | *Dit veld is afgekeurd en heeft geen betekenis voor de reactie.* |
| `totalRows` | Het totale aantal samengevoegde profielen in het Experience-platform, ook wel &#39;profile count&#39; genoemd. |
| `lastBatchId` | Laatste batch-opname-id. |
| `status` | Status van laatste sample. |
| `samplingRatio` | Verhouding van de samengevoegde profielen (`numRowsToRead`) tot het totaal van de samengevoegde profielen (`totalRows`), uitgedrukt als een percentage in decimale notatie. |
| `mergeStrategy` | Samenvoegingsstrategie gebruikt in de steekproef. |
| `lastSampledTimestamp` | Laatste succesvolle voorbeeld van tijdstempel. |

## Profieldistributie per gegevensset weergeven

Om de distributie van profielen door dataset te zien, kunt u een verzoek van de GET aan het `/previewsamplestatus/report/dataset` eindpunt uitvoeren.

**API-indeling**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet voor de gespecificeerde datum bestaat, zal een fout 404 zijn teruggekeerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de `date` parameter gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat een `data` array met daarin een lijst met gegevenssetobjecten. De getoonde reactie is beknot om drie datasets te tonen.

>[!NOTE]
>
>Als er meerdere rapporten bestonden voor de datum, wordt alleen de laatste geretourneerd. Als een datasetrapport niet voor de verstrekte datum bestond, zou de Status 404 van HTTP (niet Gevonden) zijn teruggekeerd.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `sampleCount` | Het totale aantal gesamplede profielen met deze gegevensset-id. |
| `samplePercentage` | De waarde `sampleCount` als een percentage van het totale aantal samengevoegde profielen (de `numRowsToRead` waarde als geretourneerd in de [laatste voorbeeldstatus](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen met deze dataset-id. |
| `fullIDsPercentage` | De waarde `fullIDsCount` als een percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde die wordt geretourneerd in de [laatste voorbeeldstatus](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `name` | De naam van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `description` | De beschrijving van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `value` | De id van de gegevensset. |
| `streamingIngestionEnabled` | Of de dataset voor het stromen opname wordt toegelaten. |
| `createdUser` | De gebruikers-id van de gebruiker die de gegevensset heeft gemaakt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een `date` parameter tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen `date` parameter is opgegeven, wordt het meest recente rapport geretourneerd. |



## Profieldistributie weergeven via naamruimte

U kunt een verzoek van de GET aan het `/previewsamplestatus/report/namespace` eindpunt uitvoeren om de mislukking door identiteitsnamespace over alle samengevoegde profielen in uw opslag van het Profiel te bekijken. Identiteitsnaamruimten zijn een belangrijk onderdeel van de Adobe Experience Platform Identity Service dat als indicatoren dient voor de context waarop de klantgegevens betrekking hebben. Ga voor meer informatie naar het overzicht [van de naamruimte van de](../../identity-service/namespaces.md)identiteit.

>[!NOTE]
>
>Het totale aantal profielen per naamruimte (door de waarden voor elke naamruimte bij elkaar op te tellen) is altijd hoger dan de metrische waarde voor het aantal profielen, omdat één profiel aan meerdere naamruimten kan worden gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

**API-indeling**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet voor de gespecificeerde datum bestaat, zal een fout 404 zijn teruggekeerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

Het volgende verzoek specificeert geen `date` parameter en zal daarom het meest recente rapport terugkeren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat een `data` array met afzonderlijke objecten die de details voor elke naamruimte bevatten. De getoonde reactie is afgebroken om vier naamruimten te tonen.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `sampleCount` | Het totale aantal gesamplede profielen in de naamruimte. |
| `samplePercentage` | De waarde `sampleCount` als een percentage samengevoegde profielen (de `numRowsToRead` waarde die in de [laatste voorbeeldstatus](#view-last-sample-status)is geretourneerd), uitgedrukt in decimale notatie. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een `date` parameter tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen `date` parameter is opgegeven, wordt het meest recente rapport geretourneerd. |
| `fullIDsFragmentCount` | Het totale aantal profielfragmenten in de naamruimte. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen in de naamruimte. |
| `fullIDsPercentage` | De waarde `fullIDsCount` als een percentage van het totaal van de samengevoegde profielen (de `totalRows` waarde die in de [laatste steekproefstatus](#view-last-sample-status)is geretourneerd), uitgedrukt in decimale notatie. |
| `code` | The `code` for the namespace. Dit is te vinden wanneer het werken met namespaces gebruikend de [Dienst API](../../identity-service/api/list-namespaces.md) van de Identiteit van Adobe Experience Platform en wordt ook bedoeld als symbool [!UICONTROL van de] Identiteit in de UI van het Experience Platform. Ga voor meer informatie naar het overzicht [van de naamruimte van de](../../identity-service/namespaces.md)identiteit. |
| `value` | De `id` waarde voor de naamruimte. Dit is te vinden wanneer het werken met namespaces gebruikend de [Dienst API](../../identity-service/api/list-namespaces.md)van de Identiteit. |

## Volgende stappen

U kunt gelijkaardige ramingen en voorproeven ook gebruiken om samenvatting-vlakke informatie betreffende uw segmentdefinities te bekijken om u te helpen het verwachte publiek isoleren. Als u gedetailleerde stappen wilt vinden voor het werken met segmentvoorvertoningen en -schattingen met behulp van de [!DNL Adobe Experience Platform Segmentation Service] API, raadpleegt u de handleiding voor [voorvertoningen en schattingen van eindpunten](../../segmentation/api/previews-and-estimates.md), onderdeel van de [!DNL Segmentation] API-ontwikkelaarsgids.

