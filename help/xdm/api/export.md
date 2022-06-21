---
title: API-eindpunt exporteren
description: Het /export eindpunt in de Registratie API van het Schema staat u toe om middelen XDM tussen zandbakken te delen.
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Exporteindpunt

Alle bronnen binnen de [!DNL Schema Library] bevinden zich in een specifieke sandbox in Adobe Experience Platform. In sommige gevallen wilt u wellicht XDM-bronnen (Experience Data Model) delen tussen sandboxen en organisaties. De `/rpc/export` in de [!DNL Schema Registry] API staat u toe om een de uitvoerlading voor om het even welk schema, de groep van het schemagebied of gegevenstype in te produceren [!DNL Schema Library]en gebruik vervolgens die payload om die bron (en alle afhankelijke bronnen) in een doelsandbox en -organisatie te importeren via de [`/rpc/import` eindpunt](./import.md).

## Aan de slag

De `/rpc/export` eindpunt maakt deel uit van [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

De `/rpc/export` het eindpunt maakt deel uit van de verre procedurevraag (RPCs) die door het [!DNL Schema Registry]. Anders dan bij andere eindpunten in het deelvenster [!DNL Schema Registry] API, RPC-eindpunten vereisen geen extra headers zoals `Accept` of `Content-Type`en geen `CONTAINER_ID`. In plaats daarvan moeten ze de opdracht `/rpc` naamruimte, zoals wordt getoond in de API-aanroepen hieronder.

## Een exportlading genereren voor een bron {#export}

Voor een bestaand schema, een bestaande veldgroep of een bestaand gegevenstype in het dialoogvenster [!DNL Schema Library], kunt u een exportheffing genereren door een verzoek tot GET aan de `/export` eindpunt, verstrekkend identiteitskaart van het middel in de weg.

**API-indeling**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_ID}` | De `meta:altId` of URL-gecodeerd `$id` van de XDM-bron die u wilt exporteren. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een exportlading opgehaald voor een `Restaurant` veldgroep.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Antwoord**

Een succesvolle reactie keert een serie van voorwerpen terug, die het doelXDM middel en al zijn afhankelijke middelen vertegenwoordigen. In dit voorbeeld is het eerste object in de array een door de gebruiker gemaakt object `Property` gegevenstype dat `Restaurant` veldgroep werkt, terwijl het tweede object het `Restaurant` veldgroep zelf. Deze lading kan dan worden gebruikt aan [de bron importeren](#import) naar een andere sandbox of IMS-organisatie.

Merk op dat alle instanties van huurder ID van het middel met worden vervangen `<XDM_TENANTID_PLACEHOLDER>`. Dit staat de Registratie van het Schema toe om correcte huurdersidentiteitskaart op de middelen automatisch toe te passen afhankelijk van waar zij in de verdere de invoervraag worden verzonden.

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

Nadat u de laadgegevens voor exporteren vanuit het CSV-bestand hebt gegenereerd, kunt u die laadgegevens naar de `/rpc/import` eindpunt om het schema te produceren.

Zie de [hulplijn voor importeindpunt](./import.md) voor details over hoe te om schema&#39;s van de ladingen van de uitvoer te produceren.
