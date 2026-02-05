---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;voorvertoning;voorbeeld
title: Voorbeeld van voorbeeldstatus (profiel voorvertoning) API-eindpunt
description: Het eindpunt van de voorproefvoorbeeldstatus van het Real-Time Profiel van de Klant API staat u toe om de recentste succesvolle steekproef van uw gegevens van het Profiel, de distributie van het lijstprofiel door dataset en door identiteit, voor te vertonen en rapporten te produceren die datasetoverlapping, identiteitsoverlap, en ongestipte profielen tonen.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 399b76f260732015f691fd199c977d6f7e772b01
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# Voorvertoning voorbeeldstatuseindpunt (voorvertoning profiel)

Met Adobe Experience Platform kunt u klantgegevens uit meerdere bronnen invoeren om een robuust, uniform profiel voor elk van uw individuele klanten te maken. Als gegevens in Experience Platform worden ingevoerd, wordt een voorbeeldtaak uitgevoerd om het aantal profielen en andere gegevensgerelateerde gegevens in het realtime-profiel van de klant bij te werken.

De resultaten van deze voorbeeldbaan kunnen worden bekeken gebruikend het `/previewsamplestatus` eindpunt, deel van Real-Time het Profiel van de Klant API. Dit eindpunt kan ook worden gebruikt om van profieldistributies door zowel dataset als identiteit namespace een lijst te maken, evenals veelvoudige rapporten te produceren om zicht in de samenstelling van de opslag van het Profiel van uw organisatie te bereiken. Deze gids doorloopt de stappen die worden vereist om deze metriek te bekijken gebruikend het `/previewsamplestatus` API eindpunt.

