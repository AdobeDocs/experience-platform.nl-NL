---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens prep;api gids;toewijzende reeksen;
solution: Experience Platform
title: API-eindpunt voor toewijzingssets
topic: mapping sets
description: 'U kunt het `/mappingSets eindpunt ` in Adobe Experience Platform API gebruiken om kaartreeksen programmatically terug te winnen, tot stand te brengen bij te werken en te bevestigen. '
translation-type: tm+mt
source-git-commit: 73bf6abb143c0866a400aafe984f9a553ffc1abf
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---


# Punt voor toewijzingssets

Toewijzingssets kunnen worden gebruikt om te definiëren hoe gegevens in een bronschema worden toegewezen aan dat van een doelschema. U kunt het `/mappingSets` eindpunt in de Prep API van Gegevens gebruiken om kaartreeksen programmatically terug te winnen, tot stand te brengen bij te werken en te bevestigen.

## Lijsttoewijzingssets

U kunt een lijst van alle afbeeldingsreeksen voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan het `/mappingSets` eindpunt te doen.

**API-indeling**

Het `/mappingSets` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel de meeste van deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om de kostbare overhead te helpen verminderen. Nochtans, moet u zowel `start` als `limit` parameters als deel van uw verzoek omvatten. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /mappingSets?limit={LIMIT}&start={START}
GET /mappingSets?limit={LIMIT}&start={START}&name={NAME}
GET /mappingSets?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
GET /mappingSets?limit={LIMIT}&start={START}&expandSchema={EXPAND_SCHEMA}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{LIMIT}` | (**Required**) specificeert het aantal teruggekeerde kaartreeksen. |
| `{START}` | (**Required**) Specificeert de compensatie van de pagina&#39;s van resultaten. Als u de eerste pagina met resultaten wilt ophalen, stelt u de waarde in op `start=0`. |
| `{NAME}` | Filtert de toewijzingssets op naam. |
| `{ORDER_BY}` | Hiermee sorteert u de volgorde van de resultaten. De enige ondersteunde velden zijn `createdDate` en `updatedDate`. U kunt de eigenschap voorvullen met `+` of `-` om deze te sorteren in oplopende of aflopende volgorde. |
| `{EXPAND_SCHEMA}` | Een Booleaanse waarde die bepaalt of het volledige uitvoerschema wordt geretourneerd als onderdeel van de reactie. |

**Verzoek**

Het volgende verzoek zal de laatste twee kaartreeksen binnen uw IMS Organisatie terugwinnen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "data": [
        {
            "id": "428beb15b4864daaaa9dc3f005448005",
            "version": 1,
            "createdDate": 1582250953000,
            "modifiedDate": 1582251156000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_ui_platform",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "e660142cab8e438382abc5691b364b30",
                "version": 0,
                "sampleId": "f9e83882e3e34c1f8b873a3b8113c01e"
            },
            "outputSchema": {
                "id": "1956affc28be468aa452e5e47c680c6b",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "af809223484341009ce0db13d4b32a3a",
                    "version": 0,
                    "createdDate": 1582250953000,
                    "modifiedDate": 1582250953000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "id",
                    "destination": "person.name.firstName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "id",
                    "destinationXdmPath": "person.name.firstName"
                }
            ],
            "status": "PUBLISHED",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        },
        {
            "id": "8afb1351833a4a4692ea61074b60813b",
            "version": 0,
            "createdDate": 1582250893000,
            "modifiedDate": 1582250893000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "97fe2ecf4faa400bb66dd6be88a53fe4",
                "version": 0,
                "sampleId": "0248bfb352214f908bdd6cf9c19447e1"
            },
            "outputSchema": {
                "id": "e9c3696715d94905bb4e9bfc2c508e66",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "74647d8bf3b742f289534bee2fdeb732",
                    "version": 0,
                    "createdDate": 1582250893000,
                    "modifiedDate": 1582250893000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "last_name",
                    "destination": "person.name.lastName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "last_name",
                    "destinationXdmPath": "person.name.lastName"
                }
            ],
            "status": "DRAFT",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "_page": {
        "count": 0,
        "limit": 2
    }
}
```

