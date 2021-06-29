---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;api-hulplijn;zelfstudie;maak een streamingverbinding;streaming opname;opname;
solution: Experience Platform
title: Een streamingverbinding maken met de API
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 42b8710cf6c04fabf7df1f005fae6b3828eeee49
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---


# Een streamingverbinding maken met de API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om door de stappen te lopen om een streamingverbinding te maken met behulp van de Flow Service API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Het gestandaardiseerde kader voor het  [!DNL Platform] organiseren van ervaringsgegevens.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist het creëren van een het stromen verbinding u om een doelXDM schema en een dataset te hebben. Lees de zelfstudie over [streaming recordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) of de zelfstudie over [streaming tijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md) voor meer informatie over het maken van deze bestanden.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../../../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

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
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm` zijn. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor het stromen verbindingen. |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe verbinding. Dit wordt hierna `{CONNECTION_ID}` genoemd. |
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
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm` zijn. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `auth.params.authenticationRequired` | De parameter die opgeeft dat de gemaakte streamingverbinding |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor het stromen verbindingen. |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe verbinding. Dit wordt hierna `{CONNECTION_ID}` genoemd. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

## URL voor streamingeindpunt ophalen

Als de basisverbinding is gemaakt, kunt u nu de URL van het streamingeindpunt ophalen.

**API-indeling**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` waarde van de verbinding u eerder creeerde. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de waarde `inletUrl`.

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

## Een bronverbinding maken

Nadat u de basisverbinding hebt gemaakt, moet u een bronverbinding maken. Wanneer u een bronverbinding maakt, hebt u de waarde `id` van uw gemaakte basisverbinding nodig.

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

## Een doelverbinding maken

Nadat u de bronverbinding hebt gemaakt, kunt u een doelverbinding maken. Wanneer het creëren van uw doelverbinding, zult u de `id` waarde van uw eerder gecreeerde dataset nodig hebben.

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

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde doelverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Een gegevensstroom maken

Wanneer uw bron- en doelverbindingen zijn gemaakt, kunt u nu een gegevensstroom maken. De dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST aan het `/flows` eindpunt uit te voeren.

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
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van uw onlangs gecreeerd dataflow, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het stromen eindpunt te gebruiken om gegevens in Platform in te voeren. Lees de [zelfstudie voor het maken van een streamingverbinding](../../../ui/create/streaming/http.md) voor instructies voor het maken van een streamingverbinding in de gebruikersinterface.

Lees de zelfstudie over [streamingtijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md) of de zelfstudie over [streamingrecordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) voor meer informatie over het streamen van gegevens naar Platform.

## Aanhangsel

Deze sectie bevat aanvullende informatie over het maken van streamingverbindingen met de API.

### Berichten verzenden naar een geverifieerde streamingverbinding

Als verificatie is ingeschakeld voor een streamingverbinding, moet de client de `Authorization`-header aan hun aanvraag toevoegen.

Als de `Authorization` kopbal niet aanwezig is, of een ongeldig/verlopen toegangstoken wordt verzonden, zal een HTTP 401 Onbevoegde reactie worden teruggekeerd, met een gelijkaardige reactie zoals hieronder:

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
| `{CONNECTION_ID}` | De `id`-waarde van de nieuwe streamingverbinding. |

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
