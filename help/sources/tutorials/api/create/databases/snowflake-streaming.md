---
title: Sluit uw Snowflake-streamingaccount aan op Adobe Experience Platform
description: Leer hoe u Adobe Experience Platform kunt verbinden met Snowflake-streaming met behulp van de Flow Service API.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 8bc232034301fa713f61bd3f11fbde122afcdcf9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# Stream [!DNL Snowflake] gegevens naar Experience Platform met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>* De [!DNL Snowflake] streamingbron is in bèta. Lees de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.
>* API-ondersteuning voor de [!DNL Snowflake] De streamingbron is alleen beschikbaar voor klanten die Real-Time CDP Ultimate hebben aangeschaft.


Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding en het streamen van gegevens vanuit uw [!DNL Snowflake] account aan Adobe Experience Platform met behulp van de [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voor de opstelling van de voorwaarden en informatie over de [!DNL Snowflake] streamingbron. Lees de [[!DNL Snowflake] overzicht van streamingbron](../../../../connectors/databases/snowflake-streaming.md).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken {#create-a-base-connection}

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Snowflake] verificatiereferenties als onderdeel van de aanvraaginstantie.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Snowflake]:

>[!TIP]
>
>De `auth.specName` De waarde moet exact worden ingevoerd zoals in het onderstaande voorbeeld, inclusief de lege spaties.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.account` | De naam van uw [!DNL Snowflake] streamingaccount. |
| `auth.params.database` | De naam van uw [!DNL Snowflake] database waar gegevens worden opgehaald. |
| `auth.params.warehouse` | De naam van uw [!DNL Snowflake] magazijn. De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens over aan Platform. |
| `auth.params.username` | De gebruikersnaam voor uw [!DNL Snowflake] streamingaccount. |
| `auth.params.schema` | (Optioneel) Het databaseschema dat aan uw [!DNL Snowflake] streamingaccount. |
| `auth.params.password` | Het wachtwoord voor uw [!DNL Snowflake] streamingaccount. |
| `auth.params.role` | (Optioneel) De rol van de gebruiker voor dit [!DNL Snowflake] verbinding. Indien niet opgegeven, wordt deze waarde standaard ingesteld op `public`. |
| `connectionSpec.id` | De [!DNL Snowflake] Verbindingsspecificatie-id: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding en de bijbehorende tag.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Uw gegevenstabellen verkennen {#explore-your-data-tables}

Daarna, gebruik identiteitskaart van de basisverbinding om door de gegevenslijsten van uw bron te onderzoeken en te navigeren door een verzoek van de GET aan te dienen `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding als parameter.

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van uw [!DNL Snowflake] streamingbron. |


**Verzoek**

Het volgende verzoek wint de structuur en de inhoud van uw terug [!DNL Snowflake] streamingaccount.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de structuur en de inhoud van de gegevens van uw bron op wortel-niveau terug.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `items.type` | Het type van de tabel. |
| `items.names` | De naam van de tabel. |

## Een bronverbinding maken {#create-a-source-connection}

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan `/sourceConnections` van het [!DNL Flow Service] API.

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `baseConnectionId` | De geverifieerde basis-verbindings-id voor uw [!DNL Snowflake] streamingbron. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor de [!DNL Snowflake] streamingbron. |
| `params.tableName` | De naam van de tabel in uw [!DNL Snowflake] database die u naar het Platform wilt brengen. |
| `params.timestampColumn` | De naam van de tijdstempelkolom die wordt gebruikt om incrementele waarden op te halen. |
| `params.backfill` | Een booleaanse vlag die bepaalt of de gegevens van het begin (0 epoche tijd) of van de tijd worden gehaald de bron in werking wordt gesteld. Voor meer informatie over deze waarde leest u de [[!DNL Snowflake] overzicht van streamingbron](../../../../connectors/databases/snowflake-streaming.md). |

**Antwoord**

Een geslaagde reactie retourneert uw bron-verbindings-id en de bijbehorende tag. De bron verbindings ID zal in een recentere stap worden gebruikt om een gegevensstroom tot stand te brengen.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Een gegevensstroom maken

Een gegevensstroom maken om gegevens te streamen vanaf een rondleiding [!DNL Snowflake] aan Platform, moet u een verzoek van de POST aan `/flows` eindpunt terwijl het verstrekken van de volgende waarden:

>[!TIP]
>
>Volg de onderstaande koppelingen voor stapsgewijze handleidingen voor het ophalen van de volgende id&#39;s.

* [Bronverbinding-id](#create-a-source-connection)
* [Doelverbinding-id](../../collect/database-nosql.md#create-a-target-connection)
* [Stroom-specificatie-id](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Toewijzing-id](../../collect/database-nosql.md#create-a-mapping)

**API-indeling**

```http
POST /flows
```

**Verzoek**

Met de volgende aanvraag wordt een streaming gegevensstroom gemaakt voor uw [!DNL Snowflake] account.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `sourceConnectionIds` | De bron verbindings-id voor uw [!DNL Snowflake] streamingbron. |
| `targetConnectionIds` | De doel verbindings ID voor uw [!DNL Snowflake] streamingbron. |
| `flowSpec.id` | De flow-specificatie-id om een gegevensstroom te maken voor een [!DNL Snowflake] streamingbron. Met deze flowspecificatie-id kunt u een streaminggegevensstroom maken met toewijzingstransformaties. Deze id is vast en is: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | De toewijzings-id voor de gegevensstroom. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en de bijbehorende tag.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom voor streaming gemaakt [!DNL Snowflake] gegevens die [!DNL Flow Service] API. Raadpleeg de volgende documentatie voor aanvullende informatie over Adobe Experience Platform Sources:

* [Overzicht van bronnen](../../../../home.md)
* [Uw gegevensstroom controleren met behulp van API&#39;s](../../monitor.md)