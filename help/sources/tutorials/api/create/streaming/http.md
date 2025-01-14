---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;api-hulplijn;zelfstudie;maak een streamingverbinding;streaming opname;opname;
title: Een HTTP API voor streaming verbinding maken met de Flow Service API
description: Deze zelfstudie bevat stappen voor het maken van een streamingverbinding met de HTTP API-bron voor Raw- en XDM-gegevens met de Flow Service API.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---


# Een HTTP API-streamingverbinding maken met de API [!DNL Flow Service]

De Flow Service wordt gebruikt om klantgegevens van verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Dit leerprogramma gebruikt [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/) om u door de stappen te lopen om een het stromen verbinding tot stand te brengen gebruikend [!DNL Flow Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] ervaringsgegevens ordent.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, consumentenprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.

Bovendien, vereist het creëren van een het stromen verbinding u om een doelXDM schema en een dataset te hebben. Leren hoe te om deze tot stand te brengen, te lezen gelieve het leerprogramma op [ het stromen verslaggegevens ](../../../../../ingestion/tutorials/streaming-record-data.md) of het leerprogramma op [ het stromen tijdreeksgegevens ](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding geeft de bron aan en bevat de informatie die nodig is om de stroom compatibel te maken met streaming opname-API&#39;s. Wanneer u een basisverbinding maakt, kunt u een niet-geverifieerde en een geverifieerde verbinding maken.

### Niet-geverifieerde verbinding

Niet-geverifieerde verbindingen zijn de standaardstreamingverbindingen die u kunt maken wanneer u gegevens wilt streamen naar Platform.

Als u een niet-geverifieerde basisverbinding wilt maken, vraagt u een POST naar het `/connections` -eindpunt terwijl u een naam opgeeft voor de verbinding, het gegevenstype en de specificatie-id van de HTTP-API-verbinding. Deze id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb` .

**API formaat**

```http
POST /flowservice/connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor de HTTP-API gemaakt.

>[!BEGINTABS]

>[!TAB  XDM ]

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

>[!TAB  Ruwe gegevens ]

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
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met HTTP API. Deze id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb` . |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Tot de ondersteunde waarden behoren: `xdm` en `raw` . |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe basisverbinding. |
| `etag` | Een id die is toegewezen aan de verbinding en die de versie van de basisverbinding opgeeft. |

### Geverifieerde verbinding

De voor authentiek verklaarde verbindingen zouden moeten worden gebruikt wanneer u tussen verslagen moet onderscheiden die uit vertrouwde op en niet-vertrouwde op bronnen komen. Gebruikers die gegevens met PII (Personeel Identified Information) willen verzenden, moeten een geverifieerde verbinding maken bij het streamen van gegevens naar Platform.

Als u een geverifieerde basisverbinding wilt maken, moet u de parameter `authenticationRequired` in uw aanvraag opnemen en de waarde ervan opgeven als `true` . Tijdens deze stap kunt u ook een bron-id opgeven voor uw geverifieerde basisverbinding. Deze parameter is optioneel en gebruikt dezelfde waarde als het attribuut `name` als dit niet wordt opgegeven.


**API formaat**

```http
POST /flowservice/connections
```

**Verzoek**

Met de volgende aanvraag wordt een geverifieerde basisverbinding voor de HTTP-API gemaakt.

>[!BEGINTABS]

>[!TAB  XDM ]

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
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB  Ruwe gegevens ]

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
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | Een extra id die kan worden gebruikt bij het maken van een geverifieerde basisverbinding. Deze parameter is optioneel en gebruikt dezelfde waarde als het attribuut `name` als dit niet wordt opgegeven. |
| `auth.params.authenticationRequired` | Deze parameter geeft aan of verificatie vereist is voor de streamingverbinding. Als `authenticationRequired` is ingesteld op `true` , moet verificatie worden opgegeven voor de streamingverbinding. Als `authenticationRequired` is ingesteld op `false` , is verificatie niet vereist. |

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## URL voor streamingeindpunt ophalen

Als de basisverbinding is gemaakt, kunt u nu de URL van het streamingeindpunt ophalen.

**API formaat**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De `id` waarde van de verbinding u eerder creeerde. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de waarde `inletUrl` .

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
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
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

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan het `/sourceConnections` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding.

**API formaat**

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

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met gedetailleerde van de pas gecreëerde bronverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan de [ Registratie API van het Schema ](https://www.adobe.io/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](../../../../../xdm/api/schemas.md).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan de [ Dienst API van de Catalogus uit te voeren ](https://developer.adobe.com/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](../../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, vraagt u de POST om `/targetConnections` terwijl u id&#39;s opgeeft voor uw doelgegevensset en doel-XDM-schema. Tijdens deze stap, moet u ook identiteitskaart van de de verbindingsspecificatie van het datumpigment verstrekken. Deze id is `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

**API formaat**

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

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde doelverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt.

Om een mappingsreeks tot stand te brengen, doe een verzoek van de POST aan het `mappingSets` eindpunt van [[!DNL Data Prep]  API ](https://developer.adobe.com/experience-platform-apis/references/data-prep/) terwijl het verstrekken van uw doelXDM schema `$id` en de details van de mappingsreeksen u wilt tot stand brengen.

**API formaat**

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
| `xdmSchema` | The `$id` of the target XDM schema. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

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

## Een gegevensstroom maken

Wanneer uw bron- en doelverbindingen zijn gemaakt, kunt u nu een gegevensstroom maken. De dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST aan het `/flows` eindpunt uit te voeren.

**API formaat**

```http
POST /flows
```

**Verzoek**

>[!BEGINTABS]

>[!TAB  XDM ]

Met de volgende aanvraag wordt een streaminggegevensstroom voor XDM-gegevens gemaakt.

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

>[!TAB  RAW ]

Met de volgende aanvragen wordt een streaming gegevensstroom voor onbewerkte gegevens gemaakt.

Wanneer u een gegevensstroom maakt met transformaties, kan de parameter `name` niet worden gewijzigd. Deze waarde moet altijd worden ingesteld op `Mapping` .

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
| `flowSpec.id` | De flowspecificatie-id voor [!DNL HTTP API] . Als u een gegevensstroom met transformaties wilt maken, moet u `c1a19761-d2c7-4702-b9fa-fe91f0613e81` gebruiken. Gebruik `d8a6f005-7eaf-4153-983e-e8574508b877` om een gegevensstroom zonder transformaties te maken. |
| `sourceConnectionIds` | [ bron verbindingsidentiteitskaart ](#source) die in een vroegere stap wordt teruggewonnen. |
| `targetConnectionIds` | De [ identiteitskaart van de doelverbinding ](#target) die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met details van uw onlangs gecreeerd dataflow, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## Post gegevens die aan Platform moeten worden opgenomen {#ingest-data}

>[!NOTE]
>
>U moet een vertraging van minstens ~5 minuten toevoegen tussen het maken van een gegevensstroom en het invoeren van streaming gegevens. Hierdoor kan de gegevensstroom volledig worden ingeschakeld, voordat er gegevens worden ingevoerd.

Nu u uw stroom hebt gecreeerd, kunt u uw JSON- bericht naar het het stromen eindpunt verzenden u eerder creeerde.

**API formaat**

```http
POST /collection/{INLET_URL}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INLET_URL}` | De URL van het streamingeindpunt. U kunt deze URL terugwinnen door een verzoek van de GET tot het `/connections` eindpunt te richten terwijl het verstrekken van uw identiteitskaart van de basisverbinding. |
| `{FLOW_ID}` | De id van de HTTP API-streaminggegevens. Deze id is vereist voor zowel XDM- als RAW-gegevens. |

**Verzoek**

>[!BEGINTABS]

>[!TAB  verzendt XDM- gegevens ]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
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

>[!TAB  verzendt Ruwe gegevens met stroomidentiteitskaart als kopbal van HTTP ]

Wanneer u onbewerkte gegevens verzendt, kunt u de flow-id opgeven als een queryparameter of als onderdeel van de HTTP-header. In het volgende voorbeeld wordt de flow-id opgegeven als een HTTP-header.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB  verzendt Ruwe gegevens met stroomidentiteitskaart als vraagparameter ]

Wanneer u onbewerkte gegevens verzendt, kunt u de flow-id opgeven als een queryparameter of als een HTTP-header. In het volgende voorbeeld wordt de flow-id opgegeven als een queryparameter.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
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

**Reactie**

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
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan de Adobe de levenscyclus van deze record volgen via verschillende systemen en met foutopsporing. |
| `receivedTimeMs` | Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |


## Volgende stappen

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het stromen eindpunt te gebruiken om gegevens in Platform in te voeren. Voor instructies om een het stromen verbinding in UI tot stand te brengen, te lezen gelieve [ creërend een het stromen verbindingsleerprogramma ](../../../ui/create/streaming/http.md).

Leren hoe te om gegevens aan Platform te stromen, te lezen gelieve of het leerprogramma op [ het stromen tijdreeksgegevens ](../../../../../ingestion/tutorials/streaming-time-series-data.md) of het leerprogramma op [ het stromen verslaggegevens ](../../../../../ingestion/tutorials/streaming-record-data.md).

## Bijlage

Deze sectie bevat aanvullende informatie over het maken van streamingverbindingen met de API.

### Berichten verzenden naar een geverifieerde streamingverbinding

Als verificatie is ingeschakeld voor een streamingverbinding, moet de client de header `Authorization` toevoegen aan de aanvraag.

Als de header `Authorization` niet aanwezig is of als een ongeldig/verlopen toegangstoken wordt verzonden, wordt een HTTP 401-reactie zonder toestemming geretourneerd, met een vergelijkbare reactie als hieronder:

**Reactie**

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

