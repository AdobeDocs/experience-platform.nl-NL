---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;api-hulplijn;zelfstudie;maak een streamingverbinding;streaming opname;opname;
solution: Experience Platform
title: Een HTTP API-streamingverbinding maken met de API
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: d39cdeaa57a221f10c975353a54d3ff7c88239d6
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# Een [!DNL HTTP API] streamingverbinding met de API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) om u door de stappen te lopen om een het stromen verbinding tot stand te brengen gebruikend de Dienst API van de Stroom.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert ervaringsgegevens.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist het creëren van een het stromen verbinding u om een doelXDM schema en een dataset te hebben. Lees de zelfstudie voor meer informatie over het maken van deze [streaming recordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) of de zelfstudie [streaming tijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md).

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../../../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een basisverbinding maken

Een basisverbinding geeft de bron aan en bevat de informatie die nodig is om de stroom compatibel te maken met streaming opname-API&#39;s. Wanneer u een basisverbinding maakt, kunt u een niet-geverifieerde en een geverifieerde verbinding maken.

### Niet-geverifieerde verbinding

Niet-geverifieerde verbindingen zijn de standaardstreamingverbindingen die u kunt maken wanneer u gegevens wilt streamen naar het Platform.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Als u een streamingverbinding wilt maken, moet u de provider-id en de verbindingsspecificatie-id opgeven als onderdeel van het verzoek om POST. De provider-id is `521eee4d-8cbe-4906-bb48-fb6bd4450033` en de verbindingsspecificatie-id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | De id van de streamingverbinding die u wilt maken. |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm`. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor streamingverbindingen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met gegevens over de nieuwe verbinding, inclusief de unieke id (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van uw nieuwe verbinding. Dit wordt hierna aangeduid als `{CONNECTION_ID}`. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

### Geverifieerde verbinding

De voor authentiek verklaarde verbindingen zouden moeten worden gebruikt wanneer u tussen verslagen moet onderscheiden die uit vertrouwde op en niet-vertrouwde op bronnen komen. Gebruikers die gegevens met PII (Personeel Identified Information) willen verzenden, moeten een geverifieerde verbinding maken bij het streamen van gegevens naar het Platform.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Als u een streamingverbinding wilt maken, moet u de provider-id en de verbindingsspecificatie-id opgeven als onderdeel van het verzoek om POST. De provider-id is `521eee4d-8cbe-4906-bb48-fb6bd4450033` en de verbindingsspecificatie-id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | De id van de streamingverbinding die u wilt maken. |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm`. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `auth.params.authenticationRequired` | De parameter die opgeeft dat de gemaakte streamingverbinding |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor streamingverbindingen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met gegevens over de nieuwe verbinding, inclusief de unieke id (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van uw nieuwe verbinding. Dit wordt hierna aangeduid als `{CONNECTION_ID}`. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

## URL voor streamingeindpunt ophalen

Als de basisverbinding is gemaakt, kunt u nu de URL van het streamingeindpunt ophalen.

**API-indeling**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` De waarde van de verbinding die u eerder hebt gemaakt. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de `inletUrl` waarde.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Een bronverbinding maken {#source}

Nadat u de basisverbinding hebt gemaakt, moet u een bronverbinding maken. Wanneer u een bronverbinding maakt, hebt u de `id` waarde van uw gemaakte basisverbinding.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
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
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
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

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart verstrekken van verbindingsspecificatie verbonden aan het meer van Gegevens. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het meer van Gegevens. Met deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met details van de nieuwe doelverbinding, inclusief de unieke id (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
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
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Een gegevensstroom maken

Wanneer uw bron- en doelverbindingen zijn gemaakt, kunt u nu een gegevensstroom maken. De dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST aan `/flows` eindpunt.

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "HTTP API streaming dataflow",
        "description": "HTTP API streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "63070871-ec3f-4cb5-af47-cf7abb25e8bb"
        ],
        "targetConnectionIds": [
            "98a2a72e-a80f-49ae-aaa3-4783cc9404c2"
        ],
        "transformations": [
            {
            "name": "Mapping",
            "params": {
                "mappingId": "380b032b445a46008e77585e046efe5e",
                "mappingVersion": 0
            }
            }
        ]
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | De flowspecificatie-id voor [!DNL HTTP API]. Deze id is: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source) opgehaald in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target) opgehaald in een eerdere stap. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) opgehaald in een eerdere stap. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met details over de nieuwe gegevensstroom, inclusief de unieke id (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

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

### Gegevens na RAW die moeten worden ingevoerd op het Platform {#ingest-data}

Nu u uw stroom hebt gecreeerd, kunt u uw JSON bericht naar het het stromen eindpunt verzenden u eerder creeerde.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` de waarde van de nieuwe streamingverbinding. |

**Verzoek**

Het voorbeeldverzoek neemt onbewerkte gegevens aan het het stromen eindpunt op dat eerder werd gecreeerd.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
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

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details van de nieuw opgenomen informatie.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record traceren via verschillende systemen en met foutopsporing. |
| `receivedTimeMs` | Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |
