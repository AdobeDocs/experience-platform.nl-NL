---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;inname;ontwikkelaarshandleiding;api-handleiding;upload;ingest Parquet;ingest json;
solution: Experience Platform
title: Handleiding voor de API voor batchverwerking
description: Dit document bevat een uitgebreide handleiding voor ontwikkelaars die werken met batch-opname-API's voor Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '2435'
ht-degree: 1%

---

# Handleiding voor het ontwikkelen van batterijen

Dit document verstrekt een uitvoerige gids aan het gebruiken van [&#x200B; partij ingestie API eindpunten &#x200B;](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) in Adobe Experience Platform. Voor een overzicht van partij ingestie APIs, met inbegrip van eerste vereisten en beste praktijken, gelieve te beginnen door het [&#x200B; partij ingestition API overzicht &#x200B;](overview.md) te lezen.

Het bijlage aan dit document verstrekt informatie voor [&#x200B; het formatteren gegevens die voor opname &#x200B;](#data-transformation-for-batch-ingestion), met inbegrip van steekproefCSV en JSON gegevensdossiers moeten worden gebruikt.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [&#x200B; de Ingestie API van de Partij &#x200B;](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). De opname van de partij wordt verstrekt door RESTful API waar u basisbewerkingen van CRUD tegen de gesteunde objecten types kunt uitvoeren.

Alvorens verder te gaan, te herzien gelieve het [&#x200B; partij ingestie API overzicht &#x200B;](overview.md) en [&#x200B; begonnen gids &#x200B;](getting-started.md) worden.

## Ingest JSON-bestanden

>[!NOTE]
>
>- De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, moet u op grote dossier schakelen uploadt.
>
>- Gebruik Single-line JSON in plaats van multi-line JSON als invoer voor batch-opname. Single-line JSON biedt betere prestaties omdat het systeem één invoerbestand in meerdere delen kan verdelen en parallel kan verwerken, terwijl JSON met meerdere regels niet kan worden gesplitst. Dit kan de kosten voor gegevensverwerking aanzienlijk verlagen en de latentie voor batchverwerking aanzienlijk verbeteren.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

>[!NOTE]
>
>De voorbeelden hieronder zijn voor single-line JSON. Als u JSON met meerdere regels wilt gebruiken, moet de markering `isMultiLineJson` worden ingesteld. Voor meer informatie, te lezen gelieve de [&#x200B; gids van het oplossen van problemenoplossing van de partij &#x200B;](./troubleshooting.md).

**API formaat**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van het referentiegegevensbestand. |

**Reactie**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de batch-id uit het antwoord op het aanmaken van de batch gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE]
>
>Zie de appendix sectie voor een [&#x200B; voorbeeld van een behoorlijk-geformatteerd JSON- gegevensdossier &#x200B;](#data-transformation-for-batch-ingestion).

**API formaat**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Zorg ervoor dat u een unieke bestandsnaam gebruikt, zodat er geen conflict optreedt met een ander bestand voor de batch met bestanden die wordt verzonden. |

**Verzoek**

>[!NOTE]
>
>De API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, bijvoorbeeld `acme/customers/campaigns/summer.json` . |

**Reactie**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```http
200 OK
```

## Bovenliggende bestanden samenvoegen {#ingest-parquet-files}

>[!NOTE]
>
>De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, zult u aan grote dossierupload moeten schakelen.

### Batch maken

Ten eerste moet u een batch maken met Parquet als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parameter | Beschrijving |
| --------- | ------------ |
| `{DATASET_ID}` | De id van het referentiegegevensbestand. |

**Reactie**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de instructie `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API formaat**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Zorg ervoor dat u een unieke bestandsnaam gebruikt, zodat er geen conflict optreedt met een ander bestand voor de batch met bestanden die wordt verzonden. |

**Verzoek**

>[!CAUTION]
>
>Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, bijvoorbeeld `acme/customers/campaigns/summer.parquet` . |

**Reactie**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt signaleren, is gereed voor voltooiing. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
200 OK
```

## Grote Parketbestanden samenvoegen

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u bestanden kunt uploaden die groter zijn dan 256 MB. De grote bestanden worden geüpload in blokken en vervolgens vastgezet via een API-signaal.

### Batch maken

Ten eerste moet u een batch maken met Parquet als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

**API formaat**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van het referentiegegevensbestand. |

**Reactie**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Groot bestand initialiseren

Nadat u de batch hebt gemaakt, moet u het grote bestand initialiseren voordat u bestanden naar de batch kunt uploaden.

**API formaat**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |
| `{FILE_NAME}` | De naam van het bestand dat wordt geïnitialiseerd. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
201 Created
```

### Grote bestandskoppels uploaden

Nadat het bestand is gemaakt, kunnen alle volgende hoofdstukken worden geüpload door herhaalde PATCH-aanvragen te maken, één voor elke sectie van het bestand.

**API formaat**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Zorg ervoor dat u een unieke bestandsnaam gebruikt, zodat er geen conflict optreedt met een ander bestand voor de batch met bestanden die wordt verzonden. |

**Verzoek**

>[!CAUTION]
>
>Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In gehele getallen, het begin en het eind van de gevraagde waaier. |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, bijvoorbeeld `acme/customers/campaigns/summer.json` . |


**Reactie**

```http
200 OK
```

### Volledig groot bestand

Nu u een batch hebt gemaakt, kunt u de instructie `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API formaat**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarvan u wilt aangeven dat deze is voltooid. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand waarvan u wilt aangeven dat het is voltooid. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
201 Created
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt signaleren, is voltooid. |


**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
200 OK
```

## CSV-bestanden samenvoegen

om CSV- dossiers in te voeren, zult u een klasse, een schema, en een dataset moeten tot stand brengen die CSV steunt. Voor gedetailleerde informatie over hoe te om de noodzakelijke klasse en het schema tot stand te brengen, volg de instructies die in het [&#x200B; worden verstrekt ad hoc zelfstudie van de schemaverwezenlijking &#x200B;](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, zult u aan grote dossierupload moeten schakelen.

### Gegevensset maken

Na het volgen van de instructies hierboven om de noodzakelijke klasse en het schema tot stand te brengen, zult u een dataset moeten creëren die CSV kan steunen.

**API formaat**

```http
POST /catalog/dataSets
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. |
| `{SCHEMA_ID}` | De id van het schema dat u hebt gemaakt. |

### Batch maken

Vervolgens moet u een batch maken met CSV als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema in overeenstemming zijn verbonden met de verstrekte dataset.

**API formaat**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van het referentiegegevensbestand. |

**Reactie**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de instructie `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE]
>
>Zie de appendix sectie voor een [&#x200B; voorbeeld van een behoorlijk-geformatteerd Csv- gegevensdossier &#x200B;](#data-transformation-for-batch-ingestion).

**API formaat**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Zorg ervoor dat u een unieke bestandsnaam gebruikt, zodat er geen conflict optreedt met een ander bestand voor de batch met bestanden die wordt verzonden. |

**Verzoek**

>[!CAUTION]
>
>Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, bijvoorbeeld `acme/customers/campaigns/summer.csv` . |


**Reactie**

```http
200 OK
```

### Volledige batch

Als u alle verschillende delen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```http
200 OK
```

## Een batch annuleren

Tijdens de verwerking van de batch kan deze nog steeds worden geannuleerd. Als een batch echter eenmaal is voltooid (bijvoorbeeld een successtatus of een mislukte status), kan de batch niet worden geannuleerd.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt annuleren. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
200 OK
```

## Een batch verwijderen {#delete-a-batch}

Een partij kan worden geschrapt door het volgende POST- verzoek met de `action=REVERT` vraagparameter aan identiteitskaart van de partij uit te voeren u wenst om te schrappen. De partij is gemerkt als &quot;inactief&quot;, die het voor huisvuilinzameling in aanmerking laten komen. De partij wordt asynchroon verzameld, waarna de partij als &quot;geschrapt&quot;zal worden gemerkt.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt verwijderen. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

```http
200 OK
```

## Een batch repareren

Soms kan het nodig zijn gegevens bij te werken in het profielarchief van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Adobe Experience Platform ondersteunt de update of patch van de profielopslaggegevens via een upsert action of &quot;patching a batch&quot;.

>[!NOTE]
>
>Deze updates zijn alleen toegestaan voor profielrecords, geen gebeurtenissen.

Het volgende is vereist om een batch te kunnen repareren:

- **dataset van A die voor de updates van het Profiel en van attributen wordt toegelaten.** Dit gebeurt via gegevenssetcodes en er moet een specifieke `isUpsert:true` -tag worden toegevoegd aan de `unifiedProfile` -array. Voor detailstappen die tonen hoe te om een dataset tot stand te brengen of een bestaande dataset voor upsert te vormen, volg het leerprogramma voor [&#x200B; toelatend een dataset voor de updates van het Profiel &#x200B;](../../catalog/datasets/enable-upsert.md).
- **het Dossier van het Pakket van A die de gebieden bevat die moeten worden gerepareerd en identiteitsgebieden voor het Profiel.** De gegevensindeling voor het patcheren van een batch is vergelijkbaar met het normale proces voor het inslikken van batch. De vereiste invoer is een Parquet-bestand. Naast de velden die moeten worden bijgewerkt, moeten de geüploade gegevens de identiteitsvelden bevatten om overeen te komen met de gegevens in het Profile Store.

Zodra u een dataset hebt die voor Profiel en upsert wordt toegelaten, en een dossier van het Pakket dat de gebieden bevat u wenst om evenals de noodzakelijke identiteitsgebieden te repareren, kunt u de stappen voor [&#x200B; volgen die de dossiers van het Pakket &#x200B;](#ingest-parquet-files) opnemen om het flard via partijopname te voltooien.

## Een batch opnieuw afspelen

Als u een reeds opgenomen partij wilt vervangen, kunt u dit met &quot;partij replay&quot;doen - deze actie is gelijkwaardig aan het schrappen van de oude partij en het opnemen van nieuwe in plaats daarvan.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn. Bovendien moet u de oude batch(s) als referentie opgeven in de sectie Opnieuw afspelen. In het onderstaande voorbeeld speelt u batches opnieuw af met id&#39;s `batchIdA` en `batchIdB` .

**API formaat**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parameter | Beschrijving |
| --------- | ----------- | 
| `{DATASET_ID}` | De id van het referentiegegevensbestand. |

**Reactie**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | The ID of the referenced dataset. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |


### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de instructie `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API formaat**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Zorg ervoor dat u een unieke bestandsnaam gebruikt, zodat er geen conflict optreedt met een ander bestand voor de batch met bestanden die wordt verzonden. |

**Verzoek**

>[!CAUTION]
>
>Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is. Gebruik de optie curl -F niet, omdat deze standaard een meerdelige aanvraag bevat die niet compatibel is met de API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, bijvoorbeeld `acme/customers/campaigns/summer.json` . |

**Reactie**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API formaat**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt voltooien. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```http
200 OK
```

## Bijlage

De volgende sectie bevat aanvullende informatie voor het innemen van gegevens in Experience Platform door middel van batch-inname.

### Gegevenstransformatie voor batch-opname

Om een gegevensdossier in [!DNL Experience Platform] in te nemen, moet de hiërarchische structuur van het dossier met het [&#x200B; Model van de Gegevens van de Ervaring (XDM) &#x200B;](../../xdm/home.md) schema voldoen verbonden aan de dataset die wordt geupload aan.

De informatie over hoe te om een Csv- dossier in kaart te brengen om aan een XDM- schema te voldoen kan in het [&#x200B; steekproeftransformaties &#x200B;](../../etl/transformations.md) document, samen met een voorbeeld van een behoorlijk geformatteerd JSON- gegevensdossier worden gevonden. Hier vindt u voorbeeldbestanden in het document:

- [&#x200B; CRM_profiles.csv &#x200B;](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [&#x200B; CRM_profiles.json &#x200B;](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
