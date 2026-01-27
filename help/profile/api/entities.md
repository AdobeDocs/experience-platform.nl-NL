---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Entiteiten (Profile Access) API-eindpunt
type: Documentation
description: Met Adobe Experience Platform hebt u toegang tot realtime gegevens van het klantprofiel met RESTful-API's of de gebruikersinterface. In deze handleiding wordt beschreven hoe u met behulp van de profiel-API toegang krijgt tot entiteiten, beter bekend als "profielen".
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 17bd3494c2d9b2a05ca86903297ebec85c9350f2
workflow-type: tm+mt
source-wordcount: '2290'
ht-degree: 0%

---

# Het eindpunt van entiteiten (de toegang van het Profiel)

>[!IMPORTANT]
>
>U kunt **slechts** gebruiken deze eindpunten als u Real-Time CDP Ultimate hebt.
>
>Als u Real-Time CDP Prime hebt, kunt u ervaringsgebeurtenissen voor het gebruiksgeval van het verpersoonlijkingsgebruik evenals meningsgebeurtenissen binnen Experience Platform UI blijven opnemen en gebruiken, maar u **niet** zal kunnen opzoeken ervaringsgebeurtenissen gebruikend API.
>
>Als u Real-Time CDP Ultimate hebt en **niet** momenteel programmatically gebeurtenissen opzoekt, gelieve de Zorg van de Klant van Adobe te contacteren om deze eigenschap toe te laten.

Met Adobe Experience Platform hebt u toegang tot [!DNL Real-Time Customer Profile] -gegevens via RESTful API&#39;s of de gebruikersinterface. In deze handleiding wordt beschreven hoe u met de API toegang krijgt tot entiteiten die beter bekend staan als &quot;profielen&quot;. Voor meer informatie bij de toegang tot van profielen die [!DNL Experience Platform] UI gebruiken, gelieve te verwijzen naar de [ de gebruikersgids van het Profiel ](../ui/user-guide.md).

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt is een deel van [[!DNL Real-Time Customer Profile API] ](https://www.adobe.com/go/profile-apis-en). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Entiteitsafwikkeling

Als onderdeel van de architectuurupgrade introduceert Adobe entiteitresolutie voor Accounts en Opportunity, waarbij gebruik wordt gemaakt van deterministische ID-overeenkomsten op basis van de meest recente gegevens. Entiteitsafwikkelingstaak wordt dagelijks uitgevoerd tijdens batchsegmentering, voordat het publiek met meerdere entiteiten met B2B-kenmerken wordt geëvalueerd.

Dankzij deze verbetering kan Experience Platform meerdere records die dezelfde entiteit vertegenwoordigen, identificeren en verenigen, waardoor de gegevensconsistentie wordt verbeterd en het publiek nauwkeuriger wordt gesegmenteerd.

Eerder, baseerden de Rekeningen en de Kansen zich op op identiteitsgrafiek-gebaseerde resolutie die identiteiten, met inbegrip van alle historische ingesties verbond. Bij de nieuwe aanpak van de afwikkeling van entiteiten zijn identiteiten alleen gekoppeld op basis van de meest recente gegevens.

- Account en Opportunity zijn een entiteit die wordt opgelost met een op tijd gebaseerde samenvoeging die gebaseerd is op samenvoegen:
   - Account: identiteiten die de naamruimte `b2b_account` gebruiken.
   - Opportunity: identiteiten gebruiken de naamruimte `b2b_opportunity` .
- Alle andere entiteiten zijn verenigd en alleen primaire identiteitsoverlap wordt samengevoegd met op tijd gebaseerde samenvoeging.

>[!NOTE]
>
>Het oplossen van entiteiten ondersteunt alleen `b2b_account` en `b2b_opportunity` . Identiteiten uit andere naamruimten worden niet gebruikt bij de afwikkeling van entiteiten. Als u aangepaste naamruimten gebruikt, kunt u geen accounts en mogelijkheden vinden.

### Hoe werkt het oplossen van entiteiten?

- **vóór**: Als een aantal van het Systeem van de Nummering van Gegevens Universele (DUNS) als extra identiteit werd gebruikt en het aantal DUNS van de rekening werd bijgewerkt in een bronsysteem zoals CRM, wordt rekeningidentiteitskaart verbonden met zowel oude als nieuwe DUNS aantallen.
- **na**: Als het aantal DUNS als extra identiteit werd gebruikt en het aantal DUNS van de rekening in een bronsysteem als CRM werd bijgewerkt, wordt rekeningidentiteitskaart slechts verbonden met het nieuwe aantal DUNS, daardoor die nauwkeuriger op de huidige staat van rekening wijst.

Als gevolg van deze update weerspiegelt de API van [!DNL Profile Access] nu de meest recente weergave van het samenvoegprofiel nadat een taakcyclus voor het oplossen van entiteiten is voltooid. Bovendien bieden de consistente gegevens gebruiksgevallen, zoals segmentatie, activering en analyse, met een verbeterde gegevensnauwkeurigheid en consistentie.

## Entiteiten ophalen {#retrieve-entity}

>[!IMPORTANT]
>
>De volgende B2B-entiteiten worden niet meer ondersteund voor opzoekverzoeken via API: **Account-Person Relatie, Opportunity-Person Relatie, Campagne, Campagne Lid, Marketing List, en Lid van de Lijst van de Marketing** .
>
>Deze entiteiten worden niet meer ondersteund. Als u bestaande integraties of workflows hebt die afhankelijk zijn van de toegang tot deze entiteiten, moet u deze bijwerken om ondersteunde entiteitstypen te gebruiken om ervoor te zorgen dat de functionaliteit wordt voortgezet.

U kunt een entiteit van het Profiel terugwinnen door een GET verzoek aan het `/access/entities` eindpunt samen met de vereiste vraagparameters te doen.

>[!BEGINTABS]

>[!TAB  de entiteit van het Profiel ]

**API formaat**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;).

