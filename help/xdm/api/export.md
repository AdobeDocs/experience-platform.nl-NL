---
title: API-eindpunt exporteren
description: Het /export eindpunt in de Registratie API van het Schema staat u toe om middelen XDM tussen zandbakken te delen.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Exporteindpunt

Alle bronnen in de [!DNL Schema Library] bevinden zich in een specifieke sandbox in Adobe Experience Platform. In sommige gevallen wilt u wellicht XDM-bronnen (Experience Data Model) delen tussen sandboxen en organisaties. Het `/rpc/export` eindpunt in [!DNL Schema Registry] API staat u toe een de uitvoerlading voor om het even welk schema, de groep van het schemagebied, of gegevenstype in [!DNL Schema Library] produceren, en dan die nuttige lading gebruiken om dat middel (en alle afhankelijke middelen) in een doelzandbak en organisatie door het [`/rpc/import` eindpunt ](./import.md) in te voeren.

## Aan de slag

Het `/rpc/export` eindpunt maakt deel uit van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

Het `/rpc/export` eindpunt maakt deel uit van de verre procedurevraag (RPCs) die door [!DNL Schema Registry] wordt gesteund. In tegenstelling tot andere eindpunten in de [!DNL Schema Registry] API, vereisen RPC-eindpunten geen extra kopteksten zoals `Accept` of `Content-Type` en gebruiken ze geen `CONTAINER_ID` . In plaats daarvan moeten ze de naamruimte `/rpc` gebruiken, zoals wordt getoond in de API-aanroepen hieronder.

## Een exportlading genereren voor een bron {#export}

Voor om het even welk bestaand schema, gebiedsgroep, of gegevenstype in [!DNL Schema Library], kunt u een de uitvoerlading produceren door een verzoek van de GET aan het `/export` eindpunt te richten, verstrekkend identiteitskaart van het middel in de weg.

**API formaat**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de XDM-bron die u wilt exporteren. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een exportlading opgehaald voor een veldgroep `Restaurant` .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Reactie**

Een succesvolle reactie keert een serie van voorwerpen terug, die het doelXDM middel en al zijn afhankelijke middelen vertegenwoordigen. In dit voorbeeld is het eerste object in de array een door de gebruiker gemaakt gegevenstype `Property` dat door de veldgroep `Restaurant` wordt gebruikt, terwijl het tweede object de veldgroep `Restaurant` zelf is. Deze nuttige lading kan dan worden gebruikt om het middel [&#128279;](#import) in een verschillende zandbak of organisatie in te voeren .

Merk op dat alle instanties van de huurder ID van het middel door `<XDM_TENANTID_PLACEHOLDER>` worden vervangen. Dit staat de Registratie van het Schema toe om correcte huurdersidentiteitskaart op de middelen automatisch toe te passen afhankelijk van waar zij in de verdere de invoervraag worden verzonden.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## De bron importeren {#import}

Na het produceren van de de uitvoerlading van het Csv- dossier, kunt u die lading naar het `/rpc/import` eindpunt verzenden om het schema te produceren.

Zie de [ de gids van het de invoereindpunt ](./import.md) voor details op hoe te schema&#39;s van de uitvoerladingen produceren.
