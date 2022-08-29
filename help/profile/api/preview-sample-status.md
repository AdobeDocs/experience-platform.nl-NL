---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;voorvertoning;voorbeeld
title: Voorbeeld van voorbeeldstatus (Profile Preview) API-eindpunt
description: Het eindpunt van de voorproefvoorbeeldstatus van het Real-time Profiel van de Klant API staat u toe om de recentste succesvolle steekproef van uw gegevens van het Profiel, de distributie van het lijstprofiel door dataset en door identiteit, voor te vertonen en rapporten te produceren die datasetoverlapping, identiteitsoverlap, en ongestipte profielen tonen.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 8a17648757b342bd8026382918ca41c469210b51
workflow-type: tm+mt
source-wordcount: '2870'
ht-degree: 0%

---

# Voorvertoning voorbeeldstatuseindpunt (voorvertoning profiel)

Met Adobe Experience Platform kunt u klantgegevens uit meerdere bronnen invoeren om een robuust, uniform profiel voor elk van uw individuele klanten te maken. Aangezien de gegevens in Platform worden opgenomen, wordt een steekproefbaan in werking gesteld om de profieltelling en andere gegevens-verwante metriek van het Profiel van de Klant in real time bij te werken.

De resultaten van deze voorbeeldtaak kunnen worden weergegeven met de opdracht `/previewsamplestatus` eindpunt, deel van Real-time het Profiel van de Klant API. Dit eindpunt kan ook worden gebruikt om van profieldistributies door zowel dataset als identiteit namespace een lijst te maken, evenals veelvoudige rapporten te produceren om zicht in de samenstelling van de Opslag van het Profiel van uw organisatie te bereiken. Deze gids doorloopt de stappen die worden vereist om deze metriek te bekijken gebruikend `/previewsamplestatus` API-eindpunt.

>[!NOTE]
>
>Er zijn schatting en voorproef eindpunten beschikbaar als deel van de Dienst API van de Segmentatie van Adobe Experience Platform die u toestaan om samenvatting-vlakke informatie betreffende segmentdefinities te bekijken helpen ervoor zorgen u het verwachte publiek isoleert. Ga naar de [handleiding voor voorvertoningen en schattingen van eindpunten](../../segmentation/api/previews-and-estimates.md), een deel van de [!DNL Segmentation] API-ontwikkelaarsgids.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Profielfragmenten versus samengevoegde profielen

Deze handleiding verwijst naar zowel &quot;profielfragmenten&quot; als &quot;samengevoegde profielen&quot;. Het is belangrijk dat u het verschil tussen deze termen begrijpt voordat u verdergaat.

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, heeft uw organisatie waarschijnlijk veelvoudige profielfragmenten met betrekking tot die enige klant die in veelvoudige datasets verschijnt.

Wanneer profielfragmenten in Platform worden opgenomen, worden ze samengevoegd (op basis van een samenvoegbeleid) om één profiel voor die klant te maken. Daarom is het totale aantal profielfragmenten waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel uit veelvoudige fragmenten bestaat.

Als u meer wilt weten over profielen en hun rol in het Experience Platform, leest u eerst de [Overzicht van het realtime klantprofiel](../home.md).

## Hoe de voorbeeldtaak wordt geactiveerd

Als gegevens die voor het Profiel van de Klant in real time worden toegelaten worden opgenomen in [!DNL Platform], wordt het opgeslagen in de de gegevensopslag van het Profiel. Wanneer de opname van records in de profielwinkel het totale aantal profielen met meer dan 5% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. De wijze waarop het monster wordt geactiveerd, hangt af van het type inname dat wordt gebruikt:

* Voor **workflows voor streaming gegevens**, wordt per uur gecontroleerd of de verhoging of verlaging van 5% is bereikt. Als dit het geval is, wordt er automatisch een voorbeeldtaak geactiveerd om de telling bij te werken.
* Voor **batch-opname** Als aan de drempel van 5% voor verhogen of verlagen is voldaan, wordt binnen 15 minuten nadat een batch is ingevoerd in de profielopslag een taak uitgevoerd om het aantal bij te werken. Met behulp van de profiel-API kunt u een voorvertoning weergeven van de meest recente voorbeeldtaak en de distributie van het lijstprofiel via gegevensset en naamruimte op naam.