Om tot een entiteit van het Profiel toegang te hebben, moet u **de volgende vraagparameters verstrekken:**

- `schema.name`: De naam van het XDM-schema van de entiteit. In dit geval wordt de instructie `schema.name=_xdm.context.profile` gebruikt.
- `entityId`: De id van de entiteit die u probeert op te halen.
- `entityIdNS`: De naamruimte van de entiteit die u probeert op te halen. Deze waarde moet worden verstrekt als `entityId` **** geen XID is.

Bovendien, wordt het gebruik van de volgende vraagparameter *hoogst* geadviseerd:

- `mergePolicyId`: De id van het samenvoegbeleid waarmee u de gegevens wilt filteren. Als er geen samenvoegbeleid is opgegeven, wordt het standaardsamenvoegbeleid van uw organisatie gebruikt.

Een volledige lijst van geldige parameters wordt verstrekt in de [ sectie van vraagparameters ](#query-parameters) van appendix.

**Verzoek**

Met het volgende verzoek worden de e-mail en de naam van een klant opgehaald aan de hand van een identiteit.

+++ Een voorbeeldverzoek om een entiteit op te halen met behulp van een identiteit

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 200 met de aangevraagde entiteit.

+++ Een voorbeeldreactie waarin de aangezochte entiteit is opgenomen

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>Als een verwante grafiek meer dan 50 identiteiten verbindt, zal deze dienst status 422 van HTTP en het bericht &quot;Te veel verwante identiteiten&quot;terugkeren. Als deze fout optreedt, kunt u wellicht meer queryparameters toevoegen om uw zoekopdracht te beperken.

>[!TAB  B2B- Rekening ]

**API formaat**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;).

Om tot de B2B gegevens van de Rekening toegang te hebben, moet u **** de volgende vraagparameters verstrekken:

- `schema.name`: De naam van het XDM-schema van de entiteit. In dit geval is deze waarde `schema.name=_xdm.context.account` .
- `entityId`: De id van de entiteit die u probeert op te halen.
- `entityIdNS`: De naamruimte van de entiteit die u probeert op te halen. Deze waarde moet worden verstrekt als `entityId` **** geen XID is.

Bovendien, wordt het gebruik van de volgende vraagparameter *hoogst* geadviseerd:

- `mergePolicyId`: De id van het samenvoegbeleid waarmee u de gegevens wilt filteren. Als er geen samenvoegbeleid is opgegeven, wordt het standaardsamenvoegbeleid van uw organisatie gebruikt.