## Een toewijzingsset maken

U kunt een nieuwe mappingsreeks tot stand brengen door een verzoek van de POST aan het `/mappingSets` eindpunt te doen.

**API-indeling**

```http
POST /mappingSets
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe mappingsreeks, die door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `outputSchema.schemaRef.id` | De id van het XDM-schema waarnaar u verwijst. |
| `outputSchema.schemaRef.contentType` | Bepaalt het reactieformaat van het referenced schema. Meer informatie over dit gebied kan in [de ontwikkelaarsgids van de Registratie van het Schema](../../xdm/api/schemas.md#lookup) worden gevonden. |
| `mappings.sourceType` | Het brontype beschrijft hoe de waarde uit de bron aan de bestemming zal worden gehaald. |
| `mappings.source` | De locatie waar u de gegevens wilt toewijzen. |
| `mappings.destination` | De locatie waar de gegevens moeten worden toegewezen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over de zojuist gemaakte toewijzingenset.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901254724,
    "modifiedDate": 1614901254724,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Toewijzingen valideren

U kunt bevestigen dat uw afbeeldingen behoorlijk werken door een verzoek van de POST aan het `/mappingSets/validate` eindpunt te doen.

**API-indeling**

```http
POST /mappingSets/validate
```

**Verzoek**

In het volgende verzoek worden de toewijzingen gevalideerd die in de lading zijn opgegeven.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met validatiegegevens voor de voorgestelde toewijzing.

```json
{
    "validationResponse": [
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        }
    ]
}
```

## Gegevens voorvertonen voor toewijzingen

U kunt voorproef waaraan uw gegevens zullen worden in kaart gebracht door een verzoek van de POST aan het `/mappingSets/preview` eindpunt te doen.

**API-indeling**

```http
POST /mappingSets/preview
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "data": [
        {
            "id": 1234,
            "firstName": "Jim",
            "lastName": "Seltzer"
        }
    ],
    "mappingSet": {
        "outputSchema": {
            "schemaRef": {
                "id": "https://ns.adobe.com/stardust/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "id",
                "destination": "_id",
                "name": "id",
                "description": "Identifier field"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "firstName",
                "destination": "person.name.firstName"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "lastName",
                "destination": "person.name.lastName"
            }
        ]
    }
}'
```

**Antwoord**

Een succesvol antwoord retourneert HTTP-status 200 met een voorvertoning van de toegewezen gegevens.

```json
[
    {
        "data": {
            "person": {
                "name": {
                    "firstName": "Jim",
                    "lastName": "Seltzer"
                }
            },
            "_id": "1234"
        },
        "errors": null
    }
]
```

## Een toewijzingenset opzoeken

U kunt een specifieke die afbeelding terugwinnen door zijn identiteitskaart in de weg van een verzoek van de GET aan het `/mappingSets` eindpunt te verstrekken wordt geplaatst. Dit eindpunt steunt ook verscheidene vraagparameters om u te helpen details over de gespecificeerde versie van de kaartreeks terugwinnen.

**API-indeling**

```http
GET /mappingSets/{MAPPING_SET_ID}
GET /mappingSets/{MAPPING_SET_ID}?expandSchema={EXPAND_SCHEMA}
GET /mappingSets/{MAPPING_SET_ID}?version={VERSION}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | (**Required**) identiteitskaart van de mappenset die u wilt terugwinnen. |
| `{EXPAND_SCHEMA}` | Een Booleaanse queryparameter die bepaalt of het uitvoerschema moet worden geretourneerd als onderdeel van de reactie. |
| `{VERSION}` | Een parameter van de geheelvraag die bepaalt welke versie van de afbeelding die wordt geplaatst om terug te winnen. |

**Verzoek**

