---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;api-hulplijn;zelfstudie;maak een streamingverbinding;streaming opname;opname;
title: Een HTTP API-streamingverbinding maken met de API
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: d4889a302edbcdbe3f4a969a616c2fbc52f6c556
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---


# Een HTTP API-streamingverbinding maken met de [!DNL Flow Service] API

De Flow Service wordt gebruikt om klantgegevens van verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) om u door de stappen te lopen om een het stromen verbinding tot stand te brengen gebruikend [!DNL Flow Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert ervaringsgegevens.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist het creëren van een het stromen verbinding u om een doelXDM schema en een dataset te hebben. Lees de zelfstudie voor meer informatie over het maken van deze [streaming recordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) of de zelfstudie [streaming tijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding geeft de bron aan en bevat de informatie die nodig is om de stroom compatibel te maken met streaming opname-API&#39;s. Wanneer u een basisverbinding maakt, kunt u een niet-geverifieerde en een geverifieerde verbinding maken.

### Niet-geverifieerde verbinding

Niet-geverifieerde verbindingen zijn de standaardstreamingverbindingen die u kunt maken wanneer u gegevens wilt streamen naar het Platform.

Als u een niet-geverifieerde basisverbinding wilt maken, vraagt u een POST om `/connections` eindpunt terwijl het verstrekken van een naam voor uw verbinding, het gegevenstype, en identiteitskaart van de de verbindingsspecificatie van HTTP API. Deze id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor de HTTP-API gemaakt.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Onbewerkte gegevens]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met HTTP API. Deze id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Tot de ondersteunde waarden behoren: `xdm` en `raw`. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met gegevens over de nieuwe verbinding, inclusief de unieke id (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van uw nieuwe basisverbinding. |
| `etag` | Een id die is toegewezen aan de verbinding en die de versie van de basisverbinding opgeeft. |

### Geverifieerde verbinding

De voor authentiek verklaarde verbindingen zouden moeten worden gebruikt wanneer u tussen verslagen moet onderscheiden die uit vertrouwde op en niet-vertrouwde op bronnen komen. Gebruikers die gegevens met PII (Personeel Identified Information) willen verzenden, moeten een geverifieerde verbinding maken bij het streamen van gegevens naar het Platform.

Als u een geverifieerde basisverbinding wilt maken, moet u uw bron-id opgeven en aangeven of verificatie vereist is wanneer u een verzoek tot POST bij de `/connections` eindpunt.


**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Met de volgende aanvraag wordt een geverifieerde basisverbinding voor de HTTP-API gemaakt.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "{SOURCE_ID}",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Onbewerkte gegevens]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "raw",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | De id van de streamingverbinding die u wilt maken. |
| `auth.params.authenticationRequired` | De parameter die opgeeft dat de gemaakte streamingverbinding |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met gegevens over de nieuwe verbinding, inclusief de unieke id (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## URL voor streamingeindpunt ophalen

Als de basisverbinding is gemaakt, kunt u nu de URL van het streamingeindpunt ophalen.

**API-indeling**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De `id` De waarde van de verbinding die u eerder hebt gemaakt. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de `inletUrl` waarde.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATEDD_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Een bronverbinding maken {#source}

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan `/sourceConnections` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding.

**API-indeling**

```http
POST /flowservice/sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met gedetailleerde informatie over de nieuwe bronverbinding, inclusief de unieke id (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van de Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doel-XDM-schema kan worden gemaakt door een verzoek van de POST uit te voeren naar de [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](../../../../../xdm/api/schemas.md).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan tot stand worden gebracht door een verzoek van de POST aan [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), op voorwaarde dat de id van het doelschema zich binnen de payload bevindt.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met behulp van de API](../../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, vraagt u de POST om `/targetConnections` terwijl het verstrekken van IDs voor uw doeldataset en doelXDM schema. Tijdens deze stap, moet u ook identiteitskaart van de de verbindingsspecificatie van het datumpigment verstrekken. Deze id is `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-indeling**

```http
POST /flowservice/targetConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met details van de nieuwe doelverbinding, inclusief de unieke id (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt.

Als u een toewijzingenset wilt maken, vraagt u een POST aan de `mappingSets` van het [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) terwijl u uw doel-XDM-schema aanbiedt `$id` en de details van de toewijzingssets die u wilt maken.

**API-indeling**

```http
POST /mappingSets
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `xdmSchema` | De `$id` van het doel-XDM-schema. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing inclusief de unieke id (`id`). Deze id is later vereist om een gegevensstroom te maken.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

| Eigenschap | Beschrijving |
| --- | --- |

## Een gegevensstroom maken

Wanneer uw bron- en doelverbindingen zijn gemaakt, kunt u nu een gegevensstroom maken. De dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST aan `/flows` eindpunt.

**API-indeling**

```http
POST /flows
```

**Verzoek**

>[!BEGINTABS]

>[!TAB Zonder transformaties]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB Met transformaties]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw gegevensstroom. Zorg ervoor dat de naam van uw gegevensstroom beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw gegevensstroom omhoog te kijken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de gegevensstroom. |
| `flowSpec.id` | De flowspecificatie-id voor [!DNL HTTP API]. Als u een gegevensstroom met transformaties wilt maken, moet u  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Als u een gegevensstroom zonder transformaties wilt maken, gebruikt u `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source) opgehaald in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target) opgehaald in een eerdere stap. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) opgehaald in een eerdere stap. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met details over de nieuwe gegevensstroom, inclusief de unieke id (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## Post gegevens die aan Platform moeten worden opgenomen {#ingest-data}

Nu u uw stroom hebt gecreeerd, kunt u uw JSON bericht naar het het stromen eindpunt verzenden u eerder creeerde.

**API-indeling**

```http
POST /collection/{INLET_URL}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INLET_URL}` | De URL van het streamingeindpunt. U kunt deze URL ophalen door een GET-aanvraag in te dienen bij de `/connections` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding. |

**Verzoek**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Onbewerkte gegevens]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details van de nieuw opgenomen informatie.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record traceren via verschillende systemen en met foutopsporing. |
| `receivedTimeMs` | Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |


## Volgende stappen

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het stromen eindpunt te gebruiken om gegevens in Platform in te voeren. Voor instructies voor het maken van een streamingverbinding in de gebruikersinterface leest u de [een zelfstudie over streamingverbindingen maken](../../../ui/create/streaming/http.md).

Lees de zelfstudie voor meer informatie over het streamen van gegevens naar het Platform. [streaming tijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md) of de zelfstudie [streaming recordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md).

## Aanhangsel

Deze sectie bevat aanvullende informatie over het maken van streamingverbindingen met de API.

### Berichten verzenden naar een geverifieerde streamingverbinding

Als verificatie is ingeschakeld voor een streamingverbinding, moet de client het volgende toevoegen: `Authorization` aan hun verzoek.

Als de `Authorization` header is not present, or an invalid/expired access token is sent, an HTTP 401 Unauthorised response will be returned, with a similar response as below:

**Antwoord**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
