---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Maak een gegevensstroom voor Mailchimp-leden met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform met MailChimp-leden kunt verbinden met behulp van de Flow Service API.
exl-id: 900d4073-129c-47ba-b7df-5294d25a7219
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '2102'
ht-degree: 0%

---

# Een gegevensstroom maken voor [!DNL Mailchimp Members] met behulp van de Flow Service API

Het volgende leerprogramma begeleidt u door de stappen om een bronverbinding en een dataflow tot stand te brengen om [!DNL Mailchimp Members] gegevens aan Platform te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Vereisten

Alvorens u [!DNL Mailchimp] met Adobe Experience Platform kunt verbinden gebruikend OAuth 2 verfrist code, moet u uw toegangstoken voor [!DNL MailChimp.] eerst terugwinnen zie [[!DNL Mailchimp]  OAuth 2 gids ](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) voor gedetailleerde instructies bij het vinden van uw toegangstoken.

## Een basisverbinding maken {#base-connection}

Nadat u de verificatiereferenties van [!DNL Mailchimp] hebt opgehaald, kunt u nu beginnen met het maken van een gegevensstroom om [!DNL Mailchimp Members] -gegevens naar het platform te brengen. De eerste stap bij het maken van een gegevensstroom is het maken van een basisverbinding.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

[!DNL Mailchimp] ondersteunt zowel basisverificatie als OAuth 2-vernieuwingscode. Zie de volgende voorbeelden voor begeleiding op hoe te met één van beide authentificatietypen voor authentiek te verklaren.

### Een [!DNL Mailchimp] basisverbinding maken met behulp van basisverificatie

Als u een [!DNL Mailchimp] -basisverbinding wilt maken met behulp van basisverificatie, vraagt u een POST naar het `/connections` eindpunt van de [!DNL Flow Service] API en geeft u de gegevens voor de `authorizationTestUrl` , `username` en `password` -API op.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Mailchimp] gemaakt:

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
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat de bron is geregistreerd en goedgekeurd via de API van [!DNL Flow Service] . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verbinden met Platform. |
| `auth.params.authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw [!DNL Mailchimp] -account. Dit is vereist voor basisverificatie. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Mailchimp] -account. Dit is vereist voor basisverificatie. |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### Een [!DNL Mailchimp] basisverbinding maken met OAuth 2-vernieuwingscode

Als u een [!DNL Mailchimp] -basisverbinding wilt maken met OAuth 2-vernieuwingscode, vraagt u een POST naar het `/connections` -eindpunt terwijl u referenties voor uw `authorizationTestUrl` en `accessToken` opgeeft.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Mailchimp] gemaakt:

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
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat u de bron hebt geregistreerd met de API van [!DNL Flow Service] . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verifiëren bij Platform. |
| `auth.params.authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `auth.params.accessToken` | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

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
>Als u het geaccepteerde indelingstype voor `{SOURCE_PARAMS}` wilt ophalen, moet u de volledige `list_id` -tekenreeks coderen in base64. `"list_id": "10c097ca71"` die bijvoorbeeld in base64 is gecodeerd, is gelijk aan `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=` .

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Wanneer het uitvoeren van GET verzoeken om de het dossierstructuur en inhoud van uw bron te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder vermeld zijn:

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `{OBJECT_TYPE}` | Het type object dat u wilt verkennen. Voor REST-bronnen is deze waarde standaard ingesteld op `rest` . |
| `{OBJECT}` | Het object dat u wilt verkennen. |
| `{FILE_TYPE}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Een base64-gecodeerde tekenreeks van de `list_id` . |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

U kunt een bronverbinding maken door een aanvraag voor een POST in te dienen bij de [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor bestandsgebaseerde bronnen:

| Gegevensindeling | Enumwaarde |
| ----------- | ---------- |
| Gescheiden | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Stel de waarde in op `tabular` voor alle op tabellen gebaseerde bronnen.

**API formaat**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL Mailchimp] :

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
| `data.format` | De indeling van de [!DNL Mailchimp] -gegevens die u wilt invoeren. |
| `params.listId` | Met de lijst-id [!DNL Mailchimp] die ook wel publieks-id wordt genoemd, kunt u publieksgegevens overdragen naar andere integraties. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan de [ Registratie API van het Schema ](https://www.adobe.io/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](../../../../../xdm/api/schemas.md).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan de [ Dienst API van de Catalogus uit te voeren ](https://developer.adobe.com/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](../../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste verbindingsspecificatie-id opgeven die overeenkomt met de [!DNL Data Lake] . Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan [!DNL Data Lake]. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding voor [!DNL Mailchimp] gemaakt:

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
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Lake] . Deze vaste id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` . |
| `data.format` | De indeling van de [!DNL Mailchimp] -gegevens die u naar het platform wilt verzenden. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |


