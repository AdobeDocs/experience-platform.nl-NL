---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;voorvertoning;voorbeeld
title: Voorbeeld van voorbeeldstatus (profiel voorvertoning) API-eindpunt
description: Het eindpunt van de voorproefvoorbeeldstatus van het Real-Time Profiel van de Klant API staat u toe om de recentste succesvolle steekproef van uw gegevens van het Profiel, de distributie van het lijstprofiel door dataset en door identiteit, voor te vertonen en rapporten te produceren die datasetoverlapping, identiteitsoverlap, en ongestipte profielen tonen.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: d1eb9191c74add1ab21cd268327bab9a3255d182
workflow-type: tm+mt
source-wordcount: '2904'
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

U kunt een GET-aanvraag naar het `/previewsamplestatus` -eindpunt uitvoeren om de details te bekijken van de laatste voorbeeldtaak die voor uw organisatie is uitgevoerd. Dit omvat het totale aantal profielen in de steekproef, evenals de metrische profieltelling, of het totale aantal profielen uw organisatie heeft binnen Experience Platform.

Het aantal profielen wordt gegenereerd na het samenvoegen van profielfragmenten om één profiel voor elke afzonderlijke klant te vormen. Met andere woorden, wanneer profielfragmenten samen worden samengevoegd, wordt een getal van &quot;1&quot;-profiel geretourneerd omdat ze allemaal verwant zijn aan hetzelfde individu.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. De voorbeeldtaak wordt regelmatig vernieuwd terwijl profielgegevens worden ingevoerd om een up-to-date totaal aantal profielen in Experience Platform te bieden.

**API formaat**

```http
GET /previewsamplestatus
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

De reactie bevat de details voor de laatste geslaagde voorbeeldtaak die voor de organisatie is uitgevoerd.

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
|---|---|
| `numRowsToRead` | Het totale aantal samengevoegde profielen in de steekproef. |
| `sampleJobRunning` | Een Booleaanse waarde die `true` retourneert wanneer een voorbeeldtaak wordt uitgevoerd. Hiermee krijgt u transparantie in de latentie die optreedt wanneer een batchbestand wordt geüpload naar het moment dat het daadwerkelijk wordt toegevoegd aan de profielopslag. |
| `docCount` | Totaal aantal documenten in database. |
| `totalFragmentCount` | Het totale aantal profielfragmenten in het archief met profielen. |
| `lastSuccessfulBatchTimestamp` | Tijdstempel voor laatste succes bij het invoeren van batch. |
| `streamingDriven` | *Dit gebied is afgekeurd en bevat geen betekenis aan de reactie.* |
| `totalRows` | Het totale aantal samengevoegde profielen in Experience Platform, ook wel &#39;aantal profielen&#39; genoemd. |
| `lastBatchId` | Laatste batch-inname-id. |
| `status` | Status van laatste sample. |
| `samplingRatio` | Verhouding van samengevoegde profielen (`numRowsToRead`) tot het totaal van samengevoegde profielen (`totalRows`), uitgedrukt als een percentage in decimale notatie. |
| `mergeStrategy` | Samenvoegingsstrategie gebruikt in de steekproef. |
| `lastSampledTimestamp` | Laatste succesvolle voorbeeld van tijdstempel. |

## Profieldistributie per gegevensset weergeven

Als u de verdeling van profielen op gegevensset wilt zien, kunt u een GET-aanvraag naar het eindpunt van `/previewsamplestatus/report/dataset` uitvoeren.

**API formaat**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

De reactie bevat een array `data` die een lijst met gegevenssetobjecten bevat. De getoonde reactie is beknot om drie datasets te tonen.

>[!NOTE]
>
>Als er meerdere rapporten voor de datum bestaan, wordt alleen het laatste rapport geretourneerd. Als er geen gegevenssetrapport bestaat voor de opgegeven datum, wordt HTTP Status 404 (Niet gevonden) geretourneerd.

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
| `samplePercentage` | `sampleCount` als percentage van het totale aantal gesamplede profielen (de `numRowsToRead` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen met deze dataset-id. |
| `fullIDsPercentage` | `fullIDsCount` als percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `name` | De naam van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `description` | De beschrijving van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `value` | De id van de gegevensset. |
| `streamingIngestionEnabled` | Of de dataset voor het stromen opname wordt toegelaten. |
| `createdUser` | De gebruikers-id van de gebruiker die de gegevensset heeft gemaakt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |

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

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt geen parameter `date` opgegeven en wordt daarom het meest recente rapport geretourneerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

De reactie bevat een array `data` met afzonderlijke objecten die de details voor elke naamruimte bevatten. De getoonde reactie is afgebroken om vier naamruimten te tonen.

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
| `samplePercentage` | `sampleCount` als percentage gesamplede profielen (de `numRowsToRead` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |
| `fullIDsFragmentCount` | Het totale aantal profielfragmenten in de naamruimte. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen in de naamruimte. |
| `fullIDsPercentage` | `fullIDsCount` als percentage van totaal samengevoegde profielen (de `totalRows` waarde zoals teruggekeerd in de [&#x200B; laatste steekproefstatus &#x200B;](#view-last-sample-status)), die in decimaal formaat wordt uitgedrukt. |
| `code` | De `code` voor de naamruimte. Dit kan worden gevonden wanneer het werken met namespaces gebruikend [&#x200B; de Dienst API van de Identiteit van Adobe Experience Platform &#x200B;](../../identity-service/api/list-namespaces.md) en ook bedoeld als [!UICONTROL Identity symbol] in Experience Platform UI. Om meer te leren, bezoek het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../../identity-service/features/namespaces.md). |
| `value` | De `id` -waarde voor de naamruimte. Dit kan worden gevonden wanneer het werken met namespaces gebruikend de [&#x200B; Dienst API van de Identiteit &#x200B;](../../identity-service/api/list-namespaces.md). |

## Genereer het overlappingsrapport voor de gegevensset

Het rapport van de datasetoverlapping verstrekt zicht in de samenstelling van de opslag van het Profiel van uw organisatie door de datasets bloot te stellen die het meest aan uw adresseerbare publiek (samengevoegde profielen) bijdragen. Naast het verstrekken van inzichten in uw gegevens, kan dit rapport u acties helpen om vergunningsgebruik te optimaliseren, zoals het plaatsen van vervalsingen voor bepaalde datasets.

U kunt het rapport van de datasetoverlapping produceren door een verzoek van GET aan het `/previewsamplestatus/report/dataset/overlap` eindpunt uit te voeren.

Voor geleidelijke instructies die hoe te om het rapport van de datasetoverlapping te produceren gebruikend de bevellijn of Postman UI schetsen, gelieve te verwijzen naar [&#x200B; producerend de datasetoverlapping rapporttutorial &#x200B;](../tutorials/dataset-overlap-report.md).

**API formaat**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als meerdere rapporten op dezelfde datum zijn uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een succesvol verzoek keert de Status 200 van HTTP terug (OK) en de dataset overlapt rapport.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `data` | Het `data` -object bevat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke aantal profielen. |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |

### Het rapport van de gegevensset-overlapping interpreteren

De resultaten van het rapport kunnen van de datasets en profieltellingen in de reactie worden geïnterpreteerd. Bekijk het volgende voorbeeldrapport `data` -object:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dit rapport bevat de volgende informatie:

* Er zijn 123 profielen die bestaan uit gegevens die afkomstig zijn uit de volgende datasets: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98` .
* Er zijn 454.412 profielen die bestaan uit gegevens die afkomstig zijn uit deze twee gegevenssets: `5d92921872831c163452edc8` en `5eb2cdc6fa3f9a18a7592a98` .
* Er zijn 107 profielen die slechts van gegevens van dataset `5eeda0032af7bb19162172a7` worden samengesteld.
* Er zijn in totaal 454.642 profielen in de organisatie.

