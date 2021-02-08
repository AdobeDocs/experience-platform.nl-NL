---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;voorvertoning;voorbeeld
title: Voorbeeld van voorbeeldstatus (Profile Preview) API-eindpunt
description: Met het voorbeeldstatuseindpunt van de voorvertoning, onderdeel van de Real-Time Customer Profile API, kunt u een voorvertoning weergeven van het meest recente voorbeeld van de profielgegevens, en kunt u de distributie van het lijstprofiel per dataset en per naamruimte in Adobe Experience Platform bekijken.
topic: guide
translation-type: tm+mt
source-git-commit: 5266c393b034d1744134522cf1769304f39733da
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Voorvertoning voorbeeldstatuseindpunt (voorvertoning profiel)

Met Adobe Experience Platform kunt u klantgegevens uit meerdere bronnen invoeren om robuuste, uniforme profielen voor individuele klanten te maken. Aangezien gegevens die voor het Profiel van de Klant in real time worden toegelaten in [!DNL Platform] worden opgenomen, wordt het opgeslagen binnen de gegevensopslag van het Profiel.

Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 5% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. De wijze waarop het monster wordt geactiveerd, hangt af van het type inname dat wordt gebruikt:

* Voor **streaminggegevensworkflows** wordt een controle per uur uitgevoerd om te bepalen of aan de drempel van 5% verhoging of verlaging is voldaan. Als dit het geval is, wordt er automatisch een voorbeeldtaak geactiveerd om de telling bij te werken.
* Voor **batch-opname** wordt binnen 15 minuten nadat een batch in de profielopslag is opgenomen, een taak uitgevoerd om de telling bij te werken als aan de drempel van 5% verhoging of verlaging is voldaan. Met behulp van de profiel-API kunt u een voorvertoning weergeven van de meest recente voorbeeldtaak en de distributie van het lijstprofiel via gegevensset en naamruimte.

Deze metriek zijn ook beschikbaar binnen [!UICONTROL Profielen] sectie van de UI van het Experience Platform. Voor informatie over hoe te om tot de gegevens van het Profiel toegang te hebben gebruikend UI, gelieve [[!DNL Profile] gebruikersgids](../ui/user-guide.md) te bezoeken.