**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een verzoek van de POST aan [[!DNL Data Prep]  API ](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

**API formaat**

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
| `xdmSchema` | Identiteitskaart van het [ doelXDM- schema ](#target-schema) in een vroegere stap wordt geproduceerd. |
| `mappings.destinationXdmPath` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |
| `mappings.sourceAttribute` | Het bronkenmerk dat moet worden toegewezen aan een XDM-doelpad. |
| `mappings.identity` | Een Booleaanse waarde die aangeeft of de toewijzingsset wordt gemarkeerd voor [!DNL Identity Service] . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

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

De laatste stap in de richting van het brengen van [!DNL Mailchimp] -gegevens naar Platform is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Source-verbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day` of `week` . De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde worden ingesteld op gelijk aan of groter dan `15` .


**API formaat**

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
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste id is: `6499120c-0b15-42dc-936e-847ea3c24d72` . |
| `flowSpec.version` | De corresponderende versie van de specificatie-id voor de stroom. Deze waarde is standaard ingesteld op `1.0` . |
| `sourceConnectionIds` | [ bron verbindingsidentiteitskaart ](#source-connection) die in een vroegere stap wordt geproduceerd. |
| `targetConnectionIds` | De [ identiteitskaart van de doelverbinding ](#target-connection) die in een vroegere stap wordt geproduceerd. |
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt geproduceerd. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde is standaard ingesteld op `0` . |
| `scheduleParams.startTime` | De aangewezen begintijd voor wanneer de eerste opname van gegevens begint. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day` of `week` . |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie is ingesteld op `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
}
```

## Bijlage

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor volledige API voorbeelden, lees de gids op [ controlerend uw brongegevens gebruikend API ](../../monitor.md).

### Uw gegevensstroom bijwerken

Werk de details van uw gegevensstroom bij, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen door een PATCH verzoek aan het `/flows` eindpunt van [!DNL Flow Service] API te richten, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-verzoek indient, moet u de unieke `etag` gegevens van uw gegevensstroom opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [ het bijwerken bronnen dataflows gebruikend API ](../../update-dataflows.md).

### Uw account bijwerken

Werk de naam, beschrijving en gegevens van uw bronaccount bij door een PATCH-aanvraag uit te voeren naar de [!DNL Flow Service] API en uw basis-verbindings-id op te geven als een queryparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` van uw bronaccount opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [ het bijwerken van uw bronrekening gebruikend API ](../../update.md).

### Uw gegevensstroom verwijderen

Verwijder de gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API en de id op te geven van de gegevensstroom die u wilt verwijderen als onderdeel van de queryparameter. Voor volledige API voorbeelden, lees de gids op [ schrappend uw dataflows gebruikend API ](../../delete-dataflows.md).

### Uw account verwijderen

Verwijder uw account door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de basis verbinding-id opgeeft van het account dat u wilt verwijderen. Voor volledige API voorbeelden, lees de gids bij [ het schrappen van uw bronrekening gebruikend API ](../../delete.md).