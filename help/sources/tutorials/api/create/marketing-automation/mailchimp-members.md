---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Creeer een dataflow voor de Leden van Mailchimp gebruikend de Dienst API van de Stroom
topic-legacy: tutorial
description: Leer hoe u Adobe Experience Platform met MailChimp-leden kunt verbinden met behulp van de Flow Service API.
exl-id: 900d4073-129c-47ba-b7df-5294d25a7219
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2500'
ht-degree: 0%

---

# Een gegevensstroom maken voor [!DNL Mailchimp Members] de Flow Service API gebruiken

Het volgende leerprogramma begeleidt u door de stappen om een bronverbinding en een dataflow tot stand te brengen [!DNL Mailchimp Members] gegevens naar Platform met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Vereisten

Voordat u verbinding maakt [!DNL Mailchimp] naar Adobe Experience Platform met OAuth 2-vernieuwingscode, moet u eerst uw toegangstoken ophalen voor [!DNL MailChimp.] Zie de [[!DNL Mailchimp] Handleiding OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) voor gedetailleerde instructies bij het vinden van uw toegangstoken.

## Een basisverbinding maken {#base-connection}

Zodra u uw [!DNL Mailchimp] verificatiereferenties kunt u nu het proces starten voor het maken van een gegevensstroom om [!DNL Mailchimp Members] gegevens naar Platform. De eerste stap bij het maken van een gegevensstroom is het maken van een basisverbinding.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

[!DNL Mailchimp] steunt zowel basisauthentificatie als OAuth 2 verfrist code. Zie de volgende voorbeelden voor begeleiding op hoe te met ????n van beide authentificatietypen voor authentiek te verklaren.

### Een [!DNL Mailchimp] basisverbinding met basisverificatie

Als u een [!DNL Mailchimp] basisverbinding die basisauthentificatie gebruikt, doe een verzoek van de POST aan `/connections` eindpunt van [!DNL Flow Service] API terwijl het verstrekken van geloofsbrieven voor uw `host`, `authorizationTestUrl`, `username`, en `password`.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Mailchimp]:

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Members base connection with basic authentication",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
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
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt [!DNL Mailchimp] API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| `auth.params.authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw [!DNL Mailchimp] account. Dit is vereist voor basisverificatie. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Mailchimp] account. Dit is vereist voor basisverificatie. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### Een [!DNL Mailchimp] basisverbinding met OAuth 2-vernieuwingscode

Als u een [!DNL Mailchimp] basisverbinding die OAuth 2 gebruikt verfrist code, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van geloofsbrieven voor uw `host`, `authorizationTestUrl`, en `accessToken`.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Members base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
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
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt [!DNL Mailchimp] API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| `auth.params.authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.accessToken` | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

## Ontdek uw bron {#explore}

Met de id van de basisverbinding die u in de vorige stap hebt gegenereerd, kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren.

>[!TIP]
>
>Het geaccepteerde indelingstype ophalen voor `{SOURCE_PARAMS}`, moet u het gehele `list_id` string in base64. Bijvoorbeeld: `"list_id": "10c097ca71"` gecodeerd in base64 is gelijk aan `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`.

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Wanneer het uitvoeren van GET verzoeken om de het dossierstructuur en inhoud van uw bron te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder vermeld zijn:

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `{OBJECT_TYPE}` | Het type object dat u wilt verkennen. Voor REST-bronnen wordt deze waarde standaard ingesteld op `rest`. |
| `{OBJECT}` | Het object dat u wilt verkennen. |
| `{FILE_TYPE}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Een base64-gecodeerde tekenreeks van uw `list_id`. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de structuur van het bestand waarnaar wordt gevraagd.

```json
{ 
"data": [
    {
        "list_id": "10c097ca71",
        "_links": [
            {
                "rel": "self",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
            },
            {
                "rel": "parent",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
            },
            {
                "rel": "create",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "POST",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
            }
        ],
        "members": [
            {
                "id": "cff65fb4c5f5828666ad846443720efd",
                "email_address": "kendallt2134@gmail.com",
                "unique_email_id": "72c758cbf1",
                "contact_id": "874a0d6e9ddb89d8b4a31e416ead2d6f",
                "full_name": "Kendall Roy",
                "web_id": 547094062,
                "email_type": "html",
                "status": "subscribed",
                "consents_to_one_to_one_messaging": true,
                "merge_fields": {
                    "FNAME": "Kendall",
                    "LNAME": "Roy",
                    "ADDRESS": {
                        "country": "US"
                    }
                },
                "stats": {
                    "avg_open_rate": 0,
                    "avg_click_rate": 0
                },
                "ip_opt": "103.43.112.97",
                "timestamp_opt": "2021-06-01T15:31:36+00:00",
                "member_rating": 2,
                "last_changed": "2021-06-01T15:31:36+00:00",
                "vip": false,
                "location": {
                    "latitude": 0,
                    "longitude": 0,
                    "gmtoff": 0,
                    "dstoff": 0
                },
                "source": "Admin Add",
                "tags_count": 0,
                "list_id": "10c097ca71",
                "_links": [
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        },
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
                        },
                        {
                            "rel": "update",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PATCH",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PATCH.json"
                        },
                        {
                            "rel": "upsert",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PUT",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PUT.json"
                        },
                        {
                            "rel": "delete",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "DELETE"
                        },
                        {
                            "rel": "activity",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Activity/Response.json"
                        },
                        {
                            "rel": "goals",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/goals",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Goals/Response.json"
                        },
                        {
                            "rel": "notes",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/notes",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Notes/CollectionResponse.json"
                        },
                        {
                            "rel": "events",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/events",
                            "method": "POST",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Events/POST.json"
                        },
                        {
                            "rel": "delete_permanent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/actions/delete-permanent",
                            "method": "POST"
                        }
                    ]
                }
            ]  
        }
    ]
}
```

