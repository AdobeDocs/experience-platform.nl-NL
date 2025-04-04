---
title: Een bronverbinding en gegevensstroom maken voor Oracle NetSuite-entiteiten met behulp van de Flow Service API
description: Leer hoe u een bronverbinding en gegevensstroom maakt om Oracle NetSuite-contactpersonen en -klantgegevens via de Flow Service API naar Experience Platform te sturen.
hide: true
hidefromtoc: true
badge: Beta
exl-id: ddbb413e-a6ca-49df-b68d-37c9d2aab61b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2177'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL Oracle NetSuite Entities] met de Flow Service API

>[!NOTE]
>
>De bron [!DNL Oracle NetSuite Entities] is in bèta. Zie het [ overzicht van bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Lees het volgende leerprogramma leren hoe te om contacten en klantengegevens van uw [!DNL Oracle NetSuite Activities Entities] rekening aan Adobe Experience Platform te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Oracle NetSuite Entities] via de [!DNL Flow Service] API.

### Verificatie

Lees het [[!DNL Oracle NetSuite]  overzicht ](../../../../connectors/marketing-automation/oracle-netsuite.md) voor informatie over hoe te om uw authentificatiegeloofsbrieven terug te winnen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Oracle NetSuite Entities]

In het volgende voorbeeld worden de stappen beschreven die u moet uitvoeren om de [!DNL Oracle NetSuite Entities] -bron te verifiëren, een bronverbinding te maken en een gegevensstroom te maken om uw klant en contactgegevens naar Experience Platform te sturen.

### Een basisverbinding maken {#base-connection}

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Oracle NetSuite Entities] -verificatiegegevens op als onderdeel van de aanvraagprocedure.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle NetSuite Entities] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Entities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over uw basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw bron. Deze id kan worden opgehaald nadat de bron is geregistreerd en goedgekeurd via de API van [!DNL Flow Service] . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verifiëren bij Experience Platform. |
| `auth.params.clientId` | De client-id-waarde wanneer u de integratierecord maakt. Het proces om een interingsverslag tot stand te brengen kan [ hier ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) worden gevonden. De waarde bestaat uit een tekenreeks van 64 tekens, vergelijkbaar met `7fce.....b42f` . |
| `auth.params.clientSecret` | De client-id-waarde wanneer u de integratierecord maakt. Het proces om een interingsverslag tot stand te brengen kan [ hier ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) worden gevonden. De waarde bestaat uit een tekenreeks van 64 tekens, vergelijkbaar met `5c98.....1b46` . |
| `auth.params.accessTokenUrl` | De [!DNL NetSuite] Access Token URL, vergelijkbaar met `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token` waar u ACCOUNT_ID vervangt door uw account-id van [!DNL NetSuite] . |
| `auth.params.accessToken` | De het symbolische waarde van de Toegang wordt geproduceerd aan het eind van [ stap twee ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint) van [ OAuth 2.0 de Stroom van de Verlening van de Code van de Vergunning ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) leerprogramma. Toegangstokens verlopen slechts 60 minuten. de waarde bestaat uit een tekenreeks van 1024 tekens die wordt opgemaakt als JSON Web Token (JWT), vergelijkbaar met `eyJr......f4V0` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### Ontdek uw bron {#explore}

Zodra u uw identiteitskaart van de basisverbinding hebt, kunt u de inhoud en de structuur van uw brongegevens nu onderzoeken door een verzoek van GET aan het `/connections` eindpunt uit te voeren terwijl het verstrekken van uw identiteitskaart van de basisverbinding als vraagparameter.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Verzoek**

Wanneer u GET-verzoeken uitvoert om de bestandsstructuur en inhoud van uw bron te verkennen, moet u de queryparameters opnemen die in de onderstaande tabel worden vermeld:

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding die in de vorige stap is gegenereerd. |
| `objectType=rest` | Het type object dat u wilt verkennen. Deze waarde is momenteel altijd ingesteld op `rest` . |
| `{OBJECT}` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. Voor deze bron zou de waarde `json` zijn. |
| `fileType=json` | Het bestandstype van het bestand dat u naar Experience Platform wilt verzenden. Momenteel is `json` het enige ondersteunde bestandstype. |
| `{PREVIEW}` | Een booleaanse waarde die definieert of de inhoud van de verbinding voorvertoning ondersteunt. |
| `{SOURCE_PARAMS}` | Definieert parameters voor het bronbestand dat u naar Experience Platform wilt brengen. Als u het geaccepteerde indelingstype voor `{SOURCE_PARAMS}` wilt ophalen, moet u de gehele tekenreeks coderen in base64. <br> [!DNL Oracle NetSuite Entities] biedt ondersteuning voor het ophalen van zowel klant- als contactgegevens. Afhankelijk van het objecttype dat u gebruikt, geeft u een van de volgende waarden door: <ul><li>`customer` : Haal specifieke klantgegevens op, zoals klantnamen, adressen en toetsidentificatoren.</li><li>`contact` : ontvang contactnamen, e-mails, telefoonnummers en eventuele aangepaste contactvelden die aan klanten zijn gekoppeld.</li></ul> |