Het aantal profielen en de profielen op basis van naamruimtemetriek zijn ook beschikbaar in het dialoogvenster [!UICONTROL Profiles] van de gebruikersinterface van het Experience Platform. Ga voor informatie over hoe u toegang krijgt tot profielgegevens via de gebruikersinterface naar de [[!DNL Profile] UI-hulplijn](../ui/user-guide.md).

## Laatste voorbeeldstatus weergeven {#view-last-sample-status}

U kunt een verzoek van de GET tot uitvoeren `/previewsamplestatus` eindpunt om de details voor de laatste succesvolle steekproefbaan te bekijken die voor uw IMS Organisatie werd in werking gesteld. Dit omvat het totale aantal profielen in de steekproef, evenals de metrische profieltelling, of het totale aantal profielen uw organisatie binnen Experience Platform heeft.

Het aantal profielen wordt gegenereerd na het samenvoegen van profielfragmenten om één profiel voor elke afzonderlijke klant te vormen. Met andere woorden, wanneer profielfragmenten samen worden samengevoegd, wordt een getal van &quot;1&quot;-profiel geretourneerd omdat ze allemaal verwant zijn aan hetzelfde individu.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat de details voor de laatste geslaagde voorbeeldtaak die voor de organisatie is uitgevoerd.

>[!NOTE]
>
>In dit voorbeeldantwoord: `numRowsToRead` en `totalRows` zijn gelijk aan elkaar. Afhankelijk van het aantal profielen dat uw organisatie in Experience Platform heeft, kan dit het geval zijn. Over het algemeen verschillen deze twee getallen echter `numRowsToRead` het laagste getal is omdat het de steekproef vertegenwoordigt als een subset van het totale aantal profielen (`totalRows`).

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
| `sampleJobRunning` | Een Booleaanse waarde die wordt geretourneerd `true` wanneer een voorbeeldtaak wordt uitgevoerd. Biedt transparantie in de latentie die optreedt wanneer een batchbestand wordt geüpload naar het moment dat het daadwerkelijk wordt toegevoegd aan de profielopslag. |
| `cosmosDocCount` | Het totale aantal documenten in Cosmos. |
| `totalFragmentCount` | Het totale aantal profielfragmenten in het profielarchief. |
| `lastSuccessfulBatchTimestamp` | Laatste succesvolle tijdstempel voor batch-opname. |
| `streamingDriven` | *Dit veld is afgekeurd en heeft geen betekenis voor de reactie.* |
| `totalRows` | Het totale aantal samengevoegde profielen in Experience Platform, ook wel &#39;profieltelling&#39; genoemd. |
| `lastBatchId` | Laatste batch-opname-id. |
| `status` | Status van laatste sample. |
| `samplingRatio` | Verhouding van gesamplede profielen (`numRowsToRead`) naar totaal samengevoegde profielen (`totalRows`), uitgedrukt als een percentage in decimale notatie. |
| `mergeStrategy` | Samenvoegingsstrategie gebruikt in de steekproef. |
| `lastSampledTimestamp` | Laatste succesvolle voorbeeld van tijdstempel. |

## Profieldistributie per gegevensset weergeven

Om de verdeling van profielen door dataset te zien, kunt u een verzoek van de GET aan `/previewsamplestatus/report/dataset` eindpunt.

