---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: API-eindpunt voor systeemtaken profiel
type: Documentation
description: Met Adobe Experience Platform kunt u een gegevensset of batch verwijderen uit de profielopslag om gegevens van het realtime-klantprofiel te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de profiel-API gebruiken om een profielsysteemtaak te maken of een aanvraag te verwijderen.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# Het taakeindpunt van het profielsysteem (verzoeken schrappen)

>[!IMPORTANT]
>
>De volgende eindpunten kunnen verschillen tussen implementaties van Adobe Experience Platform die worden uitgevoerd op Microsoft Azure en Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](https://experienceleague.adobe.com/nl/docs/experience-platform/landing/multi-cloud).

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen invoeren en robuuste profielen voor individuele klanten maken. Gegevens die in [!DNL Experience Platform] worden ingevoerd, worden opgeslagen in [!DNL Data Lake] en als de gegevenssets zijn ingeschakeld voor Profiel, worden die gegevens ook opgeslagen in de [!DNL Real-Time Customer Profile] -gegevensopslag. Soms kan het nodig zijn om profielgegevens die zijn gekoppeld aan een gegevensset te verwijderen uit de profielenopslag om gegevens te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de API van [!DNL Real-Time Customer Profile] gebruiken om een [!DNL Profile] -systeemtaak te maken, of &quot;aanvraag verwijderen&quot;.

>[!NOTE]
>
>Als u probeert om datasets of partijen van [!DNL Data Lake] te schrappen, gelieve het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md) voor meer informatie te bezoeken.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt is een deel van [[!DNL Real-Time Customer Profile API] ](https://www.adobe.com/go/profile-apis-en). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

## Verzoeken om verwijderen weergeven {#view}

Een verwijderingsverzoek is een langdurig, asynchroon proces, wat betekent dat uw organisatie mogelijk meerdere verwijderingsverzoeken tegelijk uitvoert. Als u alle verwijderingsaanvragen wilt weergeven die uw organisatie momenteel uitvoert, kunt u een GET-aanvraag naar het `/system/jobs` -eindpunt uitvoeren.

U kunt facultatieve vraagparameters ook gebruiken om de lijst van schrappingsverzoeken te filtreren die in de reactie zijn teruggekeerd. Als u meerdere parameters wilt gebruiken, scheidt u elke parameter met een en-teken (`&`).

**API formaat**

>[!AVAILABILITY]
>
>De volgende vraagparameters zijn **slechts** beschikbaar wanneer het gebruiken van Experience Platform op Microsoft Azure.
>
>Wanneer het gebruiken van dit eindpunt op AWS, zijn de eerste 100 systeembanen teruggekeerd in dalende orde, die op hun aanmaakdatum wordt gebaseerd.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `start` | Verschuif de pagina met geretourneerde resultaten volgens de aanmaaktijd van de aanvraag. | `start=4` |
| `limit` | Beperk het aantal geretourneerde resultaten. | `limit=10` |
| `page` | Retourneer een specifieke pagina met resultaten volgens de aanmaaktijd van de aanvraag. | `page=2` |
| `sort` | De resultaten van de soort door een specifiek gebied in het stijgen (`asc`) of dalende (`desc`) orde. De sorteerparameter werkt niet bij het retourneren van meerdere pagina&#39;s met resultaten. | `sort=batchId:asc` |

**Verzoek**

>[!IMPORTANT]
>
>Het volgende verzoek verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

+++ Een voorbeeldverzoek om de systeemtaken te bekijken.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB  Amazon Web Services (AWS) ]

>[!IMPORTANT]
>
>U **moet** de `x-sandbox-id` verzoekkopbal in plaats van de `x-sandbox-name` verzoekkopbal gebruiken wanneer het gebruiken van dit eindpunt met AWS.

+++ Een voorbeeldverzoek om de systeemtaken te bekijken.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Reactie**

>[!IMPORTANT]
>
>De volgende reactie verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

Een geslaagde reactie bevat een array &#39;children&#39; met een object voor elke verwijderaanvraag die de details van die aanvraag bevat.