Een volledige lijst van geldige parameters wordt verstrekt in de [ sectie van vraagparameters ](#query-parameters) van appendix.

**Verzoek**

+++ Een voorbeeldverzoek om een B2B-account op te halen

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 200 met de aangevraagde entiteit.

+++ Een voorbeeldreactie waarin de aangezochte entiteit is opgenomen

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB  B2B Kans ]

**API formaat**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;).

Om tot een entiteit van de Kans B2B toegang te hebben, moet u **** de volgende vraagparameters verstrekken:

- `schema.name`: De naam van het XDM-schema van de entiteit. In dit geval wordt de instructie `schema.name=_xdm.context.opportunity` gebruikt.
- `entityId`: De id van de entiteit die u probeert op te halen.
- `entityIdNS`: De naamruimte van de entiteit die u probeert op te halen. Deze waarde moet worden verstrekt als `entityId` **** geen XID is.

Bovendien, wordt het gebruik van de volgende vraagparameter *hoogst* geadviseerd:

- `mergePolicyId`: De id van het samenvoegbeleid waarmee u de gegevens wilt filteren. Als er geen samenvoegbeleid is opgegeven, wordt het standaardsamenvoegbeleid van uw organisatie gebruikt.

Een volledige lijst van geldige parameters wordt verstrekt in de [ sectie van vraagparameters ](#query-parameters) van appendix.

**Verzoek**

+++ Een voorbeeldverzoek om een B2B Opportunity op te halen

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 200 met de aangevraagde entiteit.

+++ Een voorbeeldreactie waarin de aangezochte entiteit is opgenomen

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Meerdere entiteiten ophalen {#retrieve-entities}

U kunt veelvoudige entiteiten van het Profiel terugwinnen door een POST- verzoek aan het `/access/entities` eindpunt te doen en de identiteiten in de lading te verstrekken.

>[!BEGINTABS]

>[!TAB  de entiteiten van het Profiel ]

**API formaat**

```http
POST /access/entities
```

**Verzoek**

In het volgende verzoek worden de namen en e-mailadressen van verschillende klanten opgehaald aan de hand van een lijst met identiteiten.

+++Een voorbeeldverzoek om meerdere entiteiten op te halen

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp"
      }'
```

| Eigenschap | Type | Beschrijving |
| -------- |----- | ----------- |
| `schema.name` | String | **(Vereist)** De naam van het XDM-schema tot de entiteit behoort. |
| `fields` | Array | De XDM-velden die moeten worden geretourneerd, als een array van tekenreeksen. Standaard worden alle velden geretourneerd. |
| `identities` | Array | **(Vereist)** een serie die een lijst van identiteiten voor de entiteiten bevat u wilt toegang hebben tot. |
| `identities.entityId` | String | De id van een entiteit waartoe u toegang wilt hebben. |
| `identities.entityIdNS.code` | String | De naamruimte van een entiteit-id waartoe u toegang wilt. |
| `timeFilter.startTime` | Geheel | Geeft de begintijd op voor het filteren van profielentiteiten (in milliseconden). Deze waarde wordt standaard ingesteld als het begin van de beschikbare tijd. |
| `timeFilter.endTime` | Geheel | Hiermee geeft u de eindtijd op voor het filteren van profielentiteiten (in milliseconden). Deze waarde wordt standaard ingesteld als het einde van de beschikbare tijd. |
| `limit` | Geheel | Het maximumaantal records dat moet worden geretourneerd. Deze waarde is standaard ingesteld op 1000. |
| `orderby` | String | De sorteervolgorde van opgehaalde ervaringsgebeurtenissen op tijdstempel, geschreven als `(+/-)timestamp` met als standaardwaarde `+timestamp` . |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met de aangevraagde velden met entiteiten die zijn opgegeven in de aanvraaginstantie.

+++ Een voorbeeldreactie waarin de gevraagde entiteiten zijn opgenomen

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

+++

>[!TAB  B2B- Rekening ]

**API formaat**

```http
POST /access/entities
```

**Verzoek**

Het volgende verzoek wint de gevraagde B2B- Rekeningen terug.

+++Een voorbeeldverzoek om meerdere entiteiten op te halen

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Eigenschap | Type | Beschrijving |
| -------- |----- | ----------- |
| `schema.name` | String | **(Vereist)** De naam van het XDM-schema tot de entiteit behoort. |
| `identities` | Array | **(Vereist)** een serie die een lijst van identiteiten voor de entiteiten bevat u wilt toegang hebben tot. |
| `identities.entityId` | String | De id van een entiteit waartoe u toegang wilt hebben. |
| `identities.entityIdNS.code` | String | De naamruimte van een entiteit-id waartoe u toegang wilt. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met de aangevraagde entiteiten.

+++ Een voorbeeldreactie waarin de gevraagde entiteiten zijn opgenomen

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB  B2B Kans ]

**API formaat**

```http
POST /access/entities
```

**Verzoek**

Het volgende verzoek wint de gevraagde B2B kansen terug.

+++ Een voorbeeldverzoek om meerdere entiteiten op te halen

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Eigenschap | Type | Beschrijving |
| -------- |----- | ----------- |
| `schema.name` | String | **(Vereist)** De naam van het XDM-schema tot de entiteit behoort. |
| `identities` | Array | **(Vereist)** een serie die een lijst van identiteiten voor de entiteiten bevat u wilt toegang hebben tot. |
| `identities.entityId` | String | De id van een entiteit waartoe u toegang wilt hebben. |
| `identities.entityIdNS.code` | String | De naamruimte van een entiteit-id waartoe u toegang wilt. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met de aangevraagde entiteiten.

+++ Een voorbeeldreactie waarin de gevraagde entiteiten zijn opgenomen

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Een volgende pagina met resultaten openen

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s met resultaten zijn, bevat de eigenschap `_page.next` een id. Daarnaast biedt de eigenschap `_links.next.href` een aanvraag-URI voor het ophalen van de volgende pagina. Als u de resultaten wilt ophalen, dient u een ander GET-verzoek in bij het `/access/entities` eindpunt en vervangt u `/entities` door de waarde van de opgegeven URI.

>[!NOTE]
>
>Zorg ervoor dat u `/entities/` niet per ongeluk herhaalt in het aanvraagpad. Moet slechts eenmaal worden weergegeven als, `/access/entities?start=...`

**API formaat**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschrijving |
|---|---|
| `{NEXT_URI}` | De URI-waarde die is opgehaald uit `_links.next.href` . |

**Verzoek**

Met de volgende aanvraag wordt de volgende resultatenpagina opgehaald met de `_links.next.href` URI als aanvraagpad.

+++ Een voorbeeldverzoek voor toegang tot de volgende pagina met resultaten

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Als de reactie is gelukt, wordt de volgende pagina met resultaten geretourneerd. Dit antwoord heeft geen volgende pagina&#39;s met resultaten, zoals aangegeven door de lege tekenreekswaarden `_page.next` en `_links.next.href` .

+++ Een voorbeeldreactie met de volgende pagina met entiteiten

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

+++

## Entiteiten verwijderen {#delete-entity}

>[!IMPORTANT]
>
>Het eindpunt van de verwijderingsentiteit wordt eind oktober 2025 vervangen. Als u verslag schrapt verrichtingen wilt uitvoeren, kunt u het [ verslag van de Levenscyclus van Gegevens gebruiken schrapt API werkschema ](/help/hygiene/api/workorder.md) of het [ het verslag van de Levenscyclus van Gegevens schrapt UI ](/help/hygiene/ui/record-delete.md) in plaats daarvan.
>
>Bovendien zijn verwijderingsaanvragen voor de volgende B2B-entiteiten al afgekeurd:
>
>- Account
>- Relatie account-persoon
>- Kans
>- Opportunity-Person relatie
>- Campaign
>- Campagnelid
>- Marketinglijst
>- Leden van de marketinglijst

U kunt een entiteit van de Opslag van het Profiel schrappen door een verzoek van DELETE aan het `/access/entities` eindpunt samen met de vereiste vraagparameters te doen.

**API formaat**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

De parameters van de vraag die in de verzoekweg worden verstrekt specificeren welke gegevens aan toegang. U kunt meerdere parameters opnemen, gescheiden door en-tekens (&amp;).

Om een entiteit te schrappen, moet u **** de volgende vraagparameters verstrekken:

- `schema.name`: De naam van het XDM-schema van de entiteit. In dit gebruiksgeval, kunt u **slechts** gebruiken `schema.name=_xdm.context.profile`.
- `entityId`: De id van de entiteit die u probeert op te halen.
- `entityIdNS`: De naamruimte van de entiteit die u probeert op te halen. Deze waarde moet worden verstrekt als `entityId` **** geen XID is.
- `mergePolicyId`: De id van het samenvoegbeleid van de entiteit. Het samenvoegingsbeleid bevat informatie over identiteitsstitching en key-value XDM voorwerp het samenvoegen. Als deze waarde niet wordt opgegeven, wordt het standaardsamenvoegbeleid gebruikt.

**Verzoek**

Met het volgende verzoek wordt de opgegeven entiteit verwijderd.

+++ Een voorbeeldverzoek om een entiteit te verwijderen

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 202 met een lege antwoordinstantie.

## Volgende stappen

In deze handleiding hebt u toegang tot gegevensvelden, profielen en gegevens uit de tijdreeks van [!DNL Real-Time Customer Profile] . Leren hoe te om tot andere gegevensmiddelen toegang te hebben die in [!DNL Experience Platform] worden opgeslagen, zie het [ overzicht van de Toegang van Gegevens ](../../data-access/home.md).

## Bijlage {#appendix}

In de volgende sectie vindt u aanvullende informatie over de toegang tot [!DNL Profile] -gegevens met behulp van de API.

### Query-parameters {#query-parameters}

De volgende parameters worden gebruikt in de weg voor GET- verzoeken aan het `/access/entities` eindpunt. Ze dienen om de profielentiteit te identificeren die u wilt benaderen en de gegevens te filteren die in de reactie worden geretourneerd. De vereiste parameters worden geëtiketteerd, terwijl de rest facultatief is.

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `schema.name` | **(Vereist)** De naam van het schema XDM van de entiteit. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | Als `schema.name` `_xdm.context.experienceevent` is, moet deze waarde **** het schema voor de profielentiteit specificeren dat de gebeurtenissen van de tijdreeks met betrekking tot zijn. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Vereist)** identiteitskaart van de entiteit. Als de waarde van deze parameter geen XID is, moet een parameter van identiteitsnamespace (`entityIdNS`) ook worden verstrekt. | `entityId=janedoe@example.com` |
| `entityIdNS` | Als `entityId` niet als XID wordt verstrekt, moet dit gebied **** de identiteit specificeren namespace. | `entityIdNS=email` |
| `relatedEntityId` | Als `schema.name` `_xdm.context.experienceevent` is, moet deze waarde **** identiteitskaart van de verwante profielentiteit specificeren. Deze waarde volgt dezelfde regels als `entityId` . | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Als `schema.name` &quot;_xdm.context.experienceEvent&quot; is, moet deze waarde de naamruimte van de identiteit opgeven voor de entiteit die is opgegeven in `relatedEntityId` . | `relatedEntityIdNS=CRMID` |
| `fields` | Hiermee filtert u de gegevens die in de reactie worden geretourneerd. Gebruik dit om te specificeren welke waarden van het schemagebied in opgehaalde gegevens moeten omvatten. Voor meerdere velden scheidt u waarden met een komma zonder tussenruimten. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | *geadviseerde* identificeert het fusiebeleid waardoor om de teruggekeerde gegevens te regeren. Als niet in de vraag wordt gespecificeerd, zal het gebrek van uw organisatie voor dat schema worden gebruikt. Als er geen standaardsamenvoegingsbeleid is gedefinieerd voor het schema dat u aanvraagt, retourneert de API een HTTP 422-foutstatuscode. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | De sorteervolgorde van opgehaalde entiteiten op tijdstempel. Dit wordt geschreven als `(+/-)timestamp`, waarbij de standaardwaarde `+timestamp` is. | `orderby=-timestamp` |
| `startTime` | Geeft de begintijd aan om de entiteiten te filteren (in milliseconden). | `startTime=1539838505` |
| `endTime` | Geeft de eindtijd aan om entiteiten te filteren (in milliseconden). | `endTime=1539838510` |
| `limit` | Geeft het maximumaantal entiteiten aan dat moet worden geretourneerd. Deze waarde is standaard ingesteld op 1000. | `limit=100` |
| `property` | Filters op de eigenschapswaarde. Deze vraagparameter steunt de volgende beoordelaars: =, !=, &lt;, &lt;=, >, >=. Dit kan alleen worden gebruikt met ervaringsgebeurtenissen, waarbij maximaal drie eigenschappen worden ondersteund. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