**API-indeling**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt het `date` parameter om het meest recente rapport voor de gespecificeerde datum terug te keren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie omvat een `data` array, die een lijst met gegevenssetobjecten bevat. De getoonde reactie is beknot om drie datasets te tonen.

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
| `samplePercentage` | De `sampleCount` als percentage van het totale aantal gesamplede samengevoegde profielen (de `numRowsToRead` waarde die wordt geretourneerd in het dialoogvenster [status laatste sample](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen met deze dataset-id. |
| `fullIDsPercentage` | De `fullIDsCount` als percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde die wordt geretourneerd in het dialoogvenster [status laatste sample](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `name` | De naam van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `description` | De beschrijving van de dataset, zoals die tijdens de verwezenlijking van dataset wordt verstrekt. |
| `value` | De id van de gegevensset. |
| `streamingIngestionEnabled` | Of de dataset voor het stromen opname wordt toegelaten. |
| `createdUser` | De gebruikers-id van de gebruiker die de gegevensset heeft gemaakt. |
| `reportTimestamp` | De tijdstempel van het rapport. Indien een `date` parameter werd verstrekt tijdens het verzoek, is het teruggekeerde rapport voor de verstrekte datum. Indien niet `date` parameter wordt verstrekt, is het meest recente rapport teruggekeerd. |

## Profieldistributie weergeven op naamruimte van identiteit

U kunt een verzoek van de GET tot uitvoeren `/previewsamplestatus/report/namespace` eindpunt om de uitsplitsing naar naamruimte van de identiteit in alle samengevoegde profielen in uw profielarchief weer te geven. Dit omvat zowel de standaardidentiteiten die door Adobe worden verstrekt, als de douaneidentiteiten die door uw organisatie worden bepaald.

Identiteitsnaamruimten zijn een belangrijk onderdeel van de Adobe Experience Platform Identity Service dat als indicatoren dient voor de context waarop de klantgegevens betrekking hebben. Om meer te leren, begin door te lezen [Overzicht van naamruimte in identiteit](../../identity-service/namespaces.md).

>[!NOTE]
>
>Het totale aantal profielen per naamruimte (door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan de metrische waarde van het aantal profielen, omdat één profiel aan meerdere naamruimten kan worden gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

**API-indeling**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt geen `date` en zal daarom het meest recente verslag teruggeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie omvat een `data` array, met afzonderlijke objecten die de details voor elke naamruimte bevatten. De getoonde reactie is afgebroken om vier naamruimten te tonen.

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
| `samplePercentage` | De `sampleCount` als percentage van gesamplede samengevoegde profielen (de `numRowsToRead` waarde die wordt geretourneerd in het dialoogvenster [status laatste sample](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `reportTimestamp` | De tijdstempel van het rapport. Indien een `date` parameter werd verstrekt tijdens het verzoek, is het teruggekeerde rapport voor de verstrekte datum. Indien niet `date` parameter wordt verstrekt, is het meest recente rapport teruggekeerd. |
| `fullIDsFragmentCount` | Het totale aantal profielfragmenten in de naamruimte. |
| `fullIDsCount` | Het totale aantal samengevoegde profielen in de naamruimte. |
| `fullIDsPercentage` | De `fullIDsCount` als percentage van het totale aantal samengevoegde profielen (de `totalRows` waarde die wordt geretourneerd in het dialoogvenster [status laatste sample](#view-last-sample-status)), uitgedrukt in decimale notatie. |
| `code` | De `code` voor de naamruimte. Dit is te vinden wanneer u met naamruimten werkt met de opdracht [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) en wordt ook aangeduid als de [!UICONTROL Identity symbol] in de gebruikersinterface van het Experience Platform. Ga voor meer informatie naar de [Overzicht van naamruimte in identiteit](../../identity-service/namespaces.md). |
| `value` | De `id` waarde voor de naamruimte. Dit is te vinden wanneer u met naamruimten werkt met de opdracht [Identiteitsservice-API](../../identity-service/api/list-namespaces.md). |

## Genereer het overlappingsrapport voor de gegevensset

Het rapport van de overlapping van datasets verstrekt zicht in de samenstelling van de Opslag van het Profiel van uw organisatie door de datasets bloot te stellen die het meest aan uw adresseerbare publiek (samengevoegde profielen) bijdragen. Naast het verstrekken van inzichten in uw gegevens, kan dit rapport u acties helpen om vergunningsgebruik te optimaliseren, zoals het plaatsen van TTL voor bepaalde datasets.

U kunt het rapport van de datasetoverlapping produceren door een verzoek van de GET aan te voeren `/previewsamplestatus/report/dataset/overlap` eindpunt.

Voor geleidelijke instructies die hoe te om het rapport van de datasetoverlapping te produceren gebruikend de bevellijn of Postman UI schetsen, gelieve te verwijzen naar [het produceren van de datasetoverlapping rapportleerprogramma](../tutorials/dataset-overlap-report.md).

**API-indeling**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als meerdere rapporten op dezelfde datum zijn uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt het `date` parameter om het meest recente rapport voor de gespecificeerde datum terug te keren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwoord**

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
| `data` | De `data` Het object bevat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke profielaantallen. |
| `reportTimestamp` | De tijdstempel van het rapport. Indien een `date` parameter werd verstrekt tijdens het verzoek, is het teruggekeerde rapport voor de verstrekte datum. Indien niet `date` parameter wordt verstrekt, is het meest recente rapport teruggekeerd. |

### Het rapport van de gegevensset-overlapping interpreteren

De resultaten van het rapport kunnen van de datasets en profieltellingen in de reactie worden geïnterpreteerd. Overweeg het volgende voorbeeldrapport `data` object:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dit rapport bevat de volgende informatie:

* Er zijn 123 profielen die van gegevens uit de volgende datasets worden samengesteld: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Er zijn 454.412 profielen samengesteld uit gegevens die uit deze twee datasets komen: `5d92921872831c163452edc8` en `5eb2cdc6fa3f9a18a7592a98`.
* Er zijn 107 profielen die slechts van gegevens van dataset worden samengesteld `5eeda0032af7bb19162172a7`.
* Er zijn in totaal 454.642 profielen in de organisatie.

## Rapport voor overlappende naamruimte genereren

De identiteitsnaamruimte overlapt rapport geeft inzicht in de samenstelling van de profielopslag van uw organisatie door de naamruimten die het meest bijdragen aan uw adresseerbare publiek (samengevoegde profielen) toegankelijk te maken. Dit omvat zowel de standaardnaamruimten die door Adobe worden verstrekt, als de naamruimten van de douaneidentiteit die door uw organisatie worden bepaald.

U kunt het overlappende rapport voor naamruimte genereren door een verzoek van de GET naar de `/previewsamplestatus/report/namespace/overlap` eindpunt.

**API-indeling**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als meerdere rapporten op dezelfde datum zijn uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Als een rapport niet bestaat voor de opgegeven datum, wordt een fout 404 (Niet gevonden) geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Verzoek**

In het volgende verzoek wordt het `date` parameter om het meest recente rapport voor de gespecificeerde datum terug te keren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwoord**

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
| `data` | De `data` Het object bevat door komma&#39;s gescheiden lijsten met unieke combinaties van naamruimtecodes en hun respectievelijke profielaantallen. |
| Namespace-codes | De `code` is een kort formulier voor elke naamruimtenaam van een identiteit. Een afbeelding van elk `code` het `name` kan worden gevonden met de [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md). De `code` wordt ook aangeduid als de [!UICONTROL Identity symbol] in de gebruikersinterface van het Experience Platform. Ga voor meer informatie naar de [Overzicht van naamruimte in identiteit](../../identity-service/namespaces.md). |
| `reportTimestamp` | De tijdstempel van het rapport. Indien een `date` parameter werd verstrekt tijdens het verzoek, is het teruggekeerde rapport voor de verstrekte datum. Indien niet `date` parameter wordt verstrekt, is het meest recente rapport teruggekeerd. |

### Rapport voor overlappende naamruimte interpreteren

De resultaten van het rapport kunnen van de identiteiten en profieltellingen in de reactie worden geïnterpreteerd. De numerieke waarde van elke rij vertelt u hoeveel profielen uit die nauwkeurige combinatie standaard en douaneidentiteitsnamespaces bestaan.

Neem het volgende fragment uit het `data` object:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Dit rapport bevat de volgende informatie:

* Er zijn 142 profielen die bestaan uit `AAID`, `ECID`, en `Email` standaardidentiteiten en van een douane `crmid` naamruimte identiteit.
* Er zijn 24 profielen die bestaan uit `AAID` en `ECID` naamruimten.
* Er zijn 6.565 profielen die slechts een `ECID` identiteit.

## Rapport voor niet-geselecteerde profielen genereren

U kunt de samenstelling van de Opslag van het Profiel van uw organisatie door het niet-gesloten profielrapport meer zichtbaar worden. Een &quot;niet-gekoppeld&quot; profiel is een profiel dat slechts één profielfragment bevat. Een &quot;onbekend&quot; profiel is een profiel dat is gekoppeld aan pseudoniem naamruimten, zoals `ECID` en `AAID`. Onbekende profielen zijn inactief, wat betekent dat er geen nieuwe gebeurtenissen zijn toegevoegd voor de opgegeven periode. Het rapport met niet-opgeslagen profielen bevat een indeling van profielen voor een periode van 7, 30, 60, 90 en 120 dagen.

U kunt het rapport met niet-gekoppelde profielen genereren door een verzoek tot GET aan de `/previewsamplestatus/report/unstitchedProfiles` eindpunt.

**API-indeling**

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

**Antwoord**

Een succesvolle aanvraag retourneert HTTP Status 200 (OK) en het rapport met niet-opgeslagen profielen.

>[!NOTE]
>
>Voor de toepassing van deze handleiding is het verslag ingekort en omvat het alleen `"120days"` en &quot;`7days`&quot;tijdsperiodes. Het volledige rapport met ongeordende profielen bevat een uitsplitsing van profielen voor een periode van 7, 30, 60, 90 en 120 dagen.

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
| `data` | De `data` bevat de informatie die wordt geretourneerd voor het rapport met niet-ingestelde profielen. |
| `totalNumberOfProfiles` | Het totale aantal unieke profielen in het profielarchief. Dit is gelijk aan het adresseerbare aantal. Het bevat zowel bekende als niet-gebonden profielen. |
| `totalNumberOfEvents` | The total number of ExperienceEvents in the Profile Store. |
| `unstitchedProfiles` | Een object met een uitsplitsing van niet-ingestelde profielen naar tijdsperiode. Het rapport met niet-opgeslagen profielen bevat een uitsplitsing van profielen voor tijdvakken van 7, 30, 60, 90 en 120 dagen. |
| `countOfProfiles` | Het aantal niet-gekoppelde profielen voor de tijdsperiode of het aantal niet-gebonden profielen voor de naamruimte. |
| `eventsAssociated` | Het aantal ExperienceEvents voor het tijdbereik of het aantal gebeurtenissen voor de naamruimte. |
| `nsDistribution` | Een object dat afzonderlijke naamruimten bevat met de distributie van niet-gekoppelde profielen en gebeurtenissen voor elke naamruimte. Opmerking: Het totaal optellen `countOfProfiles` voor elke naamruimte van de identiteit in het dialoogvenster `nsDistribution` object is gelijk aan `countOfProfiles` voor de periode. Hetzelfde geldt voor `eventsAssociated` per naamruimte en het totaal `eventsAssociated` per tijdsperiode. |
| `reportTimestamp` | De tijdstempel van het rapport. |

### Het rapport met niet-opgeslagen profielen interpreteren

De resultaten van het rapport kunnen inzicht geven in hoeveel ongeordende en inactieve profielen uw organisatie binnen haar Opslag van het Profiel heeft.

Neem het volgende fragment uit het `data` object:

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

Nu u weet hoe te om steekproefgegevens in de Opslag van het Profiel voor te vertonen en veelvoudige rapporten over de gegevens in werking te stellen, kunt u de schatting en voorproef eindpunten van de Dienst API van de Segmentatie ook gebruiken om summiere-vlakke informatie betreffende uw segmentdefinities te bekijken. Deze informatie helpt om ervoor te zorgen u het verwachte publiek in uw segment isoleert. Ga voor meer informatie over het werken met segmentvoorvertoningen en -schattingen met de segmentatie-API naar de [eindpuntgids voor voorvertoningen en schattingen](../../segmentation/api/previews-and-estimates.md).

