---
title: CSV-sjabloon naar API-eindpunt voor schemaconversie
description: Het /rpc/csv2schema eindpunt in de Registratie API van het Schema staat u toe om malplaatjes te gebruiken CSV om de schema's van de Gegevens van de Ervaring van het Model (XDM) automatisch tot stand te brengen.
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 3%

---

# CSV-sjabloon naar API-eindpunt voor schemaconversie

Met het eindpunt `/rpc/csv2schema` in de [!DNL Schema Registry] API kunt u automatisch een XDM-schema (Experience Data Model) maken met een CSV-bestand als sjabloon. Met behulp van dit eindpunt kunt u sjablonen maken voor het bulksgewijs importeren van schemavelden en voor handmatige API- of UI-bewerkingen.

## Aan de slag

Het `/rpc/csv2schema` eindpunt maakt deel uit van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Adobe Experience Platform API met succes te maken.

Het `/rpc/csv2schema` eindpunt maakt deel uit van de verre procedurevraag (RPCs) die door [!DNL Schema Registry] wordt gesteund. In tegenstelling tot andere eindpunten in de [!DNL Schema Registry] API, vereisen RPC-eindpunten geen extra kopteksten zoals `Accept` of `Content-Type` en gebruiken ze geen `CONTAINER_ID` . In plaats daarvan moeten ze de naamruimte `/rpc` gebruiken, zoals wordt getoond in de API-aanroepen hieronder.

## CSV-bestandsvereisten

Als u van dit eindpunt gebruik wilt maken, moet u eerst een CSV-bestand maken met de juiste kolomkoppen en bijbehorende waarden. Sommige kolommen zijn vereist, terwijl de rest optioneel is. In de onderstaande tabel worden deze kolommen en hun rol in de schemaconstructie beschreven.

