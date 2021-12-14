---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Een dataflow maken voor MailChimp-campagne met behulp van de Flow Service API
topic-legacy: tutorial
description: Leer hoe u Adobe Experience Platform verbindt met MailChimp-campagne met behulp van de Flow Service API.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 0%

---

# Een gegevensstroom maken voor [!DNL MailChimp Campaign] de Flow Service API gebruiken

Het volgende leerprogramma begeleidt u door de stappen om een bronverbinding en een dataflow tot stand te brengen [!DNL MailChimp Campaign] gegevens naar Platform met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Vereisten

Voordat u verbinding maakt [!DNL MailChimp] naar Adobe Experience Platform met OAuth 2-vernieuwingscode, moet u eerst uw toegangstoken ophalen voor [!DNL MailChimp.] Zie de [[!DNL MailChimp] Handleiding OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) voor gedetailleerde instructies bij het vinden van uw toegangstoken.

## Een basisverbinding maken {#base-connection}

Zodra u uw [!DNL MailChimp] verificatiereferenties kunt u nu het proces starten voor het maken van een gegevensstroom om [!DNL MailChimp Campaign] gegevens naar Platform. De eerste stap bij het maken van een gegevensstroom is het maken van een basisverbinding.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

[!DNL MailChimp] steunt zowel basisauthentificatie als OAuth 2 verfrist code. Zie de volgende voorbeelden voor begeleiding op hoe te met één van beide authentificatietypen voor authentiek te verklaren.

### Een [!DNL MailChimp] basisverbinding met basisverificatie

