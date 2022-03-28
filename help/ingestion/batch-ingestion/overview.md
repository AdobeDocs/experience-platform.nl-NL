---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevensopname;partij;Partij;Gegevensset inschakelen;Overzicht van inname van batch;overzicht;overzicht;overzicht van inname van batch
solution: Experience Platform
title: Overzicht van de API voor batchverwerking
topic-legacy: overview
description: Met de Adobe Experience Platform Data Ingestie-API kunt u gegevens als batchbestanden in het Platform invoeren. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket), of gegevens zijn die aan een bekend schema in het register van het Model van de Gegevens van de Ervaring (XDM) in overeenstemming zijn.
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 4%

---

# Overzicht van de API voor inname van batch

Met de Adobe Experience Platform Data Ingestie-API kunt u gegevens als batchbestanden in het Platform invoeren. Gegevens die worden ingevoerd, kunnen profielgegevens zijn van een vlak bestand (zoals een Parquet-bestand) of gegevens die overeenkomen met een bekend schema in het [!DNL Experience Data Model] (XDM) register.

De [Referentie voor API voor gegevensverwerking](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) bevat aanvullende informatie over deze API-aanroepen.

Het volgende diagram schetst het proces van partijingestie:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [Data Ingestie-API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

### [!DNL Data Ingestion] voorwaarden

- De gegevens die moeten worden geüpload, moeten de indeling Parquet of JSON hebben.
- Een dataset die in [[!DNL Catalog services]](../../catalog/home.md).
- De inhoud van het dossier van het Pakket moet een ondergroep van het schema van de dataset aanpassen die in wordt geupload.
- Heb uw uniek Token van de Toegang na authentificatie.

### Aanbevolen werkwijzen bij inname in batch

- De aanbevolen batch is tussen 256 MB en 100 GB.
- Elke batch moet maximaal 1500 bestanden bevatten.

### Beperkingen bij inname in batch

De gegevensinvoer in de batch heeft enkele beperkingen:

- Maximumaantal bestanden per batch: 1500
- Maximale batchgrootte: 100 GB
- Maximumaantal eigenschappen of velden per rij: 10000
- Maximumaantal batches per minuut per gebruiker: 138

>[!NOTE]
>
>Als u een bestand wilt uploaden dat groter is dan 512 MB, moet het bestand in kleinere delen worden verdeeld. Instructies voor het uploaden van een groot bestand vindt u in de [groot gedeelte voor het uploaden van bestanden in dit document](#large-file-upload---create-file).

### Typen

Bij het invoeren van gegevens is het belangrijk om te begrijpen hoe [!DNL Experience Data Model] (XDM) schema&#39;s werken. Voor meer informatie over hoe XDM gebiedstypes aan verschillende formaten in kaart brengen, gelieve te lezen [Handleiding voor ontwikkelaars van het schema Register](../../xdm/api/getting-started.md).

Er is enige flexibiliteit bij het opnemen van gegevens - als een type niet aanpast wat in het doelschema is, zullen de gegevens in het uitgedrukt doeltype worden omgezet. Als dit niet het geval is, zal de batchverwerking mislukken met een `TypeCompatibilityException`.

JSON en CSV hebben bijvoorbeeld geen `date` of `date-time` type. Deze waarden worden dus uitgedrukt met [Tekenreeksen met ISO 8061-indeling](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15&quot;):05:59,000-08:00&quot;) of Unix Tijd die in milliseconden (1531263959000) wordt geformatteerd en bij inname in het doelXDM type wordt omgezet.

In de onderstaande tabel worden de conversies weergegeven die worden ondersteund bij het invoeren van gegevens.

| Binnenkomend (rij) vs. Doel (kolom) | Tekenreeks | Byte | Kort | Geheel | Lang | Dubbel | Datum | Datum/tijd | Object | Kaart |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Tekenreeks | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Kort | X | X | X | X | X | X |  |  |  |  |
| Geheel | X | X | X | X | X | X |  |  |  |  |
| Lang | X | X | X | X | X | X | X | X |  |  |
| Dubbel | X | X | X | X | X | X |  |  |  |  |
| Datum |  |  |  |  |  |  | X |  |  |  |
| Datum/tijd |  |  |  |  |  |  |  | X |  |  |
| Object |  |  |  |  |  |  |  |  | X | X |
| Kaart |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Booleaanse waarden en arrays kunnen niet naar andere typen worden geconverteerd.

## De API gebruiken

De [!DNL Data Ingestion] API staat u toe om gegevens als partijen (een eenheid gegevens in te voeren die uit één of meerdere dossiers bestaat die als één enkele eenheid moeten worden opgenomen) in [!DNL Experience Platform] in drie basisstappen :

1. Maak een nieuwe batch.
2. Upload dossiers aan een gespecificeerde dataset die het XDM schema van de gegevens aanpast.
3. Geef het einde van de batch aan.

## Een batch maken

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
  -H "x-api-key: {API_KEY}"
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

U kunt bestanden uploaden met de API voor kleine bestanden uploaden. Als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden (zoals uitgebreide time-outs, aanvragen voor een grotere bestandsgrootte en andere beperkingen), kunt u overschakelen naar de API voor het uploaden van grote bestanden. Deze API uploadt het bestand in delen en koppelt gegevens aan elkaar met behulp van de API-aanroep voor groot uploaden van bestand voltooid.

>[!NOTE]
>
>De inname van de partij kan worden gebruikt om gegevens in de Opslag van het Profiel stapsgewijs bij te werken. Zie de sectie over [een batch bijwerken](#patch-a-batch) in de [handleiding voor het ontwikkelen van batch-inhoud](api-overview.md).

>[!INFO]
>
>In de onderstaande voorbeelden worden de [Apache Parquet](https://parquet.apache.org/docs/) bestandsindeling. Een voorbeeld met de JSON-bestandsindeling vindt u in het dialoogvenster [handleiding voor het ontwikkelen van batch-inhoud](api-overview.md).

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
  -H "x-api-key: {API_KEY}" \
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

Nadat het bestand is gemaakt, kunnen alle volgende elementen worden geüpload door herhaalde PATCH-aanvragen te maken, één voor elke sectie van het bestand.

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

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Door dit te doen, [!DNL Catalog] DataSetFile-items worden gemaakt voor de voltooide bestanden en zijn gekoppeld aan de hierboven gegenereerde batch. De [!DNL Catalog] batch wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

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
-H "x-api-key: {API_KEY}"
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

De `"status"` is wat de huidige status van de gevraagde partij toont. De batches kunnen een van de volgende statussen hebben:

## Statistieken van inname in batch

| Status | Beschrijving |
| ------ | ----------- |
| Verlaten | De batch is niet binnen de verwachte tijd voltooid. |
| Afgebroken | Een afbreekbewerking heeft **expliciet** is aangeroepen (via Batch Ingest-API) voor de opgegeven batch. Wanneer de batch in de status &quot;Geladen&quot; is, kan deze niet worden afgebroken. |
| Actief | De partij is met succes bevorderd en is beschikbaar voor downstreamconsumptie. Deze status kan door elkaar worden gebruikt met &quot;Succes&quot;. |
| Verwijderd | De gegevens voor de batch zijn volledig verwijderd. |
| Mislukt | Een eindstaat die uit of slechte configuratie en/of slechte gegevens voortvloeit. Gegevens voor een mislukte batch worden **niet** opdagen. Deze status kan door elkaar worden gebruikt met &quot;Mislukking&quot;. |
| Inactief | De batch is gepromoveerd, maar is teruggezet of verlopen. De partij is niet meer beschikbaar voor downstreamconsumptie. |
| Geladen | De gegevens voor de partij zijn volledig en de partij is klaar voor bevordering. |
| Laden | Gegevens voor deze batch worden geüpload en de batch is momenteel **niet** klaar om te worden bevorderd. |
| Opnieuw proberen | De gegevens voor deze batch worden verwerkt. Vanwege een systeem- of overgangsfout is de batch echter mislukt. Hierdoor wordt deze batch opnieuw geprobeerd. |
| Staand | De testfase van het promotieproces voor een batch is voltooid en de innametaak is uitgevoerd. |
| Staging | De gegevens voor de partij worden verwerkt. |
| Gestopt | De gegevens voor de batch worden verwerkt. De batchbevordering is echter vastgelopen na een aantal pogingen. |
