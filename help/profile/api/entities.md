---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Entiteiten (Profile Access) API-eindpunt
topic-legacy: guide
type: Documentation
description: Met Adobe Experience Platform hebt u toegang tot gegevens van het profiel Real-time klanten met behulp van RESTful-API's of de gebruikersinterface. In deze handleiding wordt beschreven hoe u met behulp van de profiel-API toegang krijgt tot entiteiten, beter bekend als "profielen".
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 0%

---

# Het eindpunt van entiteiten (de toegang van het Profiel)

Adobe Experience Platform biedt toegang tot [!DNL Real-time Customer Profile] gegevens die RESTful APIs of het gebruikersinterface gebruiken. In deze handleiding wordt beschreven hoe u met de API toegang krijgt tot entiteiten die beter bekend staan als &quot;profielen&quot;. Voor meer informatie over het gebruik van profielen via het dialoogvenster [!DNL Platform] UI, gelieve te verwijzen naar [Gebruikershandleiding voor profielen](../ui/user-guide.md).

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Profielgegevens benaderen op identiteit

U hebt toegang tot een [!DNL Profile] door een verzoek tot GET aan de `/access/entities` eindpunt en het verstrekken van de identiteit van de entiteit als reeks vraagparameters. Deze identiteit bestaat uit een ID-waarde (`entityId`) en de naamruimte van de identiteit (`entityIdNS`).

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in [queryparameters](#query-parameters) het aanhangsel.

**API-indeling**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Verzoek**

Met het volgende verzoek worden de e-mail en de naam van een klant opgehaald aan de hand van een identiteit:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>
>Als een verwante grafiek meer dan 50 identiteiten verbindt, zal deze dienst status 422 van HTTP en het bericht &quot;Te veel verwante identiteiten&quot;terugkeren. Als deze fout optreedt, kunt u wellicht meer queryparameters toevoegen om uw zoekopdracht te beperken.

## Profielgegevens benaderen op basis van lijst met identiteiten

U kunt meerdere profielentiteiten benaderen door een POST aan te vragen bij de `/access/entities` en het verstrekken van de identiteiten in de lading. Deze identiteiten bestaan uit een ID-waarde (`entityId`) en een naamruimte voor identiteit (`entityIdNS`).

**API-indeling**

```http
POST /access/entities
```

**Verzoek**

Met het volgende verzoek worden de namen en e-mailadressen van verschillende klanten opgehaald op basis van een lijst met identiteiten:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `schema.name` | ***(Vereist)*** De naam van het XDM-schema waartoe de entiteit behoort. |
| `fields` | De XDM-velden die moeten worden geretourneerd, als een array van tekenreeksen. Standaard worden alle velden geretourneerd. |
| `identities` | ***(Vereist)*** Een array met een lijst met identiteiten voor de entiteiten waartoe u toegang wilt hebben. |
| `identities.entityId` | De id van een entiteit waartoe u toegang wilt hebben. |
| `identities.entityIdNS.code` | De naamruimte van een entiteit-id waartoe u toegang wilt hebben. |
| `timeFilter.startTime` | Begintijd van het tijdbereikfilter, inclusief. Moet op milliseconde granularity zijn. De standaardinstelling is, indien deze niet wordt opgegeven, het begin van de beschikbare tijd. |
| `timeFilter.endTime` | Eindtijd van tijdbereikfilter, uitgesloten. Moet op milliseconde granularity zijn. De standaardinstelling (indien niet opgegeven) is het einde van de beschikbare tijd. |
| `limit` | Aantal records dat moet worden geretourneerd. Alleen van toepassing op het aantal geretourneerde ervaringsgebeurtenissen. Standaard: 1.000. |
| `orderby` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` waarbij de standaardwaarde wordt `+timestamp`. |
| `withCA` | De vlag van de eigenschap voor het toelaten van gegevens verwerkte attributen voor raadpleging. Standaard: false. |

**Antwoord**
Een succesvol antwoord retourneert de gevraagde velden met entiteiten die in de aanvraaginstantie zijn opgegeven.

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## De gebeurtenissen van de tijdreeks van de toegang voor een profiel door identiteit

U kunt tot de gebeurtenissen van de tijdreeks door de identiteit van hun bijbehorende profielentiteit toegang hebben door een verzoek van de GET tot te richten `/access/entities` eindpunt. Deze identiteit bestaat uit een ID-waarde (`entityId`) en een naamruimte voor identiteit (`entityIdNS`).

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in [queryparameters](#query-parameters) het aanhangsel.

**API-indeling**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Verzoek**

Met het volgende verzoek wordt een profielentiteit gevonden op ID en worden de waarden voor de eigenschappen opgehaald `endUserIDs`, `web`, en `channel` voor alle aan de entiteit gerelateerde tijdreeksgebeurtenissen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een gepagineerde lijst van de gebeurtenissen van de tijdreeks en bijbehorende gebieden terug die in de parameters van de verzoekvraag werden gespecificeerd.

>[!NOTE]
>
>In het verzoek is een limiet van één opgegeven (`limit=1`), `count` in de onderstaande reactie is 1 en wordt slechts één entiteit geretourneerd.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Een volgende pagina met resultaten openen

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s van resultaten zijn, `_page.next` eigenschap zal een id bevatten. Daarnaast worden de `_links.next.href` eigenschap biedt een aanvraag-URI voor het ophalen van de volgende pagina. Om de resultaten terug te winnen, doe een ander verzoek van de GET aan `/access/entities` eindpunt, nochtans moet u zeker zijn vervangen `/entities` met de waarde van de opgegeven URI.

>[!NOTE]
>
>Zorg ervoor dat u niet per ongeluk herhaalt `/entities/` in het aanvraagpad. Het mag slechts eenmaal voorkomen, `/access/entities?start=...`

**API-indeling**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschrijving |
|---|---|
| `{NEXT_URI}` | De URI-waarde is overgenomen van `_links.next.href`. |

**Verzoek**

Met het volgende verzoek wordt de volgende resultatenpagina opgehaald met de `_links.next.href` URI als aanvraagpad.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende pagina met resultaten wordt als resultaat gegeven. Dit antwoord bevat geen volgende pagina&#39;s met resultaten, zoals wordt aangegeven door de lege tekenreekswaarden van `_page.next` en `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Gebeurtenissen in tijdreeksen benaderen voor meerdere profielen op basis van identiteit

U kunt tot de gebeurtenissen van de tijdreeks van veelvoudige bijbehorende profielen toegang hebben door een POST te verzoeken aan `/access/entities` en het verstrekken van de profielidentiteiten in de lading. Deze identiteiten bestaan elk uit een ID-waarde (`entityId`) en een naamruimte voor identiteit (`entityIdNS`).

**API-indeling**

```http
POST /access/entities
```

**Verzoek**

Met het volgende verzoek worden gebruikers-id&#39;s, lokale tijden en landcodes opgehaald voor tijdreeksgebeurtenissen die zijn gekoppeld aan een lijst met profiel-id&#39;s:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Eigenschap | Beschrijving |
|---|---|
| `schema.name` | **(VEREIST)** Het XDM-schema van de op te halen entiteit |
| `relatedSchema.name` | Indien `schema.name` is `_xdm.context.experienceevent` deze waarde moet het schema opgeven voor de profielentiteit waarop de tijdreeksgebeurtenissen betrekking hebben. |
| `identities` | **(VEREIST)** Een array met profielen waaruit de bijbehorende tijdreeksgebeurtenissen moeten worden opgehaald. Elke ingang in de serie wordt geplaatst op één van twee manieren: 1) gebruiken van een volledig gekwalificeerde identiteit die uit de waarde van identiteitskaart en namespace of 2) het verstrekken van een XID bestaat. |
| `fields` | Hiermee worden de gegevens die naar een opgegeven set velden worden geretourneerd, geïsoleerd. Hiermee kunt u filteren welke schemavelden worden opgenomen in opgehaalde gegevens. Voorbeeld: persoonlijke e-mail,persoon.naam,persoon.geslacht |
| `mergePolicyId` | Hiermee wordt het samenvoegingsbeleid aangegeven waarmee de geretourneerde gegevens moeten worden beheerd. Als niet in de de dienstvraag wordt gespecificeerd, zal het gebrek van uw organisatie voor dat schema worden gebruikt. Als er geen standaardbeleid voor samenvoegen is geconfigureerd, bestaat de standaardinstelling uit geen profielsamenvoeging en geen identiteitsstitching. |
| `orderby` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` waarbij de standaardwaarde wordt `+timestamp`. |
| `timeFilter.startTime` | Geef de begintijd op voor het filteren van tijdreeksobjecten (in milliseconden). |
| `timeFilter.endTime` | Geef de eindtijd op voor het filteren van tijdreeksobjecten (in milliseconden). |
| `limit` | Numerieke waarde die het maximumaantal objecten aangeeft dat moet worden geretourneerd. Standaard: 1000 |
| `withCA` | De vlag van de eigenschap voor het toelaten van gegevens verwerkte attributen voor raadpleging. Standaard: false |

**Antwoord**

Een geslaagde reactie retourneert een gepagineerde lijst met gebeurtenissen uit de tijdreeks die zijn gekoppeld aan de meerdere profielen die in de aanvraag zijn opgegeven.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

In dit voorbeeldantwoord biedt het eerste weergegeven profiel (&quot;GkouAW-yD9aoRCPhRYROJ-TextAFW&quot;) een waarde voor `_links.next.payload`, wat betekent dat er extra resultatenpagina&#39;s zijn voor dit profiel. Zie de volgende sectie over [toegang tot aanvullende resultaten](#access-additional-results) voor meer informatie over de toegang tot deze aanvullende resultaten.

### Toegang tot extra resultaten {#access-additional-results}

Wanneer het terugwinnen van de gebeurtenissen van de tijdreeks kan er vele resultaten zijn die, daarom worden teruggekeerd vaak gepagineerd de resultaten. Als er volgende pagina&#39;s met resultaten voor een bepaald profiel zijn, kunt u `_links.next.payload` De waarde voor dat profiel bevat een object payload.

Gebruikend deze nuttige lading in het verzoeklichaam, kunt u een extra verzoek van de POST aan `access/entities` eindpunt om de verdere pagina van tijdreeksgegevens voor dat profiel terug te winnen.

## De gebeurtenissen van de tijdreeks van de toegang in veelvoudige schemaentiteiten

U kunt toegang krijgen tot meerdere entiteiten die via een relatiebeschrijving zijn verbonden. De volgende voorbeeld API vraag veronderstelt een verhouding reeds tussen twee schema&#39;s is bepaald. Voor meer informatie over relatiebeschrijvers, gelieve te lezen [!DNL Schema Registry] Handleiding voor API-ontwikkelaars [eindhulplijn descriptorpunt](../../xdm/api/descriptors.md).

U kunt queryparameters opnemen in het aanvraagpad om op te geven tot welke gegevens u toegang wilt krijgen. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in [queryparameters](#query-parameters) het aanhangsel.

**API-indeling**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Verzoek**

Het volgende verzoek wint een entiteit terug die een eerder gevestigde relatiebeschrijver bevat om tot informatie over verschillende schema&#39;s toegang te hebben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwoord**

Een geslaagde reactie retourneert een gepagineerde lijst met gebeurtenissen uit de tijdreeks die aan de meerdere entiteiten zijn gekoppeld.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Een volgende pagina met resultaten openen

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s van resultaten zijn, `_page.next` eigenschap zal een id bevatten. Daarnaast worden de `_links.next.href` eigenschap biedt een aanvraag-URI voor het ophalen van de volgende pagina door aanvullende GET-aanvragen in te dienen bij de `access/entities` eindpunt.

## Volgende stappen

Door deze handleiding te volgen, hebt u toegang tot [!DNL Real-time Customer Profile] gegevensvelden, profielen en tijdreeksgegevens. Leren hoe u toegang krijgt tot andere gegevensbronnen die zijn opgeslagen in [!DNL Platform], zie de [Overzicht van gegevenstoegang](../../data-access/home.md).

## Aanhangsel {#appendix}

De volgende sectie verstrekt aanvullende informatie betreffende de toegang tot van [!DNL Profile] gegevens die de API gebruiken.

### Parameters query {#query-parameters}

De volgende parameters worden gebruikt in het pad voor verzoeken van de GET aan de `/access/entities` eindpunt. Ze dienen om de profielentiteit te identificeren die u wilt benaderen en de gegevens te filteren die in de reactie worden geretourneerd. De vereiste parameters worden geëtiketteerd, terwijl de rest facultatief is.

| Parameter | Beschrijving | Voorbeeld |
|---|---|---|
| `schema.name` | **(VEREIST)** Het XDM-schema van de op te halen entiteit | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Indien `schema.name` is &quot;_xdm.context.experienceEvent&quot;, moet deze waarde het schema opgeven voor de profielentiteit waaraan de tijdreeksgebeurtenissen gerelateerd zijn. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(VEREIST)** De id van de entiteit. Als de waarde van deze parameter geen XID is, moet ook een naamruimteparameter voor identiteit worden opgegeven (zie `entityIdNS` hieronder). | `entityId=janedoe@example.com` |
| `entityIdNS` | Indien `entityId` wordt niet opgegeven als een XID, moet in dit veld de naamruimte van de identiteit worden opgegeven. | `entityIdNE=email` |
| `relatedEntityId` | Indien `schema.name` is &quot;_xdm.context.ExperienceEvent&quot;, moet deze waarde de naamruimte van de gerelateerde profielentiteit opgeven. Deze waarde volgt dezelfde regels als `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Indien `schema.name` is &quot;_xdm.context.experienceEvent&quot;, moet deze waarde de naamruimte van de identiteit opgeven voor de entiteit die is opgegeven in `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtert de gegevens die in de reactie worden geretourneerd. Gebruik dit om te specificeren welke schemagebiedwaarden in opgehaalde gegevens moeten omvatten. Voor meerdere velden scheidt u waarden met een komma zonder spaties tussen | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Hiermee wordt het samenvoegingsbeleid aangegeven waarmee de geretourneerde gegevens moeten worden beheerd. Als niet in de vraag wordt gespecificeerd, zal het gebrek van uw organisatie voor dat schema worden gebruikt. Als er geen standaardbeleid voor samenvoegen is geconfigureerd, bestaat de standaardinstelling uit geen profielsamenvoeging en geen identiteitsstitching. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` waarbij de standaardwaarde wordt `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Geef de begintijd op voor het filteren van tijdreeksobjecten (in milliseconden). | `startTime=1539838505` |
| `endTime` | Geef de eindtijd op voor het filteren van tijdreeksobjecten (in milliseconden). | `endTime=1539838510` |
| `limit` | Numerieke waarde die het maximumaantal objecten aangeeft dat moet worden geretourneerd. Standaard: 1000 | `limit=100` |
| `property` | Filters op de eigenschapswaarde. Ondersteunt de volgende beoordelaars: =, !=, &lt;, &lt;=, >, >=. Kan alleen worden gebruikt met ervaringsgebeurtenissen, waarbij maximaal drie eigenschappen worden ondersteund. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | De vlag van de eigenschap voor het toelaten van gegevens verwerkte attributen voor raadpleging. Standaard: false | `withCA=true` |