Als u een [!DNL MailChimp] basisverbinding die basisauthentificatie gebruikt, doe een verzoek van de POST aan `/connections` eindpunt van [!DNL Flow Service] API terwijl het verstrekken van geloofsbrieven voor uw `host`, `authorizationTestUrl`, `username`, en `password`.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL MailChimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with basic authentication",
      "description": "MailChimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat de bron is geregistreerd en goedgekeurd via het [!DNL Flow Service] API. |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verbinden met Platform. |
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt [!DNL MailChimp] API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| `auth.params.authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw [!DNL MailChimp] account. Dit is vereist voor basisverificatie. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL MailChimp] account. Dit is vereist voor basisverificatie. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### Een [!DNL MailChimp] basisverbinding met OAuth 2-vernieuwingscode

Als u een [!DNL MailChimp] basisverbinding die OAuth 2 gebruikt verfrist code, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van geloofsbrieven voor uw `host`, `authorizationTestUrl`, en `accessToken`.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL MailChimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat u de bron hebt geregistreerd met de [!DNL Flow Service] API. |
| `auth.specName` | Het authentificatietype dat u gebruikt om uw bron aan Platform voor authentiek te verklaren. |
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt [!DNL MailChimp] API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| `auth.params.authorizationTestUrl` | (Optioneel) De testURL voor autorisaties wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.accessToken` | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Ontdek uw bron {#explore}

Met de id van de basisverbinding die u in de vorige stap hebt gegenereerd, kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren. Wanneer het uitvoeren van GET verzoeken om de het dossierstructuur en inhoud van uw bron te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder vermeld zijn:

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `{OBJECT_TYPE}` | Het type object dat u wilt verkennen. Voor REST-bronnen wordt deze waarde standaard ingesteld op `rest`. |
| `{OBJECT}` | Het object dat u wilt verkennen. |
| `{FILE_TYPE}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Een base64-gecodeerde tekenreeks van uw `campaign_id`. |

>[!TIP]
>
>Het geaccepteerde indelingstype ophalen voor `{SOURCE_PARAMS}`, moet u het gehele `campaignId` string in base64. Bijvoorbeeld: `{"campaignId": "c66a200cda"}` gecodeerd in base64 is gelijk aan `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de structuur van het bestand waarnaar wordt gevraagd.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## Een bronverbinding maken {#source-connection}

U kunt een bronverbinding tot stand brengen door een verzoek van de POST aan [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor bestandsgebaseerde bronnen:

| Gegevensindeling | Enumwaarde |
| ----------- | ---------- |
| Gescheiden | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Voor alle op tabellen gebaseerde bronnen stelt u de waarde in op `tabular`.

**API-indeling**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL MailChimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van [!DNL MailChimp]. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met uw bron. |
| `data.format` | Het formaat van de [!DNL MailChimp] gegevens die u wilt invoeren. |
| `params.campaignId` | De [!DNL MailChimp] campagne-id een specifieke [!DNL MailChimp] en kunt u vervolgens e-mails naar uw lijsten/publiek sturen. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van de Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doel-XDM-schema kan worden gemaakt door een verzoek van de POST uit te voeren naar de [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](../../../../../xdm/api/schemas.md).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan tot stand worden gebracht door een verzoek van de POST aan [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), op voorwaarde dat de id van het doelschema zich binnen de payload bevindt.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met behulp van de API](../../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste verbindingsspecificatie-id opgeven die overeenkomt met de [!DNL Data Lake]. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan [!DNL Data Lake]. Met deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding gemaakt voor [!DNL MailChimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de doelverbinding. Zorg ervoor dat de naam van uw doelverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw doelverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Lake]. Deze vaste ID is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Het formaat van de [!DNL MailChimp] gegevens die u naar het Platform wilt brengen. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |


**Antwoord**

Een geslaagde reactie retourneert de unieke id van de nieuwe doelverbinding (`id`). Deze id is vereist in latere stappen.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>Data prep-functies worden momenteel niet ondersteund voor [!DNL MailChimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## Een flow maken {#flow}

De laatste stap op weg naar [!DNL MailChimp] gegevens aan Platform moeten een gegevensstroom tot stand brengen. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source-connection)
* [Doelverbinding-id](#target-connection)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day`, of `week`. De intervalwaarde geeft de periode aan tussen twee opeenvolgende inname en het maken van een eenmalige inname (`once`) hoeft geen interval te worden ingesteld. Voor alle andere frequenties moet de intervalwaarde op gelijk aan of groter dan `15`.


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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw gegevensstroom. Zorg ervoor dat de naam van uw gegevensstroom beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw gegevensstroom omhoog te kijken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de gegevensstroom. |
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste ID is: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | De corresponderende versie van de flow specification-id. Deze waarde wordt standaard ingesteld op `1.0`. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source-connection) gegenereerd in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target-connection) gegenereerd in een eerdere stap. |
| `scheduleParams.startTime` | De aangewezen begintijd voor wanneer de eerste opname van gegevens begint. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien.

**API-indeling**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Verzoek**

Het volgende verzoek wint de specificaties voor een bestaande gegevensstroom terug.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert details betreffende uw stroomlooppas, met inbegrip van informatie over zijn aanmaakdatum, bron en doelverbindingen, evenals uniek herkenningsteken van de stroomlooppas (`id`).

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `items` | Bevat één enkele lading meta-gegevens verbonden aan uw specifieke stroomlooppas. |
| `id` | Hiermee geeft u de id weer die overeenkomt met uw gegevensstroom. |
| `state` | Toont de huidige staat van uw gegevensstroom. |
| `inheritedAttributes` | Bevat de attributen die uw stroom, zoals IDs voor zijn overeenkomstige basis, bron, en doelverbinding bepalen. |
| `scheduleParams` | Bevat informatie over het innameschema van uw gegevensstroom, zoals zijn begintijd (in epoche tijd), frequentie, en interval. |
| `transformations` | Bevat informatie over de transformatie-eigenschappen die op de gegevensstroom zijn toegepast. |
| `runs` | Geeft de bijbehorende runtime-id van de flow weer. U kunt deze id gebruiken om specifieke flowuitvoering te controleren. |

## Uw gegevensstroom bijwerken

Voer een PATCH-verzoek uit aan de [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en het nieuwe programma u wilt gebruiken.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze header is de unieke versie van de verbinding die u wilt bijwerken.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

De volgende aanvraag werkt uw schema voor de uitvoering van de flow bij, evenals de naam en beschrijving van uw gegevensstroom.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Uw gegevensstroom verwijderen

Met een bestaande stroom-id kunt u een gegevensstroom verwijderen door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API.

**API-indeling**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` waarde voor de gegevensstroom u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan dataflow te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## De verbinding bijwerken

Als u de naam, beschrijving en referenties van uw verbinding wilt bijwerken, moet u een PATCH-verzoek uitvoeren naar de [!DNL Flow Service] API terwijl het verstrekken van uw identiteitskaart van de basisverbinding, versie, en de nieuwe informatie u wilt gebruiken.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze header is de unieke versie van de verbinding die u wilt bijwerken.

**API-indeling**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De unieke `id` waarde voor de verbinding u wilt bijwerken. |

**Verzoek**

De volgende aanvraag bevat een nieuwe naam en beschrijving, plus een nieuwe set referenties waarmee u de verbinding kunt bijwerken.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de verbinding bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw verbinding-id opgeeft.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Verbinding verwijderen

Zodra u een bestaande identiteitskaart van de basisverbinding hebt, voer een verzoek van de DELETE aan [!DNL Flow Service] API.

**API-indeling**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De unieke `id` waarde voor de basisverbinding u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen.
