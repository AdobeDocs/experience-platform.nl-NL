---
title: Sluit uw Snowflake Streaming-account aan op Adobe Experience Platform
description: Leer hoe u Adobe Experience Platform verbindt met Snowflake Streaming met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# [!DNL Snowflake] -gegevens met de API [!DNL Flow Service] naar Experience Platform streamen

>[!IMPORTANT]
>
>
> De [!DNL Snowflake] -streamingbron is in de API beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Dit leerprogramma verstrekt stappen op hoe te om gegevens van uw [!DNL Snowflake] rekening met Adobe Experience Platform te verbinden en te stromen gebruikend [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Voor de vereiste configuratie en informatie over de [!DNL Snowflake] streamingbron. Gelieve te lezen het [[!DNL Snowflake]  stromen bronoverzicht ](../../../../connectors/databases/snowflake-streaming.md).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken {#create-a-base-connection}

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Snowflake] -verificatiegegevens op als onderdeel van de aanvraagprocedure.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Snowflake] gemaakt:

>[!TIP]
>
>De `auth.specName` -waarde moet exact worden ingevoerd zoals in het onderstaande voorbeeld, inclusief de lege spaties.

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
| `auth.params.database` | De naam van de [!DNL Snowflake] -database waaruit gegevens worden opgehaald. |
| `auth.params.warehouse` | De naam van uw [!DNL Snowflake] magazijn. Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens naar Experience Platform. |
| `auth.params.username` | De gebruikersnaam voor uw [!DNL Snowflake] streamingaccount. |
| `auth.params.schema` | (Optioneel) Het databaseschema dat aan uw [!DNL Snowflake] streamingaccount is gekoppeld. |
| `auth.params.password` | Het wachtwoord voor uw [!DNL Snowflake] streamingaccount. |
| `auth.params.role` | (Optioneel) De rol van de gebruiker voor deze [!DNL Snowflake] -verbinding. Als deze waarde niet is opgegeven, wordt deze standaard ingesteld op `public` . |
| `connectionSpec.id` | The [!DNL Snowflake] connection specification ID: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140` . |

**Reactie**

Een geslaagde reactie retourneert de nieuwe basisverbinding en de bijbehorende tag.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Uw gegevenstabellen verkennen {#explore-your-data-tables}

Gebruik vervolgens de id van de basisverbinding om de gegevenstabellen van uw bron te verkennen en door te navigeren door een GET-aanvraag in te dienen bij het `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` -eindpunt terwijl u uw id van de basisverbinding als parameter opgeeft.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbinding-id van uw [!DNL Snowflake] streamingbron. |


**Verzoek**

Met de volgende aanvraag worden de structuur en inhoud van uw [!DNL Snowflake] streamingaccount opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

Als u een bronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

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
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `baseConnectionId` | De geverifieerde basis-verbindings-id voor uw [!DNL Snowflake] streamingbron. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor de [!DNL Snowflake] streamingbron. |
| `params.tableName` | De naam van de tabel in uw [!DNL Snowflake] -database die u naar Experience Platform wilt verzenden. |
| `params.timestampColumn` | De naam van de tijdstempelkolom die wordt gebruikt om incrementele waarden op te halen. |
| `params.backfill` | Een booleaanse vlag die bepaalt of de gegevens van het begin (0 epoche tijd) of van de tijd worden gehaald de bron in werking wordt gesteld. Voor meer informatie over deze waarde, lees het [[!DNL Snowflake]  stromen bronoverzicht ](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | De tijdzonewaarde geeft aan welke tijd van de tijdzone moet worden opgehaald tijdens het opvragen van de [!DNL Snowflake] -database. Deze parameter moet worden opgegeven als de tijdstempelkolom in de config is ingesteld op `TIMESTAMP_NTZ` . Als deze optie niet is opgegeven, wordt voor `timezoneValue` standaard UTC gebruikt. |

**Reactie**

Een geslaagde reactie retourneert uw bron-verbindings-id en de bijbehorende tag. De id van de bronverbinding wordt later gebruikt om een gegevensstroom te maken.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Een gegevensstroom maken

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

Als u een gegevensstroom wilt maken om gegevens van een tour [!DNL Snowflake] -account naar Experience Platform te streamen, moet u een POST-aanvraag indienen bij het `/flows` -eindpunt en de volgende waarden opgeven:

>[!TIP]
>
>Volg de onderstaande koppelingen voor stapsgewijze handleidingen voor het ophalen van de volgende id&#39;s.

* [Source-verbinding-id](#create-a-source-connection)
* [Doel-verbindings-id](../../collect/database-nosql.md#create-a-target-connection)
* [Stroom-specificatie-id](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Toewijzing-id](../../collect/database-nosql.md#create-a-mapping)

**API formaat**

```http
POST /flows
```

**Verzoek**

Met de volgende aanvraag wordt een streaminggegevensstroom voor uw [!DNL Snowflake] -account gemaakt.

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
| `sourceConnectionIds` | De bron-verbindings-id voor uw [!DNL Snowflake] streamingbron. |
| `targetConnectionIds` | De doel verbindings-id voor uw [!DNL Snowflake] streamingbron. |
| `flowSpec.id` | De flow-specificatie-id waarmee een gegevensstroom voor een [!DNL Snowflake] -streamingbron wordt gemaakt. Met deze flowspecificatie-id kunt u een streaminggegevensstroom maken met toewijzingstransformaties. Deze id is vast en is: `c1a19761-d2c7-4702-b9fa-fe91f0613e81` . |
| `transformations.params.mappingId` | De toewijzings-id voor de gegevensstroom. |

**Reactie**

Een geslaagde reactie retourneert uw flow-id en de bijbehorende tag.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom voor uw [!DNL Snowflake] -gegevens gemaakt met de [!DNL Flow Service] API. Raadpleeg de volgende documentatie voor aanvullende informatie over Adobe Experience Platform Sources:

* [Overzicht van bronnen](../../../../home.md)
* [Uw gegevensstroom controleren met behulp van API&#39;s](../../monitor.md)