## Rapport voor overlappende naamruimte genereren {#identity-overlap-report}

De identiteitsnaamruimte overlapt rapport geeft inzicht in de samenstelling van de opslag van het Profiel van uw organisatie door de naamruimten toegankelijk te maken die het meest bijdragen aan uw adresseerbare publiek (samengevoegde profielen). Dit omvat zowel de standaard naamruimten die door Adobe worden verschaft als de aangepaste naamruimten die door uw organisatie worden gedefinieerd.

U kunt het rapport voor naamruimte-overlapping genereren door een GET-aanvraag naar het `/previewsamplestatus/report/namespace/overlap` -eindpunt uit te voeren.

**API formaat**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als meerdere rapporten op dezelfde datum zijn uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een succesvol verzoek retourneert HTTP Status 200 (OK) en de naamruimte overlapt het rapport.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `data` | Het `data` -object bevat door komma&#39;s gescheiden lijsten met unieke combinaties van naamruimtecodes en hun respectievelijke profielaantallen. |
| Namespace-codes | `code` is een kort formulier voor elke naamruimtenaam van een identiteit. Een afbeelding van elk `code` aan zijn `name` kan worden gevonden gebruikend [&#x200B; de Dienst API van de Identiteit van Adobe Experience Platform &#x200B;](../../identity-service/api/list-namespaces.md). `code` wordt ook wel de [!UICONTROL Identity symbol] genoemd in de gebruikersinterface van Experience Platform. Om meer te leren, bezoek het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | De tijdstempel van het rapport. Als een parameter `date` tijdens het verzoek werd verstrekt, is het teruggekeerde rapport voor de verstrekte datum. Als er geen parameter `date` is opgegeven, wordt het meest recente rapport geretourneerd. |

### Rapport voor overlappende naamruimte interpreteren

De resultaten van het rapport kunnen van de identiteiten en profieltellingen in de reactie worden geïnterpreteerd. De numerieke waarde van elke rij vertelt u hoeveel profielen uit die nauwkeurige combinatie standaard en douaneidentiteitsnamespaces bestaan.

Bekijk het volgende fragment van het object `data` :

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Dit rapport bevat de volgende informatie:

* Er zijn 142 profielen die zijn samengesteld uit `AAID` , `ECID` en `Email` standaard-id&#39;s en uit een aangepaste naamruimte `crmid` identity.
* Er zijn 24 profielen die bestaan uit `AAID` en `ECID` naamruimten.
* Er zijn 6.565 profielen die alleen een `ECID` id bevatten.

## Rapport voor niet-geselecteerde profielen genereren

U kunt de samenstelling van de opslag van het Profiel van uw organisatie door het niet-gesloten profielrapport meer zichtbaar maken. Een &quot;niet-gekoppeld&quot; profiel is een profiel dat slechts één profielfragment bevat. Een &quot;onbekend&quot; profiel is een profiel dat is gekoppeld aan pseudonieme naamruimten zoals `ECID` en `AAID` . Onbekende profielen zijn inactief, wat betekent dat er geen nieuwe gebeurtenissen zijn toegevoegd voor de opgegeven periode. Het rapport met niet-opgeslagen profielen bevat een indeling van profielen voor een periode van 7, 30, 60, 90 en 120 dagen.

U kunt het rapport met niet-gekoppelde profielen genereren door een GET-aanvraag uit te voeren naar het eindpunt van `/previewsamplestatus/report/unstitchedProfiles` .

**API formaat**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Verzoek**

Het volgende verzoek retourneert het rapport met niet-ingestelde profielen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een succesvolle aanvraag retourneert HTTP Status 200 (OK) en het rapport met niet-opgeslagen profielen.

>[!NOTE]
>
>In het kader van deze handleiding is het rapport afgekapt, zodat alleen `"120days"` - en `7days` -tijdsperioden worden opgenomen. Het volledige rapport met ongeordende profielen bevat een uitsplitsing van profielen voor een periode van 7, 30, 60, 90 en 120 dagen.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `data` | Het `data` -object bevat de informatie die wordt geretourneerd voor het rapport met niet-gekoppelde profielen. |
| `totalNumberOfProfiles` | Het totale aantal unieke profielen in het archief Profiel. Dit is gelijk aan het adresseerbare aantal. Het bevat zowel bekende als niet-gebonden profielen. |
| `totalNumberOfEvents` | Het totale aantal ExperienceEvents in het archief met profielen. |
| `unstitchedProfiles` | Een object met een uitsplitsing van niet-opgegeven profielen naar tijdsperiode. Het rapport met niet-opgeslagen profielen bevat een uitsplitsing van profielen voor tijdvakken van 7, 30, 60, 90 en 120 dagen. |
| `countOfProfiles` | Het aantal niet-gekoppelde profielen voor de tijdsperiode of het aantal niet-gebonden profielen voor de naamruimte. |
| `eventsAssociated` | Het aantal ExperienceEvents voor het tijdbereik of het aantal gebeurtenissen voor de naamruimte. |
| `nsDistribution` | Een object dat afzonderlijke naamruimten bevat met de distributie van niet-gekoppelde profielen en gebeurtenissen voor elke naamruimte. Opmerking: het totaal `countOfProfiles` voor elke naamruimte van de identiteit in het `nsDistribution` -object wordt gelijk aan de `countOfProfiles` voor de tijdsperiode. Hetzelfde geldt voor `eventsAssociated` per naamruimte en het totaal `eventsAssociated` per tijdsperiode. |
| `reportTimestamp` | De tijdstempel van het rapport. |

### Het rapport met niet-opgeslagen profielen interpreteren

De resultaten van het rapport kunnen insight een overzicht geven van het aantal niet-opgeslagen en niet-actieve profielen dat uw organisatie heeft in de Profile Store.

Bekijk het volgende fragment van het object `data` :

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Dit rapport bevat de volgende informatie:

* Er zijn 1.782 profielen die slechts één profielfragment bevatten en de afgelopen zeven dagen geen nieuwe gebeurtenissen hebben.
* Er zijn 29.151 ExperienceEvents die zijn gekoppeld aan de 1.782 niet-ingestelde profielen.
* Er zijn 1.734 niet-gekoppelde profielen die één profielfragment uit de naamruimte ECID bevatten.
* Er zijn 28.591 gebeurtenissen gekoppeld aan de 1.734 niet-gekoppelde profielen die één profielfragment uit de naamruimte van de ECID bevatten.

## Volgende stappen

Nu u weet hoe te om steekproefgegevens in de opslag van het Profiel voor te vertonen en veelvoudige rapporten over de gegevens in werking te stellen, kunt u de schatting en voorproefpunten van de Dienst API van de Segmentatie ook gebruiken om summiere-vlakke informatie betreffende uw segmentdefinities te bekijken. Deze informatie helpt u ervoor te zorgen dat u uw verwachte publiek isoleert. Om meer over het werken met voorproeven en ramingen te leren die de Segmentatie API gebruiken, gelieve de [&#x200B; voorproef en de gids van de schattingseindpunten &#x200B;](../../segmentation/api/previews-and-estimates.md) te bezoeken.