Het volgende verzoek wint gedetailleerde informatie over een gespecificeerde mappingsreeks terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de mappenset terug u wilde terugwinnen.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901255000,
    "modifiedDate": 1614901255000,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string"
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                }
                            }
                        }
                    }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "{IMS_ORG}",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "a11f44b0214d4fdcb79cbb5e1d93e638",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "id": "b9bf7873451f4b7ba767ca3ba9327750",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName",
        },
        {
            "id": "bab961fc18f54789b9268ec04c6f6f9b",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName",
        }
    ],
    "status": "DRAFT",
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## Een toewijzingsset bijwerken

U kunt een mappingsreeks bijwerken door zijn identiteitskaart in de weg van een `PUT` verzoek aan het `mappingSets` eindpunt te verstrekken.

**API-indeling**

```http
PUT /mappingSets/{MAPPING_SET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | De id van de toewijzingsset die u wilt bijwerken. |

**Verzoek**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "nationality",
            "destination": "person.nationality"           
        }
    ]
}
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over de zojuist bijgewerkte toewijzingenset.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 1,
    "createdDate": 1614901255000,
    "modifiedDate": 1614909614227,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string",
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                },
                                "suffix": {
                                    "title": "Suffix",
                                    "type": "string"
                                }
                            }
                        }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id"
        },
        {
            "id": "394bec970d54410b98e1d4c55a3843ca",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "id": "a78729629b22418998b528755b3e0fb1",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "id": "c5211e1e295f48018c125c24a04e925a",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "nationality",
            "destination": "person.nationality"
        }
    ],
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## De toewijzingen voor een toewijzingsset weergeven

U kunt alle afbeeldingen bekijken die tot een specifieke die afbeelding behoren door zijn identiteitskaart in de weg van een verzoek van de GET aan het volgende eindpunt te verstrekken behoren.

**API-indeling**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | De id van de toewijzingsset waarvoor u toewijzingen wilt ophalen. |

**Verzoek**

Het volgende verzoek retourneert alle toewijzingen in de opgegeven toewijzingenset.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
[
    {
        "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "id",
        "destination": "_id",
        "name": "id",
        "description": "Identifier field",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "id",
        "destinationXdmPath": "_id"
    },
    {
        "id": "394bec970d54410b98e1d4c55a3843ca",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "firstName",
        "destination": "person.name.firstName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "firstName",
        "destinationXdmPath": "person.name.firstName"
    },
    {
        "id": "a78729629b22418998b528755b3e0fb1",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "lastName",
        "destination": "person.name.lastName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "lastName",
        "destinationXdmPath": "person.name.lastName"
    },
    {
        "id": "c5211e1e295f48018c125c24a04e925a",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "nationality",
        "destination": "person.nationality",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "nationality",
        "destinationXdmPath": "person.nationality"
    }
]
```

## Een toewijzing opzoeken in een toewijzingsset

U kunt een specifieke afbeelding voor een die afbeelding terugwinnen door hun IDs in de weg van een verzoek van de GET aan het volgende eindpunt te verstrekken wordt geplaatst.

**API-indeling**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings/{MAPPING_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | De id van de toewijzingsset waarover u toewijzingsgegevens wilt opzoeken. |
| `{MAPPING_ID}` | De id van de toewijzing die u wilt opzoeken. |

**Verzoek**

Het volgende verzoek wint informatie over een specifieke afbeelding in de gespecificeerde mappingsreeks terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings/394bec970d54410b98e1d4c55a3843ca \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde afbeelding terug.

```json
{
    "id": "394bec970d54410b98e1d4c55a3843ca",
    "version": 0,
    "createdDate": 1614909614000,
    "modifiedDate": 1614909614000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceType": "text/x.schema-path",
    "source": "firstName",
    "destination": "person.name.firstName",
    "identity": false,
    "primaryIdentity": false,
    "matchScore": 0.0,
    "functionVersion": 1,
    "sourceAttribute": "firstName",
    "destinationXdmPath": "person.name.firstName"
}
```
