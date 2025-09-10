---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;batch;Batch;gegevensset inschakelen;Overzicht van inname van batch;overzicht;overzicht;overzicht van inname van batch;
solution: Experience Platform
title: Overzicht van de API voor batchverwerking
description: Met de Adobe Experience Platform Batch Ingestie-API kunt u gegevens als batchbestanden in Experience Platform invoeren. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket), of gegevens zijn die aan een bekend schema in het register van het Model van de Gegevens van de Ervaring (XDM) in overeenstemming zijn.
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: dace7bc2f7940748422628b62f0f57854036ad3f
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 1%

---

# Overzicht van de API voor inname van batch

Met de Adobe Experience Platform Batch Ingestie-API kunt u gegevens als batchbestanden in Experience Platform invoeren. Gegevens die worden ingesloten, kunnen profielgegevens zijn van een vlak bestand (zoals een Parquet-bestand) of gegevens die overeenkomen met een bekend schema in het XDM-register ([!DNL Experience Data Model] ).

De [ Verwijzing van de Opname API van de Partij ](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) verstrekt extra informatie over deze API vraag.

Het volgende diagram schetst het proces van partijingestie:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [ de Ingestie API van de Partij ](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

### [!DNL Data Ingestion] voorwaarden

- De gegevens die moeten worden geüpload, moeten de indeling Parquet of JSON hebben.
- Een dataset die in [[!DNL Catalog services]](../../catalog/home.md) wordt gecreeerd.
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
- Maximumaantal batches per minuut op data Lake per gebruiker: 2000

>[!NOTE]
>
>Als u een bestand wilt uploaden dat groter is dan 512 MB, moet het bestand in kleinere delen worden verdeeld. De instructies om een groot dossier te uploaden kunnen in de [ grote dossier worden gevonden uploadt sectie van dit document ](#large-file-upload---create-file).

### Typen

Bij het opnemen van gegevens is het belangrijk dat u begrijpt hoe [!DNL Experience Data Model] (XDM)-schema&#39;s werken. Voor meer informatie over hoe de types van XDM- gebied aan verschillende formaten in kaart brengen, gelieve de [ de ontwikkelaarsgids van de Registratie van het Schema ](../../xdm/api/getting-started.md) te lezen.

Er is enige flexibiliteit wanneer het opnemen van gegevens - als een type niet aanpast wat in het doelschema is, zullen de gegevens in het uitgedrukt doeltype worden omgezet. Als dit niet het geval is, mislukt de batch met een `TypeCompatibilityException` .

JSON en CSV hebben bijvoorbeeld geen `date` - of `date-time` -type. Dientengevolge, worden deze waarden uitgedrukt gebruikend [ ISO 8601 geformatteerde koorden ](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15 :05: 59.000-08 :00&quot;) of Unix Tijd die in milliseconden (1531263950 wordt geformatteerd (00) en worden bij inname omgezet in het doel-XDM-type.

In de onderstaande tabel worden de conversies weergegeven die worden ondersteund bij het invoeren van gegevens.

| Binnenkomend (rij) vs. Doel (kolom) | String | Byte | Kort | Geheel | Lang | Dubbel | Datum | Datum/tijd | Object | Kaart |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| String | X | X | X | X | X | X | X | X |   |   |
| Byte | X | X | X | X | X | X |   |   |   |   |
| Kort | X | X | X | X | X | X |   |   |   |   |
| Geheel | X | X | X | X | X | X |   |   |   |   |
| Lang | X | X | X | X | X | X | X | X |   |   |
| Dubbel | X | X | X | X | X | X |   |   |   |   |
| Datum |   |   |   |   |   |   | X |   |   |   |
| Datum/tijd |   |   |   |   |   |   |   | X |   |   |
| Object |   |   |   |   |   |   |   |   | X | X |
| Kaart |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>Booleaanse waarden en arrays kunnen niet worden omgezet in andere typen.

## De API gebruiken

Met de API van [!DNL Data Ingestion] kunt u gegevens in drie basisstappen als batches (een gegevenseenheid die bestaat uit een of meer bestanden die als één eenheid moeten worden opgenomen) in [!DNL Experience Platform] invoeren:

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de batch die zojuist is gemaakt (wordt gebruikt in volgende aanvragen). |
| `relatedObjects.id` | De id van de gegevensset waarin de bestanden moeten worden geüpload. |

## Bestand uploaden

Nadat een nieuwe batch is gemaakt om te uploaden, kunnen bestanden vervolgens naar een specifieke gegevensset worden geüpload.

U kunt bestanden uploaden met de API voor kleine bestanden uploaden. Als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden (zoals uitgebreide time-outs, aanvragen voor een grotere bestandsgrootte en andere beperkingen), kunt u overschakelen naar de API voor het uploaden van grote bestanden. Deze API uploadt het bestand in delen en koppelt gegevens aan elkaar met behulp van de API-aanroep voor groot uploaden van bestand voltooid.

>[!NOTE]
>
>De opname van de partij kan worden gebruikt om gegevens in de opslag van het Profiel stapsgewijs bij te werken. Voor meer informatie, zie de sectie op [ het bijwerken van een partij ](#patch-a-batch) in de [ gids van de de partijontwikkelaar van de inname ](api-overview.md).

>[!INFO]
>
>De voorbeelden hieronder gebruiken het [ Apache 1} dossierformaat van het Pakket {. ](https://parquet.apache.org/docs/) Een voorbeeld dat het JSON dossierformaat gebruikt kan in de [ handleiding van de partijontwikkelaar ](api-overview.md) worden gevonden.

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Op deze manier worden de [!DNL Catalog] DataSetFile-items gemaakt voor de voltooide bestanden en gekoppeld aan de hierboven gegenereerde batch. De batch [!DNL Catalog] wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

**Verzoek**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die in de gegevensset moet worden geüpload. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
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

**API formaat**

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
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

In het veld `"status"` wordt de huidige status van de aangevraagde batch weergegeven. De batches kunnen een van de volgende statussen hebben:

## Statistieken van inname in batch

| Status | Beschrijving |
| ------ | ----------- |
| Verlaten | De batch is niet binnen de verwachte tijd voltooid. |
| Afgebroken | Een afbreekverrichting heeft **uitdrukkelijk** geroepen (via Samenvatting van de Partij API) voor de gespecificeerde partij. Wanneer de batch in de status &quot;Geladen&quot; is, kan deze niet worden afgebroken. |
| Actief | De partij is met succes bevorderd en is beschikbaar voor downstreamconsumptie. Deze status kan door elkaar worden gebruikt met &quot;Succes&quot;. |
| Verwijderd | De gegevens voor de batch zijn volledig verwijderd. |
| Mislukt | Een eindstaat die uit of slechte configuratie en/of slechte gegevens voortvloeit. De gegevens voor een ontbroken partij zullen **niet** verschijnen. Deze status kan door elkaar worden gebruikt met &quot;Mislukking&quot;. |
| Inactief | De batch is gepromoveerd, maar is teruggezet of verlopen. De partij is niet meer beschikbaar voor downstreamconsumptie. |
| Geladen | De gegevens voor de partij zijn volledig en de partij is klaar voor bevordering. |
| Laden | De gegevens voor deze partij worden geupload en de partij is momenteel **niet** klaar om worden bevorderd. |
| Opnieuw proberen | De gegevens voor deze batch worden verwerkt. Vanwege een systeem- of overgangsfout is de batch echter mislukt. Hierdoor wordt deze batch opnieuw geprobeerd. |
| Staand | De testfase van het promotieproces voor een batch is voltooid en de innametaak is uitgevoerd. |
| Staging | De gegevens voor de partij worden verwerkt. |
| Gestopt | De gegevens voor de batch worden verwerkt. De batchbevordering is echter vastgelopen na een aantal pogingen. |
