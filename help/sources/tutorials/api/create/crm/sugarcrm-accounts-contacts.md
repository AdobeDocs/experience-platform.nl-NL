---
title: Een bronverbinding en gegevensstroom maken voor SugarCRM-accounts en -contactpersonen met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met SugarCRM-accounts en -contactpersonen met behulp van de Flow Service API.
exl-id: 2b422b39-5b86-4313-a214-725044d9812c
source-git-commit: 0edc7a6a68ee4dc5ea24f16a8bc12aba85af0dff
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL SugarCRM Accounts & Contacts] met de Flow Service API

Het volgende leerprogramma begeleidt u door de stappen om een [!DNL SugarCRM Accounts & Contacts] bronverbinding tot stand te brengen en een dataflow tot stand te brengen om [[!DNL SugarCRM] ](https://www.sugarcrm.com/) rekeningen en contactgegevens aan Adobe Experience Platform te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL SugarCRM] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u [!DNL SugarCRM Accounts & Contacts] wilt verbinden met Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `host` | Het SugarCRM API eindpunt de bron verbindt met. | `developer.salesfusion.com` |
| `username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. | `123456789` |

## Verbinding maken [!DNL SugarCRM Accounts & Contacts] met platform met behulp van de [!DNL Flow Service] API

In het volgende voorbeeld worden de stappen beschreven die u moet uitvoeren om de [!DNL SugarCRM] -bron te verifiëren, een bronverbinding te maken en een gegevensstroom te maken om uw accounts en contactgegevens naar het Experience Platform te brengen.

### Een basisverbinding maken {#base-connection}

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL SugarCRM Accounts & Contacts] -verificatiegegevens op als onderdeel van de aanvraaginstantie.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL SugarCRM Accounts & Contacts] gemaakt:

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
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat de bron is geregistreerd en goedgekeurd via de API van [!DNL Flow Service] . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verifiëren bij Platform. |
| `auth.params.host` | De SugarCRM API gastheer: *developer.salesfusion.com* |
| `auth.params.username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. |
| `auth.params.password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Ontdek uw bron {#explore}

Met de id van de basisverbinding die u in de vorige stap hebt gegenereerd, kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren.
Gebruik de volgende vraag om de weg van het dossier te vinden u in Platform wilt brengen:

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Wanneer het uitvoeren van GET verzoeken om de het dossierstructuur en inhoud van uw bron te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder vermeld zijn:


| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `objectType=rest` | Het type object dat u wilt verkennen. Deze waarde is momenteel altijd ingesteld op `rest` . |
| `{OBJECT}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. Voor deze bron zou de waarde `json` zijn. |
| `fileType=json` | Het bestandstype van het bestand dat u naar Platform wilt verzenden. Momenteel is `json` het enige ondersteunde bestandstype. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Bepaalt parameters voor het brondossier u aan Platform wilt brengen. Als u het geaccepteerde indelingstype voor `{SOURCE_PARAMS}` wilt ophalen, moet u de gehele tekenreeks coderen in base64. <br> [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt, geeft u een van de volgende waarden door: <ul><li>`accounts` : bedrijven met wie uw organisatie een relatie heeft.</li><li>`contacts` : Individuele personen met wie uw organisatie een vaste relatie heeft.</li></ul> |

De [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt voor het verzenden van de aanvraag, ziet u als volgt:

**Verzoek**

>[!BEGINTABS]

>[!TAB  Rekeningen ]

Voor de [!DNL SugarCRM] Accounts-API wordt de waarde voor `{SOURCE_PARAMS}` doorgegeven als `{"object_type":"accounts"}` . Wanneer gecodeerd in base64, komt deze overeen met `eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=` zoals hieronder weergegeven.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB  Contacten ]

Voor de [!DNL SugarCRM] Contactpersonen-API wordt de waarde voor `{SOURCE_PARAMS}` doorgegeven als `{"object_type":"contacts"}` . Wanneer gecodeerd in base64 komt deze overeen met `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=` zoals hieronder weergegeven.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**Reactie**

En afhankelijk van welk objecttype u de ontvangen reactie leveraging is de volgende tabel:

>[!NOTE]
>
>Sommige records zijn afgekapt om een betere presentatie mogelijk te maken.

>[!BEGINTABS]

>[!TAB  Rekeningen ]

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

>[!TAB  Contacten ]

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

U kunt een bronverbinding maken door een aanvraag voor een POST in te dienen bij de [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

**API formaat**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL SugarCRM Accounts & Contacts] :

Afhankelijk van het objecttype dat u gebruikt, selecteert u een van de volgende tabbladen:

>[!BEGINTABS]

>[!TAB  Rekeningen ]

Voor de API voor [!DNL SugarCRM] Accounts moet de waarde van de `object_type` -eigenschap `accounts` zijn.

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

>[!TAB  Contacten ]

Voor de [!DNL SugarCRM] Contactpersonen-API moet de waarde van de eigenschap `object_type` `contacts` zijn.

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
| `data.format` | De indeling van de [!DNL SugarCRM Accounts & Contacts] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |
| `object_type` | [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Afhankelijk van het objecttype dat u gebruikt, geeft u een van de volgende waarden door: <ul><li>`accounts` : bedrijven met wie uw organisatie een relatie heeft.</li><li>`contacts` : Individuele personen met wie uw organisatie een vaste relatie heeft.</li></ul> |
| `path` | Dit heeft dezelfde waarde die u voor *`object_type`* selecteert. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

### Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan de [ Registratie API van het Schema ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan de [ Dienst API van de Catalogus uit te voeren ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding met de bestemming waar de ingesloten gegevens moeten worden opgeslagen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart van de verbindingsspecificatie verstrekken die aan het gegevens meer beantwoordt. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het gegevensmeer. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding voor [!DNL SugarCRM Accounts & Contacts] gemaakt:

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
| `connectionSpec.id` | De id van de verbindingsspecificatie die correspondeert met data Lake. Deze vaste id is: `6b137bf6-d2a0-48c8-914b-d50f4942eb85` . |
| `data.format` | De indeling van de [!DNL SugarCRM Accounts & Contacts] -gegevens die u wilt invoeren. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "6b137bf6-d2a0-48c8-914b-d50f4942eb85",
    "etag": "\"8405a268-0000-0200-0000-6368b8c30000\""
}
```

### Een toewijzing maken {#mapping}

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
| `outputSchema.schemaRef.id` | Identiteitskaart van het [ doelXDM- schema ](#target-schema) in een vroegere stap wordt geproduceerd. |
| `mappings.sourceType` | Het bronkenmerktype dat wordt toegewezen. |
| `mappings.source` | Het bronkenmerk dat moet worden toegewezen aan een XDM-doelpad. |
| `mappings.destination` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

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

De laatste stap op weg naar het verzenden van gegevens van [!DNL SugarCRM Accounts & Contacts] naar Platform is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Source-verbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op `hour` of `day` . De intervalwaarde geeft de periode tussen twee opeenvolgende indelingen aan. De intervalwaarde moet worden ingesteld op `1` of `24` afhankelijk van `scheduleParams.frequency` de selectie van `hour` of `day` .

**API formaat**

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
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste id is: `6499120c-0b15-42dc-936e-847ea3c24d72` . |
| `flowSpec.version` | De corresponderende versie van de specificatie-id voor de stroom. Deze waarde is standaard ingesteld op `1.0` . |
| `sourceConnectionIds` | [ bron verbindingsidentiteitskaart ](#source-connection) die in een vroegere stap wordt geproduceerd. |
| `targetConnectionIds` | De [ identiteitskaart van de doelverbinding ](#target-connection) die in een vroegere stap wordt geproduceerd. |
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt geproduceerd. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde is standaard ingesteld op `0` . |
| `scheduleParams.startTime` | This property contains information on the ingestion Scheduling of the dataflow. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `hour` of `day` . |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. De intervalwaarde moet worden ingesteld op `1` of `24` afhankelijk van `scheduleParams.frequency` de selectie van `hour` of `day` . |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## Bijlage

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor volledige API voorbeelden, lees de gids op [ controlerend uw brongegevens gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uw gegevensstroom bijwerken

Werk de details van uw gegevensstroom bij, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen door een PATCH verzoek aan het `/flows` eindpunt van [!DNL Flow Service] API te richten, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-verzoek indient, moet u de unieke `etag` gegevens van uw gegevensstroom opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [ het bijwerken bronnen dataflows gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uw account bijwerken

Werk de naam, beschrijving en gegevens van uw bronaccount bij door een PATCH-aanvraag uit te voeren naar de [!DNL Flow Service] API en uw basis-verbindings-id op te geven als een queryparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` van uw bronaccount opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [ het bijwerken van uw bronrekening gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Uw gegevensstroom verwijderen

Verwijder de gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API en de id op te geven van de gegevensstroom die u wilt verwijderen als onderdeel van de queryparameter. Voor volledige API voorbeelden, lees de gids op [ schrappend uw dataflows gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Uw account verwijderen

Verwijder uw account door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de basis verbinding-id opgeeft van het account dat u wilt verwijderen. Voor volledige API voorbeelden, lees de gids bij [ het schrappen van uw bronrekening gebruikend API ](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