>[!BEGINTABS]

>[!TAB  Klant ]

Voor [!DNL Oracle NetSuite Entities] wordt voor het ophalen van contactgegevens de waarde voor `{SOURCE_PARAMS}` doorgegeven als `{"object_type":"customer"}` . Wanneer gecodeerd in base64, komt deze overeen met `eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D` zoals hieronder weergegeven.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB  Contact ]

Voor [!DNL Oracle NetSuite Entities] wordt voor het ophalen van contactgegevens de waarde voor `{SOURCE_PARAMS}` doorgegeven als `{"object_type":"contact"}` . Wanneer gecodeerd in base64, komt deze overeen met `eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9` zoals hieronder weergegeven.


```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9' \
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

>[!TAB  Klant ]

Een geslaagde reactie retourneert een structuur zoals hieronder.

+++Selecteren om de JSON-payload weer te geven

```json
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "weblead": {
                        "type": "string"
                    },
                    "emailtransactions": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "dateclosed": {
                        "type": "string"
                    },
                    "entitynumber": {
                        "type": "string"
                    },
                    "emailpreference": {
                        "type": "string"
                    },
                    "creditholdoverride": {
                        "type": "string"
                    },
                    "entitystatus": {
                        "type": "string"
                    },
                    "giveaccess": {
                        "type": "string"
                    },
                    "isbudgetapproved": {
                        "type": "string"
                    },
                    "receivablesaccount": {
                        "type": "string"
                    },
                    "shippingcarrier": {
                        "type": "string"
                    },
                    "isperson": {
                        "type": "string"
                    },
                    "balancesearch": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "currency": {
                        "type": "string"
                    },
                    "overduebalancesearch": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "displaysymbol": {
                        "type": "string"
                    },
                    "searchstage": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "oncredithold": {
                        "type": "string"
                    },
                    "probability": {
                        "type": "string"
                    },
                    "faxtransactions": {
                        "type": "string"
                    },
                    "altname": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "printtransactions": {
                        "type": "string"
                    },
                    "alcoholrecipienttype": {
                        "type": "string"
                    },
                    "overridecurrencyformat": {
                        "type": "string"
                    },
                    "companyname": {
                        "type": "string"
                    },
                    "unbilledorderssearch": {
                        "type": "string"
                    },
                    "shipcomplete": {
                        "type": "string"
                    },
                    "symbolplacement": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2022-12-15",
                "datecreated": "2022-12-15",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "4",
                "entitynumber": "4",
                "entitystatus": "13",
                "entitytitle": "4 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "404",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2022-12-15",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-01-19",
                "datecreated": "2023-01-19",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "6",
                "entitynumber": "6",
                "entitystatus": "13",
                "entitytitle": "6 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "605",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-01-19",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-02-01",
                "datecreated": "2023-02-01",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "9",
                "entitynumber": "9",
                "entitystatus": "13",
                "entitytitle": "9 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "710",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-02-01",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
    ]
},
```

+++

>[!TAB  Contact ]

Een geslaagde reactie retourneert een structuur zoals hieronder.

+++Selecteren om de JSON-payload weer te geven

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "isprivate": {
                        "type": "string"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "company": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe2",
                "entitytitle": "John Doe2",
                "id": "1210",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999998"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe4",
                "entitytitle": "John Doe4",
                "id": "1212",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999996"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe6",
                "entitytitle": "John Doe6",
                "id": "1214",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999994"
            }
        },
    ]
}
```

+++

>[!ENDTABS]

### Een bronverbinding maken {#source-connection}

U kunt een bronverbinding maken door een POST-aanvraag in te dienen bij het eindpunt `/sourceConnections` van de [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

**API formaat**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL Oracle NetSuite Entities] :

>[!BEGINTABS]

>[!TAB  Klant ]

Bij het ophalen van klantgegevens moet de waarde van de eigenschap `object_type` `customer` zijn.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "customer"        
      }
  }'
```

>[!TAB  Contact ]

Bij het ophalen van contactgegevens moet de waarde van de eigenschap `object_type` `contact` zijn.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "contact"        
      }
  }'
```

