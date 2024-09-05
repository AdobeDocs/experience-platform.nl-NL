---
keywords: Experience Platform;home;populaire onderwerpen;gegevenstoegang;python sdk;spark sdk;gegevenstoegang api;export;Export
solution: Experience Platform
title: API-handleiding voor gegevenstoegang
description: De API van de Toegang van Gegevens steunt Adobe Experience Platform door ontwikkelaars van een RESTful interface te voorzien die op de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets binnen Experience Platform wordt geconcentreerd.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 1070c34bcd4577fcc5f0ac160196450db3aab9b0
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# API-handleiding voor gegevenstoegang

>[!IMPORTANT]
>
>De Toegang API van Gegevens is nu verouderd ****. U wordt aangeraden Doelen te gebruiken voor het exporteren van gegevens uit Adobe Experience Platform. Voor meer informatie, gelieve te verwijzen naar de [ documentatie van de de uitvoerbestemmingen van de dataset ](../destinations/destination-types.md#dataset-export-destinations).

De API voor gegevenstoegang ondersteunt Adobe Experience Platform door gebruikers een RESTful-interface te bieden die is gericht op de detecteerbaarheid en toegankelijkheid van opgenomen datasets binnen [!DNL Experience Platform] .

![ een diagram van hoe de Toegang van Gegevens de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets binnen Experience Platform vergemakkelijkt.](images/Data_Access_Experience_Platform.png)

## API-specificatieverwijzing

De OpenAPI verwijzingsdocumentatie kan [ hier ](https://developer.adobe.com/experience-platform-apis/references/data-access/) worden gevonden.

## Terminologie {#terminology}

De tabel bevat een beschrijving van enkele termen die in dit document worden gebruikt.

| Term | Beschrijving |
| ----- | ------------ |
| Gegevensset | Een verzameling gegevens die een schema en velden bevat. |
| Batch | Een reeks gegevens die over een bepaalde periode worden verzameld en samen als één eenheid worden verwerkt. |

## Lijst met bestanden in een batch ophalen {#retrieve-list-of-files-in-a-batch}

Als u een lijst wilt ophalen met bestanden die tot een bepaalde batch behoren, gebruikt u de batch-id (batchID) met de API voor gegevenstoegang.

**API formaat**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de opgegeven batch. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

De array `"data"` bevat een lijst met alle bestanden in de opgegeven batch. Elk geretourneerd bestand heeft een eigen unieke id (`{FILE_ID}`) in het veld `"dataSetFileId"` . Met deze unieke id kunt u het bestand openen of downloaden.

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.dataSetFileId` | De bestands-id voor elk bestand in de opgegeven batch. |
| `data._links.self.href` | De URL voor toegang tot het bestand. |

## Bestanden in een batch openen en downloaden

Om tot specifieke details van een dossier toegang te hebben, gebruik een dossierherkenningsteken (`{FILE_ID}`) met de API van de Toegang van Gegevens, met inbegrip van zijn naam, grootte in bytes, en een verbinding om te downloaden.

De reactie bevat een gegevensarray. Afhankelijk van het feit of het bestand waarnaar de id verwijst een afzonderlijk bestand of een map is, kan de geretourneerde gegevensarray één item of een lijst met bestanden bevatten die tot die map behoren. Elk bestandselement bevat de details van het bestand.

**API formaat**

```http
GET /files/{FILE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand dat moet worden geopend, komt overeen met de `"dataSetFileId"` . |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Enige dossierreactie**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.name` | De naam van het bestand (bijvoorbeeld `profiles.csv` ). |
| `data.length` | De bestandsgrootte (in bytes). |
| `data._links.self.href` | De URL waarmee het bestand moet worden gedownload. |

**reactie van de Folder**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

Wanneer een map wordt geretourneerd, bevat deze een array van alle bestanden in de map.

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.name` | De naam van het bestand (bijvoorbeeld `profiles.csv` ). |
| `data._links.self.href` | De URL waarmee het bestand moet worden gedownload. |

## De inhoud van een bestand openen {#access-file-contents}

U kunt de API van [!DNL Data Access] ook gebruiken om tot de inhoud van een dossier toegang te hebben. U kunt de inhoud vervolgens downloaden naar een externe bron.

**API formaat**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_NAME}` | De naam van het bestand dat u wilt openen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand in een gegevensset. |
| `{FILE_NAME}` | De volledige naam van het bestand (bijvoorbeeld `profiles.csv` ). |

**Reactie**

`Contents of the file`

## Aanvullende codevoorbeelden

Voor extra steekproeven, verwijs naar het [ leerprogramma van de gegevenstoegang ](tutorials/dataset-data.md).

## Abonneren op gebeurtenissen voor gegevensinvoer {#subscribe-to-data-ingestion-events}

U kunt aan specifieke high-value gebeurtenissen door [ Adobe Developer Console ](https://developer.adobe.com/console/) intekenen. U kunt bijvoorbeeld een abonnement nemen op gebeurtenissen voor het opnemen van gegevens om op de hoogte te worden gebracht van mogelijke vertragingen en mislukkingen. Zie het leerprogramma op [ intekenend aan de gebeurtenisberichten van de Adobe ](../observability/alerts/subscribe.md) voor meer informatie.