+++ Een geslaagde reactie voor het bekijken van de verwijderaanvragen

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `_page.count` | Het totale aantal aanvragen. Deze reactie is afgebroken voor de ruimte. |
| `_page.next` | Als een extra pagina van resultaten bestaat, bekijk de volgende pagina van resultaten door de waarde van identiteitskaart in a [ raadplegingsverzoek ](#view-a-specific-delete-request) met de `"next"` verstrekte waarde te vervangen. |
| `jobType` | Het type taak dat wordt gemaakt. In dit geval wordt altijd `"DELETE"` geretourneerd. |
| `status` | De status van de verwijderaanvraag. Mogelijke waarden zijn `"NEW"` , `"PROCESSING"` , `"COMPLETED"` en `"ERROR"` . |
| `metrics` | Een voorwerp dat het aantal verslagen omvat die zijn verwerkt (`"recordsProcessed"`) en de tijd in seconden dat het verzoek is verwerkt, of hoe lang het verzoek om (`"timeTakenInSec"`) nam te voltooien. |

+++

>[!TAB  Amazon Web Services (AWS) ]

Een geslaagde reactie retourneert een array met een object voor elk van de systeemaanvragen.

+++ Een succesvol antwoord op de systeemaanvragen

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `requestId` | De id van de systeemtaak. |
| `requestType` | Het type systeemtaak. Mogelijke waarden zijn `BACKFILL_TTL` , `DELETE_EE_BATCH` en `TRUNCATE_DATASET` . |
| `status` | De status van de systeemtaak. Mogelijke waarden zijn `NEW` , `SUCCESS` , `ERROR` , `FAILED` en `IN-PROGRESS` . |
| `properties` | Een voorwerp dat partij en/of dataset IDs van de systeembaan bevat. |

+++

>[!ENDTABS]

## Een verwijderaanvraag maken {#create-a-delete-request}

Het in werking stellen van een nieuw schrappingsverzoek wordt gedaan door een POST- verzoek aan het `/systems/jobs` eindpunt, waar identiteitskaart van de te schrappen dataset of partij in het lichaam van het verzoek wordt verstrekt.

### Een gegevensset en de bijbehorende profielgegevens verwijderen

Om een dataset en alle profielgegevens verbonden aan de dataset van de opslag van het Profiel te schrappen, moet dataset identiteitskaart in het lichaam van het POST- verzoek worden omvat. Deze actie zal ALLE gegevens voor een bepaalde dataset schrappen. [!DNL Experience Platform] staat u toe om datasets te schrappen die op zowel verslag als tijdreeksschema&#39;s worden gebaseerd.

**API formaat**

```http
POST /system/jobs
```

**Verzoek**

>[!IMPORTANT]
>
>Het volgende verzoek verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

+++ Een steekproefverzoek om een dataset te schrappen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `dataSetId` | De id van de gegevensset die u wilt verwijderen. |

>[!TAB  Amazon Web Services (AWS) ]

>[!IMPORTANT]
>
>U **moet** de `x-sandbox-id` verzoekkopbal in plaats van de `x-sandbox-name` verzoekkopbal gebruiken wanneer het gebruiken van dit eindpunt met AWS.

+++ Een steekproefverzoek om een dataset te schrappen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `dataSetId` | De id van de gegevensset die u wilt verwijderen. |

>[!ENDTABS]

**Reactie**

>[!IMPORTANT]
>
>De volgende reactie verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `status` voor de aanvraag op het moment dat deze wordt gemaakt, is `"NEW"` totdat deze wordt verwerkt. De `dataSetId` in de reactie moet overeenkomen met de `dataSetId` die in de aanvraag wordt verzonden.

+++ Een geslaagde reactie voor het maken van een verwijderaanvraag.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| `dataSetId` | De id van de gegevensset, zoals opgegeven in het POST-verzoek. |

+++

>[!TAB  Amazon Web Services (AWS) ]

Een succesvolle reactie keert de details van het onlangs gecreeerde systeemverzoek terug.

+++ Een geslaagde reactie voor het maken van een verwijderaanvraag.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `requestId` | De id van de systeemtaak. |
| `requestType` | Het type systeemtaak. Mogelijke waarden zijn `BACKFILL_TTL` , `DELETE_EE_BATCH` en `TRUNCATE_DATASET` . |
| `status` | De status van de systeemtaak. Mogelijke waarden zijn `NEW` , `SUCCESS` , `ERROR` , `FAILED` en `IN-PROGRESS` . |
| `properties` | Een voorwerp dat partij en/of dataset IDs van de systeembaan bevat. |

+++

>[!ENDTABS]

### Een batch verwijderen

Om een partij te kunnen verwijderen, moet de partij-ID worden opgenomen in de hoofdtekst van de POST-aanvraag. Gelieve te worden geadviseerd dat u geen partijen voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd. Alleen batches voor gegevenssets op basis van tijdreeksschema&#39;s mogen worden verwijderd.

>[!NOTE]
>
> De reden u niet batches voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd is omdat de reeksen van de recordtype dataset vorige verslagen beschrijven en daarom niet &quot;undone&quot;of geschrapt kunnen zijn. De enige manier om het effect van onjuiste partijen voor datasets te verwijderen die op verslagschema&#39;s worden gebaseerd is de partij met de correcte gegevens opnieuw op te nemen om de onjuiste verslagen te beschrijven.

Voor meer informatie over verslag en tijdreeksgedrag, te herzien gelieve de [ sectie over XDM gegevensgedrag ](../../xdm/home.md#data-behaviors) in het [!DNL XDM System] overzicht.

**API formaat**

```http
POST /system/jobs
```

**Verzoek**

>[!IMPORTANT]
>
>Het volgende verzoek verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

+++ Een voorbeeldaanvraag om een batch te verwijderen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `datasetId` | De id van de gegevensset voor de batch die u wilt verwijderen. |
| `batchId` | De id van de batch die u wilt verwijderen. |

>[!TAB  Amazon Web Services (AWS) ]

>[!IMPORTANT]
>
>U **moet** de `x-sandbox-id` verzoekkopbal in plaats van de `x-sandbox-name` verzoekkopbal gebruiken wanneer het gebruiken van dit eindpunt met AWS.

+++ Een voorbeeldaanvraag om een batch te verwijderen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `datasetId` | De id van de gegevensset voor de batch die u wilt verwijderen. |
| `batchId` | De id van de batch die u wilt verwijderen. |

>[!ENDTABS]

**Reactie**

>[!IMPORTANT]
>
>De volgende reactie verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `"status"` voor de aanvraag op het moment dat deze wordt gemaakt, is `"NEW"` totdat deze wordt verwerkt. De `"batchId"` -waarde in het antwoord moet overeenkomen met de `"batchId"` -waarde die in de aanvraag wordt verzonden.

+++ Een geslaagde reactie voor het maken van een verwijderaanvraag.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| `datasetId` | De id van de opgegeven gegevensset. |
| `batchId` | De id van de batch, zoals opgegeven in de POST-aanvraag. |

+++

>[!TAB  Amazon Web Services (AWS) ]

Een succesvolle reactie keert de details van het onlangs gecreeerde systeemverzoek terug.

+++ Een geslaagde reactie voor het maken van een verwijderaanvraag.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `requestId` | De id van de systeemtaak. |
| `requestType` | Het type systeemtaak. Mogelijke waarden zijn `BACKFILL_TTL` , `DELETE_EE_BATCH` en `TRUNCATE_DATASET` . |
| `status` | De status van de systeemtaak. Mogelijke waarden zijn `NEW` , `SUCCESS` , `ERROR` , `FAILED` en `IN-PROGRESS` . |
| `properties` | Een voorwerp dat partij en/of dataset IDs van de systeembaan bevat. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>De volgende eigenschap is **slechts** beschikbaar wanneer het gebruiken van Experience Platform op Microsoft Azure.

Als u probeert om een schrappingsverzoek voor een partij van de dataset van het Verslag in werking te stellen, zult u een fout op 400 niveau ontmoeten, gelijkend op het volgende:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Een specifiek verwijderingsverzoek weergeven {#view-a-specific-delete-request}

Als u een specifieke verwijderingsaanvraag wilt weergeven, inclusief details zoals de status, kunt u een opzoekaanvraag (GET) uitvoeren naar het `/system/jobs` -eindpunt en de id van de verwijderingsaanvraag opnemen in het pad.

**API formaat**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | De id van de verwijderaanvraag die u wilt bekijken. |

**Verzoek**

>[!IMPORTANT]
>
>Het volgende verzoek verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

+++ Een voorbeeldverzoek om een profieltaak weer te geven.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB  Amazon Web Services (AWS) ]

>[!IMPORTANT]
>
>U **moet** de `x-sandbox-id` verzoekkopbal in plaats van de `x-sandbox-name` verzoekkopbal gebruiken wanneer het gebruiken van dit eindpunt met AWS.

+++ Een voorbeeldverzoek om een profieltaak weer te geven.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Reactie**

>[!IMPORTANT]
>
>De volgende reactie verschilt tussen de Azure- en AWS-instanties.

>[!BEGINTABS]

>[!TAB  Microsoft Azure ]

In het antwoord worden de details van het verwijderingsverzoek weergegeven, inclusief de bijgewerkte status. De id van de verwijderaanvraag in de reactie (de `"id"` -waarde) moet overeenkomen met de id die in het aanvraagpad is verzonden.

+++ Een geslaagde reactie voor het weergeven van een verwijderingsaanvraag.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Properties | Beschrijving |
| ---------- | ----------- |
| `jobType` | Het type taak dat wordt gemaakt, in dit geval retourneert deze altijd `"DELETE"` . |
| `status` | De status van de verwijderaanvraag. Mogelijke waarden zijn `NEW` , `PROCESSING` , `COMPLETED` en `ERROR` . |
| `metrics` | Een serie die het aantal verslagen omvat die zijn verwerkt (`"recordsProcessed"`) en de tijd in seconden dat het verzoek verwerking is geweest, of hoe lang het verzoek om (`"timeTakenInSec"`) nam te voltooien. |

+++

>[!TAB  Amazon Web Services (AWS) ]

Een succesvolle reactie keert de details van het gespecificeerde systeemverzoek terug.

+++ Een geslaagde reactie voor het weergeven van een verwijderingsaanvraag.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `requestId` | De id van de systeemtaak. |
| `requestType` | Het type systeemtaak. Mogelijke waarden zijn `BACKFILL_TTL` , `DELETE_EE_BATCH` en `TRUNCATE_DATASET` . |
| `status` | De status van de systeemtaak. Mogelijke waarden zijn `NEW` , `SUCCESS` , `ERROR` , `FAILED` en `IN-PROGRESS` . |
| `properties` | Een voorwerp dat partij en/of dataset IDs van de systeembaan bevat. |

+++

>[!ENDTABS]

Als de status van de verwijderaanvraag is ingesteld op `"COMPLETED"` , kunt u bevestigen dat de gegevens zijn verwijderd door via de API voor gegevenstoegang toegang te krijgen tot de verwijderde gegevens. Voor instructies op hoe te om de Toegang API van Gegevens te gebruiken om tot datasets en partijen toegang te hebben, te herzien gelieve de [ documentatie van de Toegang van Gegevens ](../../data-access/home.md).

## Een verwijderingsaanvraag verwijderen

>[!AVAILABILITY]
>
>Dit eindpunt wordt **slechts** gesteund in de Azure instantie van Adobe Experience Platform, en wordt **niet** gesteund op de instantie van AWS.

Met [!DNL Experience Platform] kunt u een eerdere aanvraag verwijderen. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de verwijdertaak niet is voltooid of vastgelopen in het verwerkingsstadium. Als u een verwijderaanvraag wilt verwijderen, kunt u een DELETE-aanvraag naar het `/system/jobs` -eindpunt uitvoeren en de id van de verwijderaanvraag opnemen die u naar het aanvraagpad wilt verwijderen.

**API formaat**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | De id van de verwijderaanvraag die u wilt verwijderen. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. U kunt bevestigen dat de aanvraag is verwijderd door een GET-aanvraag uit te voeren om de aanvraag voor verwijderen met de id weer te geven. Dit zou een Status 404 van HTTP (niet Gevonden) moeten terugkeren, erop wijzend dat het schrappingsverzoek werd verwijderd.

## Volgende stappen

Nu u de stappen kent die nodig zijn om gegevenssets en batches te verwijderen uit [!DNL Profile store] within [!DNL Experience Platform] , kunt u veilig gegevens verwijderen die ten onrechte zijn toegevoegd of die uw organisatie niet meer nodig heeft. Houd er rekening mee dat een verwijderingsaanvraag niet ongedaan kan worden gemaakt. Verwijder daarom alleen gegevens die u zeker weet dat u deze nu niet nodig hebt en in de toekomst niet meer nodig hebt.
