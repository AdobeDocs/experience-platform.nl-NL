---
title: Een bronverbinding en gegevensstroom maken voor SugarCRM-accounts en -contactpersonen met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met SugarCRM-accounts en -contactpersonen met behulp van de Flow Service API.
exl-id: 2b422b39-5b86-4313-a214-725044d9812c
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2160'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL SugarCRM Accounts & Contacts] de Flow Service API gebruiken

De volgende zelfstudie begeleidt u door de stappen om een [!DNL SugarCRM Accounts & Contacts] bronverbinding en een gegevensstroom maken om [[!DNL SugarCRM]](https://www.sugarcrm.com/) accounts en contactpersonen aan Adobe Experience Platform met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL SugarCRM] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL SugarCRM Accounts & Contacts] aan Platform, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `host` | Het SugarCRM API eindpunt de bron verbindt met. | `developer.salesfusion.com` |
| `username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. | `123456789` |

## Verbinden [!DNL SugarCRM Accounts & Contacts] naar Platform met de [!DNL Flow Service] API

Hieronder worden de stappen beschreven die u moet uitvoeren om uw [!DNL SugarCRM] bron, creeer een bronverbinding, en creeer een gegevensstroom om uw rekeningen en contactgegevens aan Experience Platform te brengen.

### Een basisverbinding maken {#base-connection}

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL SugarCRM Accounts & Contacts] verificatiegegevens als onderdeel van de aanvraaginstantie.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL SugarCRM Accounts & Contacts]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Accounts & Contacts base connection",
      "description": "Create a live inbound connection to your SugarCRM Accounts & Contacts instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over uw basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat de bron is geregistreerd en goedgekeurd via het [!DNL Flow Service] API. |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verifiëren bij Platform. |
| `auth.params.host` | De SugarCRM API-host: *developer.salesfusion.com* |
| `auth.params.username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. |
| `auth.params.password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Ontdek uw bron {#explore}

Met de id van de basisverbinding die u in de vorige stap hebt gegenereerd, kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren.
Gebruik de volgende vraag om de weg van het dossier te vinden u in Platform wilt brengen:

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Wanneer het uitvoeren van GET verzoeken om de het dossierstructuur en inhoud van uw bron te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder vermeld zijn:


| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `objectType=rest` | Het type object dat u wilt verkennen. Deze waarde is momenteel altijd ingesteld op `rest`. |
| `{OBJECT}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. Voor deze bron zou de waarde `json`. |
| `fileType=json` | Het bestandstype van het bestand dat u naar Platform wilt verzenden. Momenteel `json` is het enige ondersteunde bestandstype. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Bepaalt parameters voor het brondossier u aan Platform wilt brengen. Het geaccepteerde indelingstype ophalen voor `{SOURCE_PARAMS}`, moet u het volledige koord in base64 coderen. <br> [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt, geeft u een van de volgende waarden door: <ul><li>`accounts` : Bedrijven met wie uw organisatie een relatie heeft.</li><li>`contacts` : Individuele personen met wie uw organisatie een vaste relatie heeft.</li></ul> |

De [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt voor het verzenden van de aanvraag, ziet u als volgt:

**Verzoek**

>[!BEGINTABS]

>[!TAB Accounts]

Voor [!DNL SugarCRM] Accounts-API de waarde voor `{SOURCE_PARAMS}` wordt doorgegeven als `{"object_type":"accounts"}`. Wanneer gecodeerd in base64, komt deze overeen met `eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=` zoals hieronder weergegeven.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB Contactpersonen]

Voor [!DNL SugarCRM] Contacteert API de waarde voor `{SOURCE_PARAMS}` wordt doorgegeven als `{"object_type":"contacts"}`. Wanneer gecodeerd in base64 staat deze gelijk aan `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=` zoals hieronder weergegeven.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**Antwoord**

En afhankelijk van welk objecttype u de ontvangen reactie leveraging is de volgende tabel:

>[!NOTE]
>
>Sommige records zijn afgekapt om een betere presentatie mogelijk te maken.

>[!BEGINTABS]

>[!TAB Accounts]

Een geslaagde reactie retourneert een structuur zoals hieronder.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "key_account": {
                        "type": "boolean"
                    },
                    "owner_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "billing_city": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "account_name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account_score": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
                    },
                    "contacts": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 1,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/1/",
                "account_name": "No Company",
                "owner_id": 1,
                "owner": "https://developer.salesfusion.com/api/2.0/users/1/",
                "created_date": "2022-06-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "updated_date": "2019-08-29T15:18:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/1/contacts/",
                "created_by_id": 1,
                "updated_by_id": 1,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 2,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/2/",
                "account_name": "360 Vacations",
                "owner_id": 45,
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "phone": "+1 - 384 - 735 - 3844",
                "created_date": "2022-09-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "billing_city": "New York City",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/2/contacts/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 50,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/50/",
                "account_name": "Waverly Trading House",
                "owner_id": 40,
                "owner": "https://developer.salesfusion.com/api/2.0/users/40/",
                "phone": "+1 - 964 - 226 - 4552",
                "created_date": "2022-09-18T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "billing_city": "Minneapolis",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/50/contacts/",
                "created_by_id": 40,
                "updated_by_id": 40,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        }
    ]
}
```

>[!TAB Contactpersonen]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "opt_out": {
                        "type": "string"
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "contact_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "title": {
                        "type": "string"
                    },
                    "deleted_date": {},
                    "contact": {
                        "type": "string"
                    },
                    "account_name": {
                        "type": "string"
                    },
                    "first_name": {
                        "type": "string"
                    },
                    "del_date": {},
                    "email": {
                        "type": "string"
                    },
                    "delivered_date": {},
                    "owner": {
                        "type": "string"
                    },
                    "owner_name": {
                        "type": "string"
                    },
                    "last_name": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "opt_out_date": {},
                    "phone": {
                        "type": "string"
                    },
                    "crm_id": {
                        "type": "string"
                    },
                    "crm_type": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "deliverability_status": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "deliverability_message": {},
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 1,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/1/",
                "first_name": "Cynthia",
                "last_name": "Rose",
                "phone": "+1 - 000 - 000 - 000",
                "email": "test.user@hotmail.com",
                "account_id": 10,
                "account_name": "Sunyvale Reporting Ltd",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/10/",
                "owner_name": "Sarah Smith",
                "owner": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_date": "2022-06-23T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_by_id": 41,
                "updated_by_id": 41,
                "crm_id": "f53c3982-84ea-11ec-874a-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "Assigned",
                "title": "Director Operations",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 2,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/2/",
                "email": "test.user@outlook.com",
                "created_date": "2022-06-21T23:35:00Z",
                "updated_date": "2022-02-03T21:55:00Z",
                "opt_out": "N",
                "crm_type": "Contact",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 3,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/3/",
                "first_name": "Jonathan",
                "last_name": "Ryan",
                "phone": "+1 - 000 - 000 - 0000",
                "email": "test.user@yahoo.com",
                "account_id": 52,
                "account_name": "Q3 ARVRO III PR",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/52/",
                "owner_name": "Max Jensen",
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_date": "2022-07-02T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "crm_id": "f54a1840-84ea-11ec-9546-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "New",
                "title": "Director Sales",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
    ]
}
```

