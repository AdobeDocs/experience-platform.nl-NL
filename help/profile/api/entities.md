---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 9600f315f162b6cd86e2dbe2fffc793cc91c9319
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---


# Entiteiten (toegang tot profiel)

Met het Adobe Experience Platform hebt u via RESTful-API&#39;s of de gebruikersinterface toegang tot gegevens van het klantprofiel in realtime. In deze handleiding wordt beschreven hoe u met de API toegang krijgt tot entiteiten die beter bekend staan als &quot;profielen&quot;. Raadpleeg de gebruikershandleiding bij [Profiel voor meer informatie over toegang tot profielgegevens via de interface van het platform](../ui/user-guide.md).

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van Real-time API van het Profiel van de Klant. Lees voordat u verdergaat de handleiding voor ontwikkelaars van de [realtime-API voor klantprofielen](getting-started.md).

Met name bevat de sectie [Aan de](getting-started.md#getting-started) slag van de handleiding voor ontwikkelaars van profielen koppelingen naar verwante onderwerpen, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar API&#39;s van het Experience Platform met succes uit te voeren.

## Profielgegevens benaderen op identiteit

U kunt tot een entiteit van het Profiel toegang hebben door een GET verzoek aan het `/access/entities` eindpunt te doen en de identiteit van de entiteit als reeks vraagparameters te verstrekken. Deze identiteit bestaat uit een ID-waarde (`entityId`) en de naamruimte voor identiteit (`entityIdNS`).

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in de sectie van [vraagparameters](#query-parameters) van bijlage.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>Als een verwante grafiek meer dan 50 identiteiten verbindt, zal deze dienst status 422 van HTTP en het bericht &quot;Te veel verwante identiteiten&quot;terugkeren. Als deze fout optreedt, kunt u wellicht meer queryparameters toevoegen om uw zoekopdracht te beperken.

## Profielgegevens benaderen op basis van lijst met identiteiten

U kunt tot veelvoudige profielentiteiten door hun identiteiten toegang hebben door een POST- verzoek aan het `/access/entities` eindpunt te richten en de identiteiten in de lading te verstrekken. Deze identiteiten bestaan uit een ID-waarde (`entityId`) en een naamruimte voor identiteit (`entityIdNS`).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `orderby` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` de standaardinstelling `+timestamp`. |
| `withCA` | De vlag van de eigenschap voor het toelaten van gegevens verwerkte attributen voor raadpleging. Standaard: false. |

**Met een geslaagde reactie** worden de gevraagde velden van entiteiten geretourneerd die in de aanvraaginstantie zijn opgegeven.

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

U kunt tot de gebeurtenissen van de tijdreeks door de identiteit van hun bijbehorende profielentiteit toegang hebben door een GET verzoek aan het `/access/entities` eindpunt te doen. Deze identiteit bestaat uit een ID-waarde (`entityId`) en een naamruimte voor identiteit (`entityIdNS`).

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in de sectie van [vraagparameters](#query-parameters) van bijlage.

**API-indeling**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Verzoek**

Met het volgende verzoek wordt een profielentiteit gezocht op ID en worden de waarden voor de eigenschappen `endUserIDs`, `web`en `channel` voor alle tijdreeksgebeurtenissen opgehaald die aan de entiteit zijn gekoppeld.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een gepagineerde lijst van de gebeurtenissen van de tijdreeks en bijbehorende gebieden terug die in de parameters van de verzoekvraag werden gespecificeerd.

>[!NOTE]
>In het verzoek werd een limiet van één (`limit=1`) gespecificeerd, zodat de `count` in het antwoord hieronder vermelde limiet 1 is en slechts één entiteit wordt geretourneerd.

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

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s met resultaten zijn, bevat de `_page.next` eigenschap een id. Bovendien, verstrekt het `_links.next.href` bezit een verzoek URI voor het terugwinnen van de volgende pagina. Om de resultaten terug te winnen, doe een ander GET verzoek aan het `/access/entities` `/entities` eindpunt, nochtans moet u zeker zijn om met de waarde van verstrekte URI te vervangen.

>[!NOTE]
>Zorg ervoor dat u niet per ongeluk `/entities/` in het aanvraagpad herhaalt. Het mag slechts eenmaal voorkomen, `/access/entities?start=...`

**API-indeling**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschrijving |
|---|---|
| `{NEXT_URI}` | De URI-waarde die is opgehaald uit `_links.next.href`. |

**Verzoek**

Met de volgende aanvraag wordt de volgende pagina met resultaten opgehaald door de `_links.next.href` URI als aanvraagpad te gebruiken.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als de reactie is gelukt, wordt de volgende pagina met resultaten geretourneerd. Dit antwoord heeft geen volgende pagina&#39;s van resultaten, zoals die door de lege koordwaarden van `_page.next` en `_links.next.href`worden vermeld.

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

U kunt tot gebeurtenissen van de tijdreeks van veelvoudige bijbehorende profielen toegang hebben door een POST- verzoek aan het `/access/entities` eindpunt te doen en de profielidentiteiten in de lading te verstrekken. Deze identiteiten bestaan elk uit een waarde van identiteitskaart (`entityId`) en een identiteitsnamespace (`entityIdNS`).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `relatedSchema.name` | Als `schema.name` deze waarde `_xdm.context.experienceevent` is, moet het schema voor de profielentiteit specificeren die de gebeurtenissen van de tijdreeks met betrekking tot zijn. |
| `identities` | **(VEREIST)** Een arraylijst met profielen waaruit de bijbehorende tijdreeksgebeurtenissen kunnen worden opgehaald. Elke ingang in de serie wordt geplaatst op één van twee manieren: 1) gebruiken van een volledig gekwalificeerde identiteit die uit de waarde van identiteitskaart en namespace of 2) het verstrekken van een XID bestaat. |
| `fields` | Hiermee worden de gegevens die naar een opgegeven set velden worden geretourneerd, geïsoleerd. Hiermee kunt u filteren welke schemavelden worden opgenomen in opgehaalde gegevens. Voorbeeld: persoonlijke e-mail,persoon.naam,persoon.geslacht |
| `mergePolicyId` | Hiermee wordt het samenvoegingsbeleid aangegeven waarmee de geretourneerde gegevens moeten worden beheerd. Als niet in de de dienstvraag wordt gespecificeerd, zal het gebrek van uw organisatie voor dat schema worden gebruikt. Als er geen standaardbeleid voor samenvoegen is geconfigureerd, bestaat de standaardinstelling uit geen profielsamenvoeging en geen identiteitsstitching. |
| `orderby` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` de standaardinstelling `+timestamp`. |
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

In dit voorbeeldantwoord, verstrekt het eerste vermelde profiel (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) een waarde voor, betekenend dat er extra pagina&#39;s van resultaten voor dit profiel zijn. `_links.next.payload` Zie de volgende sectie over de [toegang tot van extra resultaten](#access-additional-results) voor details over hoe te om tot die extra resultaten toegang te hebben.

### Toegang tot extra resultaten {#access-additional-results}

Wanneer het terugwinnen van de gebeurtenissen van de tijdreeks kan er vele resultaten zijn die, daarom worden teruggekeerd vaak gepagineerd de resultaten. Als er volgende pagina&#39;s met resultaten voor een bepaald profiel zijn, bevat de `_links.next.payload` waarde voor dat profiel een object payload.

Gebruikend deze nuttige lading in het verzoeklichaam, kunt u een extra verzoek van de POST aan het `access/entities` eindpunt uitvoeren om de verdere pagina van tijdreeksgegevens voor dat profiel terug te winnen.

## De gebeurtenissen van de tijdreeks van de toegang in veelvoudige schemaentiteiten

U kunt toegang krijgen tot meerdere entiteiten die via een relatiebeschrijving zijn verbonden. De volgende voorbeeld API vraag veronderstelt een verhouding reeds tussen twee schema&#39;s is bepaald. Voor meer informatie over relatiebeschrijvers, gelieve te lezen de de ontwikkelaarsgids van de [beschrijvers](../../xdm/api/descriptors.md)van de Registratie van het Schema API voor ontwikkelaars.

U kunt queryparameters opnemen in het aanvraagpad om op te geven tot welke gegevens u toegang wilt krijgen. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;). Een volledige lijst van geldige parameters wordt verstrekt in de sectie van [vraagparameters](#query-parameters) van bijlage.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s met resultaten zijn, bevat de `_page.next` eigenschap een id. Bovendien, verstrekt het `_links.next.href` bezit een verzoek URI om de verdere pagina terug te winnen door extra te maken GET verzoeken aan het `access/entities` eindpunt.

## Volgende stappen

Met deze handleiding hebt u de gegevensvelden, profielen en gegevens uit de tijdreeks van het profiel van de klant in real time geopend. Leer hoe te om tot andere gegevensmiddelen toegang te hebben die in Platform worden opgeslagen, zie het overzicht [van de Toegang van](../../data-access/home.md)Gegevens.

## Aanhangsel {#appendix}

In de volgende sectie vindt u aanvullende informatie over de toegang tot profielgegevens met de API.

### Parameters query {#query-parameters}

De volgende parameters worden gebruikt in de weg voor GET verzoeken aan het `/access/entities` eindpunt. Ze dienen om de profielentiteit te identificeren die u wilt benaderen en de gegevens te filteren die in de reactie worden geretourneerd. De vereiste parameters worden geëtiketteerd, terwijl de rest facultatief is.

| Parameter | Beschrijving | Voorbeeld |
|---|---|---|
| `schema.name` | **(VEREIST)** Het XDM-schema van de op te halen entiteit | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Als `schema.name` &quot;_xdm.context.experienceEvent&quot; is, moet deze waarde het schema opgeven voor de profielentiteit waarop de gebeurtenissen uit de tijdreeks betrekking hebben. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(VEREIST)** De id van de entiteit. Als de waarde van deze parameter geen XID is, moet ook een naamruimteparameter voor identiteit worden opgegeven (zie `entityIdNS` hieronder). | `entityId=janedoe@example.com` |
| `entityIdNS` | Als `entityId` geen XID wordt verstrekt, moet dit gebied de identiteitsnaamruimte specificeren. | `entityIdNE=email` |
| `relatedEntityId` | Als &quot;_xdm.context.experienceEvent&quot; `schema.name` is, moet deze waarde de naamruimte van de identiteit van de verwante profielentiteit opgeven. Deze waarde volgt dezelfde regels als `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Als `schema.name` &quot;_xdm.context.experienceEvent&quot; is, moet deze waarde de naamruimte voor de identiteit opgeven voor de entiteit die is opgegeven in `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtert de gegevens die in de reactie worden geretourneerd. Gebruik dit om te specificeren welke schemagebiedwaarden in opgehaalde gegevens moeten omvatten. Voor meerdere velden scheidt u waarden met een komma zonder spaties tussen | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Hiermee wordt het samenvoegingsbeleid aangegeven waarmee de geretourneerde gegevens moeten worden beheerd. Als niet in de vraag wordt gespecificeerd, zal het gebrek van uw organisatie voor dat schema worden gebruikt. Als er geen standaardbeleid voor samenvoegen is geconfigureerd, bestaat de standaardinstelling uit geen profielsamenvoeging en geen identiteitsstitching. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` de standaardinstelling `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Geef de begintijd op voor het filteren van tijdreeksobjecten (in milliseconden). | `startTime=1539838505` |
| `endTime` | Geef de eindtijd op voor het filteren van tijdreeksobjecten (in milliseconden). | `endTime=1539838510` |
| `limit` | Numerieke waarde die het maximumaantal objecten aangeeft dat moet worden geretourneerd. Standaard: 1000 | `limit=100` |
| `withCA` | De vlag van de eigenschap voor het toelaten van gegevens verwerkte attributen voor raadpleging. Standaard: false | `withCA=true` |