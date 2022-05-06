---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;inname;ontwikkelaarshandleiding;api-handleiding;upload;ingest Parquet;ingest json;
solution: Experience Platform
title: Handleiding voor de API voor batchverwerking
description: Dit document bevat een uitgebreide handleiding voor ontwikkelaars die werken met batch-opname-API's voor Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 1%

---

# Handleiding voor het ontwikkelen van batterijen

Dit document biedt een uitgebreide handleiding voor het gebruik van [batch-opname-API-eindpunten](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) in Adobe Experience Platform. Voor een overzicht van batch-opname-API&#39;s, inclusief voorwaarden en aanbevolen procedures, begint u met het lezen van de [overzicht van batch-invoer-API](overview.md).

De bijlage bij dit document bevat informatie voor [formatteren van gegevens die voor opname moeten worden gebruikt](#data-transformation-for-batch-ingestion), inclusief voorbeeld-CSV- en JSON-gegevensbestanden.

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [Data Ingestie-API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Gegevensinvoer biedt een RESTful-API waarmee u standaard CRUD-bewerkingen kunt uitvoeren op de ondersteunde objecttypen.

Controleer voordat je doorgaat de [overzicht van batch-invoer-API](overview.md) en de [gids Aan de slag](getting-started.md).

## Ingest JSON-bestanden

>[!NOTE]
>
>De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, moet u op grote dossier schakelen uploadt.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

>[!NOTE]
>
>De voorbeelden hieronder zijn voor single-line JSON. Als u JSON met meerdere regels wilt gebruiken, `isMultiLineJson` de markering moet worden ingesteld . Lees voor meer informatie de [handleiding voor het oplossen van problemen met batchverwerking](./troubleshooting.md).

**API-indeling**

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

**Antwoord**

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
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de batch-id uit het antwoord op het aanmaken van de batch gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE]
>
>Zie het aanhangsel voor een [voorbeeld van een JSON-gegevensbestand met de juiste indeling](#data-transformation-for-batch-ingestion).

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Dit bestandspad is de locatie waar het bestand wordt opgeslagen op de zijde Adobe. |

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
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, zoals `Users/sample-user/Downloads/sample.json`. |

**Antwoord**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API-indeling**

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

**Antwoord**

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

**Antwoord**

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
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de opdracht `batchId` van tevoren om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Dit bestandspad is de locatie waar het bestand wordt opgeslagen op de zijde Adobe. |

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
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, zoals `Users/sample-user/Downloads/sample.json`. |

**Antwoord**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API-indeling**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch die u wilt signaleren, is klaar voor voltooiing. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
200 OK
```

## Grote Parketbestanden samenvoegen

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u bestanden kunt uploaden die groter zijn dan 256 MB. De grote bestanden worden geüpload in blokken en vervolgens vastgezet via een API-signaal.

### Batch maken

Ten eerste moet u een batch maken met Parquet als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

**API-indeling**

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

**Antwoord**

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
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Groot bestand initialiseren

Nadat u de batch hebt gemaakt, moet u het grote bestand initialiseren voordat u bestanden naar de batch kunt uploaden.

**API-indeling**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{FILE_NAME}` | De naam van het bestand dat wordt geïnitialiseerd. |

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
201 Created
```

### Grote bestandskoppels uploaden

Nadat het bestand is gemaakt, kunnen alle volgende elementen worden geüpload door herhaalde PATCH-aanvragen te maken, één voor elke sectie van het bestand.

**API-indeling**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Dit bestandspad is de locatie waar het bestand wordt opgeslagen op de zijde Adobe. |

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
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, zoals `Users/sample-user/Downloads/sample.json`. |


**Antwoord**

```http
200 OK
```

### Volledig groot bestand

Nu u een batch hebt gemaakt, kunt u de opdracht `batchId` van tevoren om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API-indeling**

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

**Antwoord**

```http
201 Created
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API-indeling**

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

**Antwoord**

```http
200 OK
```

## CSV-bestanden samenvoegen

om CSV- dossiers in te voeren, zult u een klasse, een schema, en een dataset moeten tot stand brengen die CSV steunt. Voor gedetailleerde informatie over hoe te om de noodzakelijke klasse en het schema tot stand te brengen, volg de instructies die in [zelfstudie over het maken van ad-hocschema&#39;s](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, zult u aan grote dossierupload moeten schakelen.

### Gegevensset maken

Na het volgen van de instructies hierboven om de noodzakelijke klasse en het schema tot stand te brengen, zult u een dataset moeten creëren die CSV kan steunen.

**API-indeling**

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
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. |
| `{SCHEMA_ID}` | De id van het schema dat u hebt gemaakt. |

### Batch maken

Vervolgens moet u een batch maken met CSV als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema in overeenstemming zijn verbonden met de verstrekte dataset.

**API-indeling**

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

**Antwoord**

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
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de opdracht `batchId` van tevoren om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE]
>
>Zie het aanhangsel voor een [voorbeeld van een CSV-gegevensbestand met de juiste indeling](#data-transformation-for-batch-ingestion).

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Dit bestandspad is de locatie waar het bestand wordt opgeslagen op de zijde Adobe. |

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
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, zoals `Users/sample-user/Downloads/sample.json`. |


**Antwoord**

```http
200 OK
```

### Volledige batch

Als u alle verschillende delen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API-indeling**

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

**Antwoord**

```http
200 OK
```

## Een batch annuleren

Tijdens de verwerking van de batch kan deze nog steeds worden geannuleerd. Als een batch echter eenmaal is voltooid (bijvoorbeeld een successtatus of een mislukte status), kan de batch niet worden geannuleerd.

**API-indeling**

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

**Antwoord**

```http
200 OK
```

## Een batch verwijderen {#delete-a-batch}

Een partij kan worden geschrapt door het volgende verzoek van de POST met uit te voeren `action=REVERT` De parameter van de vraag aan identiteitskaart van de partij u wenst om te schrappen. De partij is gemerkt als &quot;inactief&quot;, die het voor huisvuilinzameling in aanmerking laten komen. De partij wordt asynchroon verzameld, waarna de partij als &quot;geschrapt&quot;zal worden gemerkt.

**API-indeling**

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

**Antwoord**

```http
200 OK
```

## Een batch repareren

Soms kan het nodig zijn gegevens bij te werken in de profielopslag van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Adobe Experience Platform ondersteunt de update of patch van Profile Store-gegevens via een upsert-actie of &#39;patching a batch&#39;.

>[!NOTE]
>
>Deze updates zijn alleen toegestaan voor profielrecords, geen gebeurtenissen.

Het volgende is vereist om een batch te kunnen repareren:

- **Een dataset die voor de updates van het Profiel en van attributen wordt toegelaten.** Dit wordt gedaan door datasetmarkeringen en vereist een specifieke `isUpsert:true` -tag wordt toegevoegd aan de `unifiedProfile` array. Voor detailstappen die tonen hoe te om een dataset tot stand te brengen of een bestaande dataset voor upsert te vormen, volg het leerprogramma voor [het toelaten van een dataset voor de updates van het Profiel](../../catalog/datasets/enable-upsert.md).
- **Een Parket-bestand met de velden die moeten worden gerepareerd en identiteitsvelden voor het profiel.** De gegevensindeling voor het patchen van een batch is vergelijkbaar met het normale inslikproces voor batches. De vereiste invoer is een Parquet-bestand. Naast de velden die moeten worden bijgewerkt, moeten de geüploade gegevens de identiteitsvelden bevatten, zodat ze overeenkomen met de gegevens in het Profile Store.

Als u een gegevensset hebt die is ingeschakeld voor Profiel en Bijvoegen, en een Parquet-bestand dat de velden bevat die u wilt repareren en de benodigde identiteitsvelden, kunt u de stappen volgen voor [Parket-bestanden invoegen](#ingest-parquet-files) om de pleister te voltooien door middel van batch-inname.

## Een batch opnieuw afspelen

Als u een reeds opgenomen partij wilt vervangen, kunt u dit met &quot;partij replay&quot;doen - deze actie is gelijkwaardig aan het schrappen van de oude partij en het opnemen van nieuwe in plaats daarvan.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn. Bovendien moet u de oude batch(s) als referentie opgeven in de sectie Opnieuw afspelen. In het onderstaande voorbeeld worden batches opnieuw afgespeeld met id&#39;s `batchIdA` en `batchIdB`.

**API-indeling**

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

**Antwoord**

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
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |


### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de opdracht `batchId` van tevoren om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. Dit bestandspad is de locatie waar het bestand wordt opgeslagen op de zijde Adobe. |

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
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. Dit bestandspad is het lokale bestandspad, zoals `Users/sample-user/Downloads/sample.json`. |

**Antwoord**

```http
200 OK
```

### Volledige batch

Nadat u alle verschillende onderdelen van het bestand hebt geüpload, moet u aangeven dat de gegevens volledig zijn geüpload en dat de batch klaar is voor promotie.

**API-indeling**

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

**Antwoord**

```http
200 OK
```

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor het innemen van gegevens in Experience Platforms door middel van batch-inname.

### Gegevenstransformatie voor batch-opname

Om een gegevensbestand in te voeren [!DNL Experience Platform]moet de hiërarchische structuur van het bestand voldoen aan de [Experience Data Model (XDM)](../../xdm/home.md) schema verbonden aan de dataset die wordt geupload aan.

Informatie over hoe u een CSV-bestand kunt toewijzen om te voldoen aan een XDM-schema vindt u in het dialoogvenster [voorbeeldtransformaties](../../etl/transformations.md) samen met een voorbeeld van een JSON-gegevensbestand met de juiste indeling. Hier vindt u voorbeeldbestanden in het document:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