>[!ENDTABS]

### Een bronverbinding maken {#source-connection}

U kunt een bronverbinding tot stand brengen door een verzoek van de POST aan [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

**API-indeling**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL SugarCRM Accounts & Contacts]:

Afhankelijk van het objecttype dat u gebruikt, selecteert u een van de volgende tabbladen:

>[!BEGINTABS]

>[!TAB Accounts]

Voor [!DNL SugarCRM] Accounts-API `object_type` eigenschapswaarde moet `accounts`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "accounts",
          "path": "accounts"
      }
  }'
```

>[!TAB Contactpersonen]

Voor [!DNL SugarCRM] Contactpersoon API `object_type` eigenschapswaarde moet `contacts`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts",
          "path": "contacts"
      }
  }'
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van [!DNL SugarCRM Accounts & Contacts]. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met uw bron. |
| `data.format` | Het formaat van de [!DNL SugarCRM Accounts & Contacts] gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `object_type` | [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt, geeft u een van de volgende waarden door: <ul><li>`accounts` : Bedrijven met wie uw organisatie een relatie heeft.</li><li>`contacts` : Individuele personen met wie uw organisatie een vaste relatie heeft.</li></ul> |
| `path` | Dit heeft dezelfde waarde als waarvoor u selecteert *`object_type`*. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

### Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan tot stand worden gebracht door een POST verzoek aan te voeren [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan tot stand worden gebracht door een verzoek van de POST aan [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), op voorwaarde dat de id van het doelschema zich binnen de payload bevindt.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met de API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding met de bestemming waar de ingesloten gegevens moeten worden opgeslagen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart van de verbindingsspecificatie verstrekken die aan het gegevens meer beantwoordt. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het gegevensmeer. Met deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding gemaakt voor [!DNL SugarCRM Accounts & Contacts]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de doelverbinding. Zorg ervoor dat de naam van uw doelverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw doelverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De id van de verbindingsspecificatie die correspondeert met data Lake. Deze vaste ID is: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | Het formaat van de [!DNL SugarCRM Accounts & Contacts] gegevens die u wilt invoeren. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id van de nieuwe doelverbinding (`id`). Deze id is vereist in latere stappen.

```json
{
    "id": "6b137bf6-d2a0-48c8-914b-d50f4942eb85",
    "etag": "\"8405a268-0000-0200-0000-6368b8c30000\""
}
```

### Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een verzoek van de POST uit te voeren aan [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen die zijn gedefinieerd in de payload van het verzoek.

**API-indeling**

```http
POST /conversion/mappingSets
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account",
          "destination": "_extconndev.account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_id",
          "destination": "_extconndev.account_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.acount_name",
          "destination": "_extconndev.account_name"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_score",
          "destination": "_extconndev.account_score"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.billing_city",
          "destination": "_extconndev.billing_city"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.contacts",
          "destination": "_extconndev.contacts"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.custom_score_field",
          "destination": "_extconndev.custom_score_field"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.key_account",
          "destination": "_extconndev.key_account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner",
          "destination": "_extconndev.owner"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner_id",
          "destination": "_extconndev.owner_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.phone",
          "destination": "_extconndev.phone_no"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      }
      ]
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `outputSchema.schemaRef.id` | De id van de [doel-XDM-schema](#target-schema) gegenereerd in een eerdere stap. |
| `mappings.sourceType` | Het bronkenmerktype dat wordt toegewezen. |
| `mappings.source` | Het bronkenmerk dat moet worden toegewezen aan een XDM-doelpad. |
| `mappings.destination` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing inclusief de unieke id (`id`). Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Een flow maken {#flow}

De laatste stap op weg naar het verzamelen van gegevens van [!DNL SugarCRM Accounts & Contacts] aan Platform moet een gegevensstroom creëren. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van `hour` of `day`. De intervalwaarde geeft de periode tussen twee opeenvolgende indelingen aan. Interval moet worden ingesteld als `1` of `24` afhankelijk van `scheduleParams.frequency` selectie van `hour` of `day`.

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
      ],
      "targetConnectionIds": [
          "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw gegevensstroom. Zorg ervoor dat de naam van uw gegevensstroom beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw gegevensstroom omhoog te kijken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over uw gegevensstroom. |
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste ID is: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | De corresponderende versie van de specificatie-id voor de stroom. Deze waarde wordt standaard ingesteld op `1.0`. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source-connection) gegenereerd in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target-connection) gegenereerd in een eerdere stap. |
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) gegenereerd in een eerdere stap. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde wordt standaard ingesteld op `0`. |
| `scheduleParams.startTime` | This property contains information on the ingestion Scheduling of the dataflow. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `hour` of `day`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval moet worden ingesteld als `1` of `24` afhankelijk van `scheduleParams.frequency` selectie van `hour` of `day`. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## Bijlage

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Lees de handleiding voor volledige API-voorbeelden op [de gegevensstroom van uw bronnen controleren met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uw gegevensstroom bijwerken

Werk de details van uw dataflow, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen bij door een verzoek van de PATCH aan het `/flows` eindpunt van [!DNL Flow Service] API, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-verzoek indient, moet u de unieke gegevens van uw gegevensstroom opgeven `etag` in de `If-Match` header. Lees de handleiding voor volledige API-voorbeelden op [bronnen bijwerken met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uw account bijwerken

Werk de naam, beschrijving en referenties van uw bronaccount bij door een PATCH-verzoek uit te voeren naar de [!DNL Flow Service] API terwijl het verstrekken van uw identiteitskaart van de basisverbinding als vraagparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke bronaccount opgeven `etag` in de `If-Match` header. Lees de handleiding voor volledige API-voorbeelden op [het bijwerken van uw bronrekening gebruikend API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Uw gegevensstroom verwijderen

Verwijder de gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl het verstrekken van identiteitskaart van dataflow wilt u als deel van de vraagparameter schrappen. Lees de handleiding voor volledige API-voorbeelden op [verwijderen, gegevensstromen met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Uw account verwijderen

Uw account verwijderen door een DELETE-verzoek uit te voeren aan de [!DNL Flow Service] API terwijl het verstrekken van de identiteitskaart van de basisverbinding van de rekening u wilt schrappen. Lees de handleiding voor volledige API-voorbeelden op [verwijderen van uw bronaccount met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
