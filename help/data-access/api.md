---
keywords: Experience Platform;home;populaire onderwerpen;gegevenstoegang;python sdk;spark sdk;gegevenstoegang api;export;Export
solution: Experience Platform
title: API-handleiding voor gegevenstoegang
topic: developer guide
description: De API van de Toegang van Gegevens steunt Adobe Experience Platform door ontwikkelaars van een RESTful interface te voorzien die op de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets binnen Experience Platform wordt geconcentreerd.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 1%

---


# API-handleiding voor gegevenstoegang

De API van de Toegang van Gegevens steunt Adobe Experience Platform door gebruikers van een RESTful interface te voorzien die op de ontdekkingsbaarheid en de toegankelijkheid van opgenomen datasets binnen [!DNL Experience Platform] wordt geconcentreerd.

![Toegang tot gegevens op Experience Platform](images/Data_Access_Experience_Platform.png)

## API-specificatieverwijzing

De naslagdocumentatie voor de Swagger-API vindt u [hier](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologie

Een beschrijving van enkele veelgebruikte termen in dit document.

| Term | Beschrijving |
| ----- | ------------ |
| Gegevensset | Een verzameling gegevens met een schema en velden. |
| Batch | Een reeks gegevens die over een bepaalde periode worden verzameld en samen als één eenheid worden verwerkt. |

## Lijst met bestanden in een batch ophalen

Door een batch-id (batchID) te gebruiken, kan de API voor gegevenstoegang een lijst ophalen met bestanden die tot die bepaalde batch behoren.

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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

De array `"data"` bevat een lijst met alle bestanden in de opgegeven batch. Elk geretourneerd bestand heeft een eigen unieke id (`{FILE_ID}`) in het veld `"dataSetFileId"`. Deze unieke id kan vervolgens worden gebruikt om het bestand te openen of te downloaden.

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.dataSetFileId` | De bestands-id voor elk bestand in de opgegeven batch. |
| `data._links.self.href` | De URL voor toegang tot het bestand. |

## Bestanden in een batch openen en downloaden

Door een dossier herkenningsteken (`{FILE_ID}`) te gebruiken, kan API van de Toegang van Gegevens worden gebruikt om tot specifieke details van een dossier, met inbegrip van zijn naam, grootte in bytes, en een verbinding toegang te hebben om te downloaden.

De reactie bevat een gegevensarray. Afhankelijk van het feit of het bestand waarnaar de id verwijst een afzonderlijk bestand of een map is, kan de geretourneerde gegevensarray één item of een lijst met bestanden bevatten die tot die map behoren. Elk bestandselement bevat de details van het bestand.

**API-indeling**

```http
GET /files/{FILE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | Gelijk aan `"dataSetFileId"`, identiteitskaart van het te betreden dossier. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Eén bestandreactie**

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
| `data.name` | Naam van het bestand (bijvoorbeeld profielen.csv). |
| `data.length` | Grootte van het bestand (in bytes). |
| `data._links.self.href` | De URL waarmee het bestand moet worden gedownload. |

**Mapreactie**

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
| `data.name` | Naam van het bestand (bijvoorbeeld profielen.csv). |
| `data._links.self.href` | De URL waarmee het bestand moet worden gedownload. |

## De inhoud van een bestand openen

De [!DNL Data Access] API kan ook worden gebruikt om tot de inhoud van een dossier toegang te hebben. Deze kan vervolgens worden gebruikt om de inhoud naar een externe bron te downloaden.

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand in een gegevensset. |
| `{FILE_NAME}` | De volledige naam van het bestand (bijvoorbeeld profielen.csv). |

**Antwoord**

`Contents of the file`

## Aanvullende codevoorbeelden

Voor extra steekproeven, gelieve te verwijzen naar [gegevens tot leerprogramma](tutorials/dataset-data.md).

## Abonneren op gebeurtenissen voor gegevensinvoer

[!DNL Platform] maakt specifieke hoogwaardige gebeurtenissen beschikbaar voor abonnement via de  [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). U kunt bijvoorbeeld een abonnement nemen op gebeurtenissen voor het opnemen van gegevens om op de hoogte te worden gebracht van mogelijke vertragingen en mislukkingen. Zie de zelfstudie over [abonneren op gegevensinvoer-meldingen](../ingestion/quality/subscribe-events.md) voor meer informatie.