## Een bronverbinding maken {#source-connection}

U kunt een bronverbinding tot stand brengen door een verzoek van de POST aan [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling defini??ren.

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

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest listId",
      "description": "MailChimp Members source connection to ingest listId",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "data": {
          "format": "json",
      },
      "params": {
          "listId": "10c097ca71"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van [!DNL Mailchimp]. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met uw bron. |
| `data.format` | Het formaat van de [!DNL Mailchimp] gegevens die u wilt invoeren. |
| `params.listId` | Wordt ook wel publiek-id genoemd. [!DNL Mailchimp] lijst ID staat voor de overdracht van publieksgegevens aan andere integraties toe. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
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

Met de volgende aanvraag wordt een doelverbinding gemaakt voor [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Members target connection",
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
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Lake]. Deze vaste ID is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Het formaat van de [!DNL Mailchimp] gegevens die u naar het Platform wilt brengen. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |


**Antwoord**

Een geslaagde reactie retourneert de unieke id van de nieuwe doelverbinding (`id`). Deze id is vereist in latere stappen.

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een verzoek van de POST aan [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen die zijn gedefinieerd in de payload van het verzoek.

**API-indeling**

```http
POST /conversion/mappingSets
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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

| Eigenschap | Beschrijving |
| --- | --- |
| `xdmSchema` | De id van de [doel-XDM-schema](#target-schema) gegenereerd in een eerdere stap. |
| `mappings.destinationXdmPath` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |
| `mappings.sourceAttribute` | Het bronattribuut dat aan een bestemmingsXDM weg moet worden in kaart gebracht. |
| `mappings.identity` | Een booleaanse waarde die aangeeft of de toewijzingsset wordt gemarkeerd voor [!DNL Identity Service]. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing inclusief de unieke id (`id`). Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

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

## Een flow maken {#flow}

De laatste stap op weg naar [!DNL Mailchimp] gegevens aan Platform moeten een gegevensstroom tot stand brengen. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source-connection)
* [Doelverbinding-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day`, of `week`. De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde op gelijk aan of groter dan `15`.


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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Members dataflow",
      "description": "MailChimp Members dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc"
      ],
      "targetConnectionIds": [
          "8db5fb4a-6ce8-4370-afc0-1765e39535a5"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                  "mappingVersion": 0
              }
          }
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
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) gegenereerd in een eerdere stap. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde wordt standaard ingesteld op `0`. |
| `scheduleParams.startTime` | De aangewezen begintijd voor wanneer de eerste opname van gegevens begint. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
            "name": "MailChimp Members dataflow",
            "description": "MailChimp Members dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"2e01f11d-0000-0200-0000-615649660000\"",
            "etag": "\"2e01f11d-0000-0200-0000-615649660000\"",
            "sourceConnectionIds": [
                "e70d2773-711f-43ee-b956-9a1a5da03dd8"
            ],
            "targetConnectionIds": [
                "43e141f6-6385-4d80-a4e4-c0fb59abbd43"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "e70d2773-711f-43ee-b956-9a1a5da03dd8",
                        "connectionSpec": {
                            "id": "2e8580db-6489-4726-96de-e33f5f60295f",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "05c595e5-edc3-45c8-90bb-fcf556b57c4b",
                            "connectionSpec": {
                                "id": "2e8580db-6489-4726-96de-e33f5f60295f",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "43e141f6-6385-4d80-a4e4-c0fb59abbd43",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633044818",
                "frequency": "minute",
                "interval": 15
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/flows/209812ad-7bef-430c-b5b2-a648aae72094/runs",
            "lastOperation": {
                "started": 1633044829988,
                "updated": 0,
                "operation": "create"
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `items` | Bevat ????n enkele lading meta-gegevens verbonden aan uw specifieke stroomlooppas. |
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
              "value": "MailChimp Members Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Members Dataflow Updated"
          }
      ]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifi??ren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
          "value": "MailChimp Members Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Members Connection"
      }
  ]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de verbinding bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifi??ren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw verbinding-id opgeeft.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen.