>[!NOTE]
>
>Er zijn schatting en voorproef eindpunten beschikbaar als deel van de Dienst API van de Segmentatie van Adobe Experience Platform die u toestaan om samenvatting-vlakke informatie betreffende segmentdefinities te bekijken helpen ervoor zorgen u het verwachte publiek isoleert. Om gedetailleerde stappen voor het werken met voorproef te vinden en eindpunten te schatten, gelieve te bezoeken de [&#x200B; voorproeven en de gids van geschatte eindpunten &#x200B;](../../segmentation/api/previews-and-estimates.md), een deel van de [!DNL Segmentation] API ontwikkelaarsgids.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Real-Time Customer Profile]  API &#x200B;](https://www.adobe.com/go/profile-apis-en). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Profielfragmenten versus samengevoegde profielen

Deze handleiding verwijst naar zowel &quot;profielfragmenten&quot; als &quot;samengevoegde profielen&quot;. Het is belangrijk dat u het verschil tussen deze termen begrijpt voordat u verdergaat.

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, heeft uw organisatie waarschijnlijk veelvoudige profielfragmenten met betrekking tot die enige klant die in veelvoudige datasets verschijnt.

Wanneer profielfragmenten in Experience Platform worden opgenomen, worden ze samengevoegd (op basis van een samenvoegbeleid) om één profiel voor die klant te maken. Daarom is het totale aantal profielfragmenten waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel uit veelvoudige fragmenten bestaat.

Meer over profielen en hun rol binnen Experience Platform leren, gelieve te beginnen door het [&#x200B; overzicht van het Profiel van de Klant in real time &#x200B;](../home.md) te lezen.

## Hoe de voorbeeldtaak wordt geactiveerd

Aangezien gegevens die voor het Profiel van de Klant in real time worden toegelaten in [!DNL Experience Platform] worden opgenomen, wordt het opgeslagen binnen de gegevensopslag van het Profiel. Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 3% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. De wijze waarop het monster wordt geactiveerd, hangt af van het type inname dat wordt gebruikt:

* Voor **het stromen gegevenswerkschema&#39;s**, wordt een controle gedaan op een uurbasis om te bepalen als de 3% toename of dalingsdrempel is voldaan aan. Als dit het geval is, wordt er automatisch een voorbeeldtaak geactiveerd om de telling bij te werken.
* Voor **partijingestie**, binnen 15 minuten van met succes het opnemen van een partij in de opslag van het Profiel, als de 3% verhoging of dalingsdrempel wordt ontmoet, wordt een baan in werking gesteld om de telling bij te werken. Met behulp van de profiel-API kunt u een voorvertoning weergeven van de meest recente voorbeeldtaak en de distributie van het lijstprofiel via gegevensset en naamruimte op naam.

Het aantal profielen en de profielen op basis van naamruimtewaarden zijn ook beschikbaar in de sectie [!UICONTROL Profiles] van de gebruikersinterface van Experience Platform. Voor informatie over hoe te om tot de gegevens van het Profiel toegang te hebben gebruikend UI, gelieve de [[!DNL Profile]  gids UI &#x200B;](../ui/user-guide.md) te bezoeken.

## Laatste voorbeeldstatus weergeven {#view-last-sample-status}

U kunt de details voor de laatste succesvolle steekproefbaan bekijken die voor uw organisatie door een verzoek van GET aan het `/previewsamplestatus` eindpunt werd in werking gesteld. Dit rapport bevat het totale aantal profielen in het voorbeeld, evenals het aantal profielen of het totale aantal profielen dat uw organisatie in Experience Platform heeft.

Het aantal profielen wordt gegenereerd na het samenvoegen van profielfragmenten om één profiel voor elke afzonderlijke klant te vormen. Met andere woorden, wanneer profielfragmenten samen worden samengevoegd, wordt een getal van &quot;1&quot;-profiel geretourneerd omdat ze allemaal verwant zijn aan hetzelfde individu.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. De voorbeeldtaak wordt regelmatig vernieuwd terwijl profielgegevens worden ingevoerd om een up-to-date totaal aantal profielen in Experience Platform te bieden.

**API formaat**

```http
GET /previewsamplestatus
```

**Verzoek**

+++ Een voorbeeldverzoek om de laatste voorbeeldstatus weer te geven.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP terug en omvat de details voor de laatste succesvolle steekproefbaan die voor de organisatie in werking werd gesteld.

+++ Een voorbeeldreactie die de laatste voorbeeldstatus bevat.

>[!NOTE]
>
>In dit voorbeeld zijn `numRowsToRead` en `totalRows` gelijk aan elkaar. Afhankelijk van het aantal profielen dat uw organisatie in Experience Platform heeft, kan dit het geval zijn. Over het algemeen verschillen deze twee getallen echter, waarbij `numRowsToRead` het laagste getal is omdat het de steekproef vertegenwoordigt als een subset van het totale aantal profielen (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | Het totale aantal samengevoegde profielen in de steekproef. |
| `sampleJobRunning` | Een Booleaanse waarde die `true` retourneert wanneer een voorbeeldtaak wordt uitgevoerd. Hiermee krijgt u transparantie in de latentie die optreedt wanneer een batchbestand wordt geüpload naar het moment dat het daadwerkelijk wordt toegevoegd aan de profielopslag. |
| `docCount` | Totaal aantal documenten in database. |
| `totalFragmentCount` | Het totale aantal profielfragmenten in het archief met profielen. |
| `lastSuccessfulBatchTimestamp` | Tijdstempel voor laatste succes bij het invoeren van batch. |
| `streamingDriven` | *Dit gebied is afgekeurd en bevat geen betekenis aan de reactie.* |
| `totalRows` | Het totale aantal samengevoegde profielen in Experience Platform, ook bekend als het aantal profielen. |
| `lastBatchId` | Laatste batch-inname-id. |
| `status` | Status van laatste sample. |
| `samplingRatio` | Verhouding van samengevoegde profielen (`numRowsToRead`) tot het totaal van samengevoegde profielen (`totalRows`), uitgedrukt als een percentage in decimale notatie. |
| `mergeStrategy` | Samenvoegingsstrategie gebruikt in de steekproef. |
| `lastSampledTimestamp` | Laatste succesvolle voorbeeld van tijdstempel. |

+++

## Profieldistributie per gegevensset weergeven

U kunt de verdeling van profielen door dataset zien door een GET- verzoek aan het `/previewsamplestatus/report/dataset` eindpunt te doen.

**API formaat**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. | `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

+++ Een steekproefverzoek om de profieldistributie door dataset terug te winnen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Reactie**

>[!NOTE]
>
>Als er meerdere rapporten voor de datum bestaan, wordt alleen het laatste rapport geretourneerd. Als er geen gegevenssetrapport bestaat voor de opgegeven datum, wordt HTTP Status 404 (Niet gevonden) geretourneerd.

Een geslaagde reactie retourneert HTTP-status 200 en bevat een `data` -array die een lijst met gegevenssetobjecten bevat.

+++ Een steekproefreactie die de recentste datasetvoorwerpen bevat.

>[!NOTE]
>
>De volgende getoonde reactie is beknot om drie datasets te tonen.

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
| -------- | ----------- |
| `sampleCount` | Het totale aantal gesamplede profielen met deze gegevensset-id. |
| `samplePercentage` | `sampleCount` als percentage van het totale aantal gesamplede profielen (de `numRowsToRead` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen met deze dataset-id. |
| `fullIDsPercentage` | `fullIDsCount` als percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `name` | De naam van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `description` | De beschrijving van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `value` | De id van de gegevensset. |
| `streamingIngestionEnabled` | Of de dataset voor het stromen opname wordt toegelaten. |
| `createdUser` | De gebruikers-id van de gebruiker die de gegevensset heeft gemaakt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |

+++

## Profieldistributie weergeven op naamruimte van identiteit

U kunt een GET-aanvraag naar het eindpunt van `/previewsamplestatus/report/namespace` uitvoeren om de uitsplitsing naar naamruimte van de identiteit weer te geven voor alle samengevoegde profielen in het archief Profiel. Dit geldt zowel voor de standaardidentiteiten die door Adobe worden geleverd als voor de aangepaste identiteiten die door uw organisatie zijn gedefinieerd.

Identiteitsnaamruimten zijn een belangrijk onderdeel van de Adobe Experience Platform Identity Service dat als indicatoren dient voor de context waarop de klantgegevens betrekking hebben. Om meer te leren, begin door het [&#x200B; overzicht van identiteitskaart te lezen namespace &#x200B;](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Het totale aantal profielen per naamruimte (door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan de metrische waarde van het aantal profielen, omdat één profiel aan meerdere naamruimten kan worden gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

**API formaat**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `date` | Geeft de datum aan van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: `YYYY-MM-DD`. | `date=2025-6-20` |

**Verzoek**

In het volgende verzoek wordt geen parameter `date` opgegeven en wordt het meest recente rapport geretourneerd.

+++ Een steekproefverzoek om het meest recente rapport voor profieldistributie door namespace terug te keren. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Reactie**

Een succesvol antwoord retourneert HTTP-status 200 en bevat een `data` -array, met afzonderlijke objecten die de details voor elke naamruimte bevatten. De getoonde reactie is afgebroken om vier naamruimten te tonen.

+++ Een voorbeeldreactie bevat informatie over de profieldistributie per naamruimte.

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
| -------- | ----------- |
| `sampleCount` | Het totale aantal gesamplede profielen in de naamruimte. |
| `samplePercentage` | `sampleCount` als percentage gesamplede profielen (de `numRowsToRead` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |
| `fullIDsFragmentCount` | Het totale aantal profielfragmenten in de naamruimte. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen in de naamruimte. |
| `fullIDsPercentage` | `fullIDsCount` als percentage van totaal samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `code` | De `code` voor de naamruimte. Dit kan worden gevonden wanneer het werken met namespaces gebruikend [&#x200B; de Dienst API van de Identiteit van Adobe Experience Platform &#x200B;](../../identity-service/api/list-namespaces.md) en ook bedoeld als [!UICONTROL Identity symbol] in Experience Platform UI. Om meer te leren, bezoek het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../../identity-service/features/namespaces.md). |
| `value` | De `id` -waarde voor de naamruimte. Dit kan worden gevonden wanneer het werken met namespaces gebruikend de [&#x200B; Dienst API van de Identiteit &#x200B;](../../identity-service/api/list-namespaces.md). |

+++

## Een lijst maken van de gegevenssetstatistieken {#dataset-stats}

U kunt een rapport produceren dat statistieken over de dataset door een GET- verzoek aan het `/previewsamplestatus/report/dataset_stats` eindpunt te doen geeft.

**API formaat**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Verzoek**

+++ Een steekproefverzoek om het rapport van de datasetstatistieken te produceren.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over de statistieken van de dataset terug.

+++ Een steekproefreactie die informatie over de statistieken van de dataset bevat.

>[!NOTE]
>
>De volgende reactie is beknot om drie datasets te tonen.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `120days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 120 dagen zullen blijven. |
| `14days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 14 dagen zullen blijven. |
| `30days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 30 dagen zullen blijven. |
| `365days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 365 dagen zullen blijven. |
| `60days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 60 dagen zullen blijven. |
| `7days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 7 dagen zullen blijven. |
| `90days` | Het aantal verslagen die in de dataset na een gegevensvervaldatum van 90 dagen zullen blijven. |
| `datasetId` | De id van de gegevensset. |
| `datasetType` | Het gegevenstype van de dataset. Deze waarde kan `Profiles` of `ExperienceEvents` zijn. |
| `percentEvents` | Het percentage van de verslagen van de Gebeurtenissen van de Ervaring die binnen de dataset zijn. |
| `percentProfiles` | Het percentage van de verslagen van het Profiel die binnen de dataset zijn. |
| `profileFragments` | Het totale aantal profielfragmenten dat in de dataset bestaat. |
| `records` | Het totale aantal profielverslagen die in de dataset worden opgenomen. |
| `totalProfiles` | Het totale aantal profielen dat in de gegevensset wordt opgenomen. |

+++

## Volgende stappen

Nu u weet hoe te om steekproefgegevens in de opslag van het Profiel voor te vertonen en veelvoudige rapporten over de gegevens in werking te stellen, kunt u de schatting en voorproefpunten van de Dienst API van de Segmentatie ook gebruiken om summiere-vlakke informatie betreffende uw segmentdefinities te bekijken. Deze informatie helpt u ervoor te zorgen dat u uw verwachte publiek isoleert. Om meer over het werken met voorproeven en ramingen te leren die de Segmentatie API gebruiken, gelieve de [&#x200B; voorproef en de gids van de schattingseindpunten &#x200B;](../../segmentation/api/previews-and-estimates.md) te bezoeken.

