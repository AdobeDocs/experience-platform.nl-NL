---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht batchverwerking Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Overzicht van inname in batch

Met de API voor inname van batch kunt u gegevens als batchbestanden in het Adobe Experience Platform opnemen. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een parquetdossier), of gegevens zijn die aan een bekend schema in het register van het Model van de Gegevens van de Ervaring (XDM) in overeenstemming zijn.

De verwijzing naar [de API voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) gegevensverwerking biedt aanvullende informatie over deze API-aanroepen.

Het volgende diagram schetst het proces van partijingestie:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## De API gebruiken

Met de API voor gegevensinname kunt u gegevens als batches (een gegevenseenheid die bestaat uit een of meer bestanden die als één eenheid moeten worden opgenomen) in het Experience Platform innemen in drie basisstappen:

1. Maak een nieuwe batch.
2. Upload dossiers aan een gespecificeerde dataset die het XDM schema van de gegevens aanpast.
3. Geef het einde van de batch aan.


### Voorwaarden voor gegevensinname

- De gegevens die moeten worden geüpload, moeten de indeling Parquet of JSON hebben.
- Een dataset die in de diensten [van de](../../catalog/home.md)Catalogus wordt gecreeerd.
- De inhoud van het ouderdossier moet een ondergroep van het schema van de dataset aanpassen die in wordt geupload.
- Heb uw uniek Token van de Toegang na authentificatie.

### Aanbevolen werkwijzen bij inname in batch

- De aanbevolen batch is tussen 256 MB en 100 GB.
- Elke batch moet maximaal 1500 bestanden bevatten.

Als u een bestand wilt uploaden dat groter is dan 512 MB, moet het bestand in kleinere delen worden verdeeld. Instructies voor het uploaden van een groot bestand vindt u [hier](#large-file-upload---create-file).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Een batch maken

Voordat gegevens kunnen worden toegevoegd aan een gegevensset, moet deze worden gekoppeld aan een batch, die later wordt geüpload naar een opgegeven gegevensset.

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `datasetId` | De id van de gegevensset waarin de bestanden moeten worden geüpload. |

**Reactie**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de batch die zojuist is gemaakt (wordt gebruikt in volgende aanvragen). |
| `relatedObjects.id` | De id van de gegevensset waarin de bestanden moeten worden geüpload. |

## Bestand uploaden

Nadat een nieuwe batch is gemaakt om te uploaden, kunnen bestanden vervolgens naar een specifieke gegevensset worden geüpload.

U kunt bestanden uploaden met de **Small File Upload API**. Als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden (zoals uitgebreide time-outs, overschrijdingen van aanvragen voor een grotere bestandsgrootte en andere beperkingen), kunt u overschakelen naar de API **voor** grote bestanden uploaden. Deze API uploadt het bestand in delen en koppelt gegevens aan elkaar met behulp van de volledige API **-aanroep voor** groot bestand uploaden.

>[!NOTE] In de onderstaande voorbeelden wordt de [bestandsindeling Parquet](https://parquet.apache.org/documentation/latest/) gebruikt. Een voorbeeld dat de JSON-bestandsindeling gebruikt, vindt u in de ontwikkelaarshandleiding voor [batchinvoer](./api-overview.md).

### Kleine bestandsupload

Zodra een partij wordt gecreeerd, kunnen de gegevens aan een preexisting dataset worden geupload.  Het bestand dat wordt geüpload, moet overeenkomen met het XDM-schema waarnaar wordt verwezen.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch. |
| `{DATASET_ID}` | De id van de dataset om bestanden te uploaden. |
| `{FILE_NAME}` | De naam van het bestand zoals dit wordt weergegeven in de gegevensset. |

**Verzoek**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het pad en de bestandsnaam van het bestand dat in de gegevensset moet worden geüpload. |

**Reactie**

```JSON
#Status 200 OK, with empty response body
```

### Grote bestandsupload - bestand maken

Als u een groot bestand wilt uploaden, moet het bestand in kleinere delen worden gesplitst en één voor één worden geüpload.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch. |
| `{DATASET_ID}` | Identiteitskaart van de dataset die de dossiers opneemt. |
| `{FILE_NAME}` | De naam van het bestand zoals dit wordt weergegeven in de gegevensset. |

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie**

```JSON
#Status 201 CREATED, with empty response body
```

### Grote bestandsupload - volgende onderdelen uploaden

Nadat het bestand is gemaakt, kunnen alle volgende hoofdstukken worden geüpload door herhaalde PATCH-aanvragen te maken, één voor elke sectie van het bestand.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch. |
| `{DATASET_ID}` | De id van de gegevensset waarin de bestanden moeten worden geüpload. |
| `{FILE_NAME}` | Naam van dossier aangezien het in de dataset zal worden gezien. |

**Verzoek**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het pad en de bestandsnaam van het bestand dat in de gegevensset moet worden geüpload. |

**Reactie**

```JSON
#Status 200 OK, with empty response
```

## Signaalbatchverwerking

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Op deze manier worden de Catalog **DataSetFile** -items gemaakt voor de voltooide bestanden en gekoppeld aan de hierboven gegenereerde batch. De catalogusbatch wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

**Verzoek**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die in de gegevensset moet worden geüpload. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Reactie**

```JSON
#Status 200 OK, with empty response
```

## Batchstatus controleren

Wanneer u wacht tot de bestanden naar de batch zijn geüpload, kunt u de status van de batch controleren om de voortgang te zien.

**API-indeling**

```http
GET /batch/{BATCH_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die wordt gecontroleerd. |

**Verzoek**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt of bijgewerkt. |

In dit `"status"` veld wordt de huidige status van de aangevraagde batch weergegeven. De batches kunnen een van de volgende statussen hebben:

## Statistieken van inname in batch

| Status | Beschrijving |
| ------ | ----------- |
| Verlaten | De batch is niet binnen de verwachte tijd voltooid. |
| Afgebroken | Er is **expliciet** een afbreekbewerking aangeroepen (via de Batch Ingest-API) voor de opgegeven batch. Als de batch eenmaal is **geladen** , kan deze niet worden afgebroken. |
| Actief | De partij is met succes bevorderd en is beschikbaar voor downstreamconsumptie. Deze status kan onderling verwisselbaar met **Succes** worden gebruikt. |
| Verwijderd | De gegevens voor de batch zijn volledig verwijderd. |
| Mislukt | Een eindstaat die uit of slechte configuratie en/of slechte gegevens voortvloeit. Gegevens voor een mislukte batch worden **niet** weergegeven. Deze status kan onderling verwisselbaar met **Mislukking** worden gebruikt. |
| Inactief | De batch is gepromoveerd, maar is teruggezet of verlopen. De partij is niet meer beschikbaar voor downstreamconsumptie. |
| Geladen | De gegevens voor de partij zijn volledig en de partij is klaar voor bevordering. |
| Laden | De gegevens voor deze batch worden geüpload en de batch is momenteel **niet** klaar om te worden gepromoveerd. |
| Opnieuw proberen | De gegevens voor deze batch worden verwerkt. Vanwege een systeem- of overgangsfout is de batch echter mislukt. Hierdoor wordt deze batch opnieuw geprobeerd. |
| Staand | De testfase van het promotieproces voor een batch is voltooid en de innametaak is uitgevoerd. |
| Staging | De gegevens voor de partij worden verwerkt. |
| Gestopt | De gegevens voor de batch worden verwerkt. De batchbevordering is echter vastgelopen na een aantal pogingen. |