| CSV-koppositie | CSV-kopnaam | Vereist/optioneel | Beschrijving |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Optioneel | Wanneer het veld is opgenomen en is ingesteld op `true` , wordt hiermee aangegeven dat het veld niet gereed is voor API-upload en moet worden genegeerd. |
| 2 | `isCustom` | Vereist | Hiermee wordt aangegeven of het veld een aangepast veld is. |
| 3 | `fieldGroupId` | Optioneel | De id van de veldgroep waaraan een aangepast veld moet worden gekoppeld. |
| 4 | `fieldGroupName` | (Zie beschrijving) | De naam van de veldgroep waaraan dit veld moet worden gekoppeld.<br><br> Facultatief voor douanevelden die bestaande standaardgebieden niet uitbreiden. Als deze optie leeg blijft, wijst het systeem automatisch de naam toe.<br><br> Vereist voor standaardgebieden of douanegebieden die standaardgebiedsgroepen uitbreiden, die wordt gebruikt om `fieldGroupId` te vragen. |
| 5 | `fieldPath` | Vereist | Het volledige XED-puntnotatiepad voor het veld. Als u alle velden uit een standaardveldgroep wilt opnemen (zoals aangegeven onder `fieldGroupName`), stelt u de waarde in op `ALL` . |
| 6 | `displayName` | Optioneel | De titel of de vriendelijke weergavenaam voor het veld. Kan ook een alias voor de titel zijn als er een bestaat. |
| 7 | `fieldDescription` | Optioneel | Een beschrijving voor het veld. Kan ook een alias voor de beschrijving zijn als er een bestaat. |
| 8 | `dataType` | (Zie beschrijving) | Wijst op het [ basistype van gegevens ](../schema/field-constraints.md#basic-types) voor het gebied. Vereist voor alle aangepaste velden.<br><br> Als `dataType` is ingesteld op `object` , moet `properties` of `$ref` ook voor dezelfde rij worden gedefinieerd, maar niet voor beide. |
| 9 | `isRequired` | Optioneel | Geeft aan of het veld verplicht is voor gegevensinvoer. |
| 10 | `isArray` | Optioneel | Geeft aan of het veld een array is van de aangegeven `dataType` . |
| 11 | `isIdentity` | Optioneel | Geeft aan of het veld een identiteitsveld is. |
| 12 | `identityNamespace` | Vereist als `isIdentity` true is | De [ identiteit namespace ](../../identity-service/features/namespaces.md) voor het identiteitsgebied. |
| 13 | `isPrimaryIdentity` | Optioneel | Geeft aan of het veld de primaire identiteit voor het schema is. |
| 14 | `minimum` | Optioneel | (Alleen voor numerieke velden) De minimumwaarde voor het veld. |
| 15 | `maximum` | Optioneel | (Alleen voor numerieke velden) De maximumwaarde voor het veld. |
| 16 | `enum` | Optioneel | Een lijst met opsommingswaarden voor het veld, uitgedrukt als een array (bijvoorbeeld `[value1,value2,value3]`). |
| 17 | `stringPattern` | Optioneel | (Alleen voor tekenreeksvelden) Een regex-patroon dat de tekenreekswaarde moet overeenkomen om de validatie tijdens het invoeren van gegevens door te geven. |
| 18 | `format` | Optioneel | (Alleen voor tekenreeksvelden) De indeling voor het tekenreeksveld. |
| 19 | `minLength` | Optioneel | (Alleen voor tekenreeksvelden) De minimumlengte van het tekenreeksveld. |
| 20 | `maxLength` | Optioneel | (Alleen voor tekenreeksvelden) De maximumlengte van het tekenreeksveld. |
| 21 | `properties` | (Zie beschrijving) | Vereist als `dataType` is ingesteld op `object` en `$ref` niet is gedefinieerd. Dit definieert de hoofdtekst van het object als een JSON-tekenreeks (bijvoorbeeld `{"myField": {"type": "string"}}` ). |
| 22 | `$ref` | (Zie beschrijving) | Vereist als `dataType` is ingesteld op `object` en `properties` niet is gedefinieerd. Hiermee wordt de `$id` van het object waarnaar wordt verwezen, gedefinieerd voor het objecttype (bijvoorbeeld `https://ns.adobe.com/xdm/context/person` ). |
| 23 | `comment` | Optioneel | Wanneer `isIgnored` is ingesteld op `true` , wordt deze kolom gebruikt om de headerinformatie van het schema op te geven. |

{style="table-layout:auto"}

Verwijs naar het volgende [ malplaatje CSV ](../assets/sample-csv-template.csv) om te bepalen hoe uw Csv- dossier zou moeten worden geformatteerd.

## Een exportlading maken van een CSV-bestand

Nadat u de CSV-sjabloon hebt ingesteld, kunt u het bestand naar het `/rpc/csv2schema` -eindpunt verzenden en het naar een exportlading omzetten.

**API formaat**

```http
POST /rpc/csv2schema
```

**Verzoek**

De payload van de aanvraag moet formuliergegevens gebruiken als indeling. De vereiste formuliervelden worden hieronder weergegeven.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `csv-file` | Het pad naar de CSV-sjabloon die op uw lokale computer is opgeslagen. |
| `schema-class-id` | `$id` van de XDM [ klasse ](../schema/composition.md#class) dat dit schema zal aanwenden. |
| `schema-name` | Een weergavenaam voor het schema. |
| `schema-description` | Een beschrijving voor het schema. |

**Reactie**

Een geslaagde reactie retourneert een exportlading die uit het CSV-bestand is gegenereerd. De payload heeft de vorm van een array en elk arrayitem is een object dat een afhankelijke XDM-component voor het schema vertegenwoordigt. Selecteer de onderstaande sectie om een volledig voorbeeld weer te geven van een exportlading die uit een CSV-bestand is gegenereerd.

+++ Voorbeeld van payload van reactie

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## De payload van het schema importeren

Na het produceren van de de uitvoerlading van het Csv- dossier, kunt u die lading naar het `/rpc/import` eindpunt verzenden om het schema te produceren.

Zie de [ de gids van het de invoereindpunt ](./import.md) voor details op hoe te schema&#39;s van de uitvoerladingen produceren.