>[!ENDTABS]

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van [!DNL Oracle NetSuite Entities]. Deze id is gegenereerd in een eerdere stap. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met uw bron. |
| `data.format` | De indeling van de [!DNL Oracle NetSuite Entities] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |
| `object_type` | [!DNL Oracle NetSuite Entities] ondersteunt zowel ophalen door de klant als opvragen door contact. Afhankelijk van welke entiteit u wilt, geeft u een van de volgende waarden door: <ul><li>`customer` : Haal specifieke klantgegevens op, zoals klantnamen, adressen en toetsidentificatoren.</li><li>`contact` : ontvang contactnamen, e-mails, telefoonnummers en eventuele aangepaste contactvelden die aan klanten zijn gekoppeld.</li></ul> |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### Een doel-XDM-schema maken {#target-schema}

Als u de brongegevens in Experience Platform wilt gebruiken, moet u een doelschema maken om de brongegevens naar wens te structureren. Het doelschema wordt dan gebruikt om een dataset van Experience Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een POST- verzoek aan de [ Registratie API van het Schema ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](../../../../../xdm/api/schemas.md#create-a-schema).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een POST- verzoek aan de [ Dienst API van de Catalogus uit te voeren ](https://developer.adobe.com/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](../../../../../catalog/api/create-dataset.md).

### Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding met de bestemming waar de ingesloten gegevens moeten worden opgeslagen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart verstrekken van de verbindingsspecificatie die aan het gegevens meer beantwoordt. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het gegevensmeer. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding voor [!DNL Oracle NetSuite Entities] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Target Connection Generic Rest",
      "description": " Oracle NetSuite Entities Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de doelverbinding. Zorg ervoor dat de naam van uw doelverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw doelverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De id van de verbindingsspecificatie die correspondeert met data Lake. Deze vaste id is: `6b137bf6-d2a0-48c8-914b-d50f4942eb85` . |
| `data.format` | De indeling van de [!DNL Oracle NetSuite Entities] -gegevens die u wilt invoeren. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een POST- verzoek aan [[!DNL Data Prep]  API ](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

**API formaat**

```http
POST /conversion/mappingSets
```

**Verzoek**

Met de volgende aanvraag wordt een toewijzing gemaakt voor [!DNL DNL NetSuite Entities]

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
            "source": "items.id",
            "destination": "_extconndev.NS_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.entitytitle",
            "destination": "_extconndev.NS_entity_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.datecreated",
            "destination": "_extconndev.NS_datecreated"
        },
        {
            "sourceType": "ATTRIBUTE",
            "destination": "_extconndev.NS_email",
            "source": "items.email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NS_lastmodified"
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
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Een flow maken {#flow}

De laatste stap naar het verzenden van gegevens van [!DNL Oracle NetSuite Entities] naar Experience Platform is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Source-verbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

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
    "name": "Oracle NetSuite Entities connector Flow Generic Rest",
    "description": "Oracle NetSuite Entities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
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
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Experience Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt geproduceerd. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde is standaard ingesteld op `0` . |
| `scheduleParams.startTime` | This property contains information on the ingestion Scheduling of the dataflow. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## Bijlage

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor volledige API voorbeelden, lees de gids op [ controlerend uw brongegevens gebruikend API ](../../monitor.md).

### Uw gegevensstroom bijwerken

Werk de details van uw gegevensstroom bij, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen door een PATCH- verzoek aan het `/flows` eindpunt van [!DNL Flow Service] API te doen, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` gegevens van uw gegevensstroom opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [ het bijwerken bronnen dataflows gebruikend API ](../../update-dataflows.md).

### Uw account bijwerken

Werk de naam, beschrijving en gegevens van uw bronaccount bij door een PATCH-aanvraag uit te voeren naar de [!DNL Flow Service] API en uw basis-verbindings-id op te geven als een queryparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` naam van uw bronaccount opgeven in de header van `If-Match` . Voor volledige API voorbeelden, lees de gids bij [ het bijwerken van uw bronrekening gebruikend API ](../../update.md).

### Uw gegevensstroom verwijderen

Verwijder uw gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de id opgeeft van de gegevensstroom die u wilt verwijderen als onderdeel van de queryparameter. Voor volledige API voorbeelden, lees de gids op [ schrappend uw dataflows gebruikend API ](../../delete-dataflows.md).

### Uw account verwijderen

Verwijder uw account door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de basis-verbindings-id opgeeft van het account dat u wilt verwijderen. Voor volledige API voorbeelden, lees de gids bij [ het schrappen van uw bronrekening gebruikend API ](../../delete.md).