>[!NOTE]
>
>Er zijn schatting en voorproef eindpunten beschikbaar als deel van de Dienst API van de Segmentatie van Adobe Experience Platform die u toestaan om samenvatting-vlakke informatie betreffende segmentdefinities te bekijken helpen ervoor zorgen u het verwachte publiek isoleert. Voor gedetailleerde stappen voor het werken met segmentvoorproef en schattingseindpunten, gelieve te bezoeken [voorproeven en schattingen eindpuntgids](../../segmentation/api/previews-and-estimates.md), deel van [!DNL Segmentation] API ontwikkelaarsgids.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Lees voordat u doorgaat de [Aan de slag-handleiding](getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Profielfragmenten versus samengevoegde profielen

Deze handleiding verwijst naar zowel &quot;profielfragmenten&quot; als &quot;samengevoegde profielen&quot;. Het is belangrijk dat u het verschil tussen deze termen begrijpt voordat u verdergaat.

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd (op basis van het samenvoegbeleid) om één profiel voor die klant te maken. Daarom is het totale aantal profielfragmenten waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel uit veelvoudige fragmenten bestaat.

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
>In dit voorbeeldantwoord zijn `numRowsToRead` en `totalRows` gelijk aan elkaar. Afhankelijk van het aantal profielen dat uw organisatie in Experience Platform heeft, kan dit het geval zijn. Over het algemeen verschillen deze twee getallen echter, waarbij `numRowsToRead` het laagste getal is omdat het de steekproef vertegenwoordigt als een subset van het totale aantal profielen (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
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
| `sampleJobRunning` | Een Booleaanse waarde die `true` retourneert wanneer een voorbeeldtaak wordt uitgevoerd. Hiermee krijgt u transparantie in de latentie die optreedt wanneer een batchbestand wordt geüpload naar het moment dat het daadwerkelijk wordt toegevoegd aan de profielopslag. |
| `cosmosDocCount` | Het totale aantal documenten in Cosmos. |
| `totalFragmentCount` | Het totale aantal profielfragmenten in het profielarchief. |
| `lastSuccessfulBatchTimestamp` | Laatste succesvolle tijdstempel voor batch-opname. |
| `streamingDriven` | *Dit veld is afgekeurd en heeft geen betekenis voor de reactie.* |
| `totalRows` | Het totale aantal samengevoegde profielen in Experience Platform, ook wel &#39;profieltelling&#39; genoemd. |
| `lastBatchId` | Laatste batch-opname-id. |
| `status` | Status van laatste sample. |
| `samplingRatio` | Verhouding van samengevoegde profielen (`numRowsToRead`) tot het totaal van samengevoegde profielen (`totalRows`), uitgedrukt als een percentage in decimale notatie. |
| `mergeStrategy` | Samenvoegingsstrategie gebruikt in de steekproef. |
| `lastSampledTimestamp` | Laatste succesvolle voorbeeld van tijdstempel. |

## Profieldistributie per gegevensset weergeven

Om de verdeling van profielen door dataset te zien, kunt u een verzoek van de GET aan het `/previewsamplestatus/report/dataset` eindpunt uitvoeren.

**API-indeling**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet voor de gespecificeerde datum bestaat, zal een fout 404 zijn teruggekeerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie omvat een `data`-array, die een lijst met gegevenssetobjecten bevat. De getoonde reactie is beknot om drie datasets te tonen.

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
| `samplePercentage` | De `sampleCount` als percentage van het totale aantal gesamplede gesamplede profielen (de `numRowsToRead`-waarde zoals geretourneerd in de [laatste voorbeeldstatus](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen met deze dataset-id. |
| `fullIDsPercentage` | De `fullIDsCount` als percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in [laatste steekproefstatus](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `name` | De naam van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `description` | De beschrijving van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `value` | De id van de gegevensset. |
| `streamingIngestionEnabled` | Of de dataset voor het stromen opname wordt toegelaten. |
| `createdUser` | De gebruikers-id van de gebruiker die de gegevensset heeft gemaakt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een `date` parameter tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |

## Profieldistributie weergeven via naamruimte

U kunt een verzoek van de GET aan het `/previewsamplestatus/report/namespace` eindpunt uitvoeren om de mislukking door identiteitsnamespace over alle samengevoegde profielen in uw opslag van het Profiel te bekijken. Identiteitsnaamruimten zijn een belangrijk onderdeel van de Adobe Experience Platform Identity Service dat als indicatoren dient voor de context waarop de klantgegevens betrekking hebben. Voor meer informatie gaat u naar [Naamruimte overzicht](../../identity-service/namespaces.md).

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
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie omvat een `data` serie, met individuele voorwerpen die de details voor elke namespace bevatten. De getoonde reactie is afgebroken om vier naamruimten te tonen.

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
| `samplePercentage` | De `sampleCount` als percentage van gesamplede samengevoegde profielen (de `numRowsToRead`-waarde zoals geretourneerd in de [laatste voorbeeldstatus](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een `date` parameter tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |
| `fullIDsFragmentCount` | Het totale aantal profielfragmenten in de naamruimte. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen in de naamruimte. |
| `fullIDsPercentage` | De `fullIDsCount` als percentage van het totaal van samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in [laatste steekproefstatus](#view-last-sample-status)), uitgedrukt in decimaal formaat. |
| `code` | De `code` voor de naamruimte. Dit is te vinden wanneer het werken met namespaces gebruikend [de Dienst API van de Identiteit van Adobe Experience Platform](../../identity-service/api/list-namespaces.md) en ook bedoeld als [!UICONTROL Identiteitssymbool] in Experience Platform UI. Voor meer informatie gaat u naar [Naamruimte overzicht](../../identity-service/namespaces.md). |
| `value` | De waarde `id` voor de naamruimte. Dit is te vinden wanneer het werken met namespaces gebruikend [Identiteitsdienst API](../../identity-service/api/list-namespaces.md). |

## Volgende stappen

Nu u weet hoe te om steekproefgegevens in de opslag van het Profiel voor te vertonen, kunt u de schatting en voorproefpunten van de Dienst API van de Segmentatie ook gebruiken om summiere-vlakke informatie betreffende uw segmentdefinities te bekijken. Deze informatie helpt om ervoor te zorgen u het verwachte publiek in uw segment isoleert. Als u meer wilt weten over het werken met segmentvoorvertoningen en -schattingen met de segmentatie-API, gaat u naar de [gids voor voorvertoningen en eindpunten voor ramingen](../../segmentation/api/previews-and-estimates.md).