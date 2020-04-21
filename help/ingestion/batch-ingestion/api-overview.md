---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Batch Ingestieontwikkelaarshandleiding
topic: developer guide
translation-type: tm+mt
source-git-commit: 6c17351b04fedefd4b57b9530f1d957da8183a68

---


# Handleiding voor het ontwikkelen van batterijen

Dit document biedt een uitgebreid overzicht van het gebruik van API&#39;s voor [batchinvoer](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

De bijlage bij dit document bevat informatie voor het [opmaken van gegevens die moeten worden gebruikt voor inname](#data-transformation-for-batch-ingestion), waaronder voorbeeld-CSV- en JSON-gegevensbestanden.

## Aan de slag

Gegevensinvoer biedt een RESTful-API waarmee u standaard CRUD-bewerkingen kunt uitvoeren op de ondersteunde objecttypen.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben naast elkaar om met succes vraag aan de Ingestie API van de Partij te maken.

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [Inname](./overview.md)in batch: Hiermee kunt u gegevens als batchbestanden in Adobe Experience Platform opnemen.
- [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
- [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

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

Voor aanvragen die een payload (POST, PUT, PATCH) bevatten, is mogelijk een extra `Content-Type` header nodig. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters. In deze handleiding worden de volgende inhoudstypen gebruikt:

- Inhoudstype: application/json
- Inhoudstype: application/octet-stream

## Typen

Bij het opnemen van gegevens is het belangrijk om te begrijpen hoe de schema&#39;s van het Gegevensmodel van de Ervaring (XDM) werken. Voor meer informatie over hoe de de gebiedstypes van XDM aan verschillende formaten in kaart brengen, te lezen gelieve de de ontwikkelaarsgids [van de Registratie van het](../../xdm/api/getting-started.md)Schema.

Er is enige flexibiliteit bij het opnemen van gegevens - als een type niet aanpast wat in het doelschema is, zullen de gegevens in het uitgedrukt doeltype worden omgezet. Als dit niet het geval is, zal het de partij met een `TypeCompatibilityException`.

JSON en CSV hebben bijvoorbeeld geen datum- of datum-tijdtype. Dientengevolge, worden deze waarden uitgedrukt gebruikend [ISO 8061 geformatteerde koorden](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) of Unix Tijd geformatteerd in milliseconden (153126395999 000) en worden bij inname omgezet in het doel-XDM-type.

In de onderstaande tabel worden de conversies weergegeven die worden ondersteund bij het invoeren van gegevens.

| Binnenkomend (rij) vs. Doel (kolom) | String | Byte | Kort | Geheel | Lang | Dubbel | Datum | Datum/tijd | Object | Kaart |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| String | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Kort | X | X | X | X | X | X |  |  |  |  |
| Geheel | X | X | X | X | X | X |  |  |  |  |
| Lang | X | X | X | X | X | X | X | X |  |  |
| Dubbel | X | X | X | X | X | X |  |  |  |  |
| Datum |  |  |  |  |  |  | X |  |  |  |
| Datum/tijd |  |  |  |  |  |  |  | X |  |  |
| Object |  |  |  |  |  |  |  |  | X | X |
| Kaart |  |  |  |  |  |  |  |  | X | X |

>[!NOTE] Booleaanse waarden en arrays kunnen niet naar andere typen worden geconverteerd.

## Ingestiebeperkingen

De gegevensinvoer in de batch heeft enkele beperkingen:
- Maximumaantal bestanden per batch: 1500
- Maximale batchgrootte: 100 GB
- Maximumaantal eigenschappen of velden per rij: 10000
- Maximumaantal batches per minuut per gebruiker: 138

## Ingest JSON-bestanden

>[!NOTE] De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, moet u op grote dossier schakelen uploadt.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

>[!NOTE] De voorbeelden hieronder zijn voor single-line JSON. Om JSON met meerdere regels in te voeren, moet de `isMultiLineJson` markering worden ingesteld. Lees voor meer informatie de handleiding voor het oplossen van problemen met [batchinvoer](./troubleshooting.md).

**API-indeling**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de methode `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE] Zie de bijlage voor een [voorbeeld van een JSON-gegevensbestand](#data-transformation-for-batch-ingestion)met de juiste indeling.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. |

**Verzoek**

>[!NOTE] De API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```http
200 OK
```

## Bovenliggende bestanden samenvoegen

>[!NOTE] De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, zult u aan grote dossierupload moeten schakelen.

### Batch maken

Ten eerste moet u een batch maken met Parquet als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn.

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de methode `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. |

**Verzoek**

>[!CAUTION] Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
200 OK
```

## Grote Parketbestanden samenvoegen

>[!NOTE] In deze sectie wordt beschreven hoe u bestanden kunt uploaden die groter zijn dan 256 MB. De grote bestanden worden geüpload in blokken en vervolgens vastgezet via een API-signaal.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
201 Created
```

### Grote bestandskoppels uploaden

Nu het bestand is gemaakt, kunnen alle volgende hoofdstukken worden geüpload door herhaalde PATCH-aanvragen te maken, één voor elke sectie van het bestand.

**API-indeling**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. |

**Verzoek**

>[!CAUTION] Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In gehele getallen, het begin en het eind van de gevraagde waaier. |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. |


**Antwoord**

```http
200 OK
```

### Volledig groot bestand

Nu u een batch hebt gemaakt, kunt u de methode `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
200 OK
```

## CSV-bestanden samenvoegen

om CSV- dossiers in te voeren, zult u een klasse, een schema, en een dataset moeten tot stand brengen die CSV steunt. Voor gedetailleerde informatie over hoe te om de noodzakelijke klasse en het schema tot stand te brengen, volg de instructies die in de [ad hoc zelfstudie](../../xdm/api/ad-hoc.md)van de schemaverwezenlijking worden verstrekt.

>[!NOTE] De volgende stappen zijn van toepassing op kleine bestanden (256 MB of minder). Als u een gatewayonderbreking of de fouten van de verzoeklichaamsomvang raakt, zult u aan grote dossierupload moeten schakelen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. |
| `{SCHEMA_ID}` | De id van het schema dat u hebt gemaakt. |

Een uitleg van wat het verschillende gedeelte van de sectie &quot;fileDescription&quot; van de JSON-hoofdtekst hieronder kan worden weergegeven:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `format` | De indeling van het hoofdbestand, niet de indeling van het invoerbestand. |
| `delimiters` | Het teken dat als scheidingsteken moet worden gebruikt. |
| `quotes` | Het teken dat voor aanhalingstekens moet worden gebruikt. |
| `escapes` | Het teken dat als escape-teken moet worden gebruikt. |
| `header` | Het geüploade bestand **moet** kopteksten bevatten. Aangezien de schemabevestiging wordt gedaan, moet dit aan waar worden geplaatst. Daarnaast mogen kopteksten **geen** spaties bevatten. Als u spaties in de koptekst hebt, vervangt u deze door onderstrepingstekens. |
| `charset` | Een optioneel veld. Andere ondersteunde tekensets zijn US-ASCII en ISO-8869-1. Als deze parameter leeg blijft, wordt standaard UTF-8 gebruikt. |

De dataset waarnaar wordt verwezen moet het hierboven vermelde blok van de dossierbeschrijving hebben en moet aan een geldig schema in de registratie richten. Anders wordt het bestand niet in parket gebracht.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de nieuwe batch. |
| `{DATASET_ID}` | De id van de gegevensset waarnaar wordt verwezen. |
| `{USER_ID}` | De id van de gebruiker die de batch heeft gemaakt. |

### Bestanden uploaden

Nu u een batch hebt gemaakt, kunt u de methode `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

>[!NOTE] Zie de appendix sectie voor een [voorbeeld van een behoorlijk-formatted Csv- gegevensdossier](#data-transformation-for-batch-ingestion).

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. |

**Verzoek**

>[!CAUTION] Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
200 OK
```

## Een batch verwijderen {#delete-a-batch}

Een partij kan worden geschrapt door het volgende POST- verzoek met de `action=REVERT` vraagparameter aan identiteitskaart van de partij uit te voeren u wenst om te schrappen. De partij is gemerkt als &quot;inactief&quot;, die het voor huisvuilinzameling in aanmerking laten komen. De partij wordt asynchroon verzameld, waarna de partij als &quot;geschrapt&quot;zal worden gemerkt.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwoord**

```http
200 OK
```

## Een batch opnieuw afspelen

Als u een reeds opgenomen partij wilt vervangen, kunt u dit met &quot;partij replay&quot;doen - deze actie is gelijkwaardig aan het schrappen van de oude partij en het opnemen van nieuwe in plaats daarvan.

### Batch maken

Ten eerste moet u een batch maken, met JSON als invoerindeling. Wanneer het creëren van de partij, zult u een datasetidentiteitskaart moeten verstrekken. U zult ook moeten ervoor zorgen dat alle dossiers die als deel van de partij worden geupload met het schema XDM verbonden aan de verstrekte dataset in overeenstemming zijn. Bovendien moet u de oude batch(s) als referentie opgeven in de sectie Opnieuw afspelen. In het onderstaande voorbeeld speelt u batches opnieuw met id&#39;s `batchIdA` en `batchIdB`.

**API-indeling**

```http
POST /batches
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

Nu u een batch hebt gemaakt, kunt u de methode `batchId` from before gebruiken om bestanden naar de batch te uploaden. U kunt meerdere bestanden uploaden naar de batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De id van de batch waarnaar u wilt uploaden. |
| `{DATASET_ID}` | De id van de referentiegegevensset van de batch. |
| `{FILE_NAME}` | De naam van het bestand dat u wilt uploaden. |

**Verzoek**

>[!CAUTION] Deze API biedt ondersteuning voor uploaden in één onderdeel. Zorg ervoor dat het inhoudstype application/octet-stream is. Gebruik de optie curl -F niet, omdat deze standaard een meerdelige aanvraag bevat die niet compatibel is met de API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Het volledige pad en de naam van het bestand dat u wilt uploaden. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```http
200 OK
```

## Aanhangsel

### Gegevenstransformatie voor batch-opname

Om een gegevensdossier in het Platform van de Ervaring in te gaan, moet de hiërarchische structuur van het dossier het schema van de Gegevens van de [Ervaring (XDM)](../../xdm/home.md) in acht nemen verbonden aan de dataset die aan wordt geupload.

Informatie over hoe u een CSV-bestand kunt toewijzen om te voldoen aan een XDM-schema vindt u in het document met [voorbeeldtransformaties](../../etl/transformations.md) , samen met een voorbeeld van een JSON-gegevensbestand met de juiste indeling. Hier vindt u voorbeeldbestanden in het document:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)