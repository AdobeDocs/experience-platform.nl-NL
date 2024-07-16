---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Registry;field Group;Field group;Field groups;create
solution: Experience Platform
title: API-eindpunt voor veldgroepen
description: Het /fieldgroups eindpunt in de Registratie API van het Schema staat u toe om groepen van het XDM schemagebied binnen uw ervaringstoepassing programmatically te beheren.
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# Het eindpunt van schemaveldgroepen

De de gebiedsgroepen van het schema zijn herbruikbare componenten die één of meerdere gebieden bepalen die een bepaald concept, zoals een individuele persoon, een postadres, of een milieu van Webbrowser vertegenwoordigen. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Met het eindpunt `/fieldgroups` in de [!DNL Schema Registry] API kunt u via programmacode veldgroepen beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met veldgroepen ophalen {#list}

U kunt alle veldgroepen weergeven onder de container `global` of `tenant` door een GET-aanvraag in te dienen bij respectievelijk `/global/fieldgroups` of `/tenant/fieldgroups` .

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [ vraagparameters ](./appendix.md#query) in het bijlage document voor meer informatie.

**API formaat**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarvan u veldgroepen wilt ophalen: `global` voor veldgroepen die zijn gemaakt door Adoben of `tenant` voor veldgroepen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie het [ bijlage document ](./appendix.md#query) voor een lijst van beschikbare parameters. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een lijst met veldgroepen opgehaald uit de container `tenant` . Hierbij wordt een `orderby` query-parameter gebruikt om de veldgroepen op hun `title` -kenmerk te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor groepen met lijstvelden:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-veldgroep voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

In de bovenstaande aanvraag is de header `application/vnd.adobe.xed-id+json` `Accept` gebruikt en daarom bevat de reactie alleen de kenmerken `title` , `$id` , `meta:altId` en `version` voor elke veldgroep. Als u de andere `Accept` header (`application/vnd.adobe.xed+json` ) gebruikt, worden alle kenmerken van elke veldgroep geretourneerd. Selecteer de juiste `Accept` header, afhankelijk van de informatie die u in uw reactie nodig hebt.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## Een veldgroep opzoeken {#lookup}

U kunt een specifieke veldgroep opzoeken door de id van de veldgroep op te nemen in het pad van een GET-aanvraag.

**API formaat**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin de veldgroep is opgeslagen die u wilt ophalen: `global` voor een door Adobe gemaakte veldgroep of `tenant` voor een veldgroep die eigendom is van uw organisatie. |
| `{FIELD_GROUP_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de veldgroep die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een veldgroep opgehaald op basis van de `meta:altId` -waarde die in het pad is opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Voor alle opzoekverzoeken moet een `version` worden opgenomen in de `Accept` -koptekst. De volgende `Accept` headers zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Met `$ref` en `allOf` heeft Raw titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` en `allOf` resolve, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Onbewerkt met `$ref` en `allOf` , geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` en `allOf` opgelost, inclusief beschrijvingen. |

{style="table-layout:auto"}

**Reactie**

Als de reactie is geslaagd, worden de details van de veldgroep geretourneerd. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende kopteksten van `Accept` om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
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
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een veldgroep maken {#create}

U kunt een aangepaste veldgroep definiëren onder de `tenant` -container door een POST aan te vragen.

**API formaat**

```http
POST /tenant/fieldgroups
```

**Verzoek**

Wanneer u een nieuwe veldgroep definieert, moet deze een `meta:intendedToExtend` -kenmerk bevatten met een lijst van de `$id` -klassen waarmee de veldgroep compatibel is. In dit voorbeeld is de veldgroep compatibel met een klasse `Property` die eerder is gedefinieerd. Aangepaste velden moeten onder `_{TENANT_ID}` worden genest (zoals in het voorbeeld wordt getoond) om conflicten te voorkomen met vergelijkbare velden die door klassen en andere veldgroepen worden verschaft.

>[!NOTE]
>
>Voor details op hoe te om verschillende gebiedstypes te bepalen om in uw gebiedsgroep te omvatten, zie de gids op [ bepalend douanegebieden in API ](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
                  },
                  "propertyType": {
                    "type": "string",
                    "title": "Property Type",
                    "description": "Type and primary use of property.",
                    "enum": [
                        "retail",
                        "yoga",
                        "fitness"
                    ],
                    "meta:enum": {
                        "retail": "Retail Store",
                        "yoga": "Yoga Studio",
                        "fitness": "Fitness Center"
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een lading met de details van de nieuwe veldgroep, inclusief de `$id` , `meta:altId` en `version` . Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
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
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Het uitvoeren van een verzoek van de GET aan [ lijst alle gebiedsgroepen ](#list) in de huurderscontainer zou nu de het gebiedsgroep van de Details van het Bezit omvatten, of u kunt [ een raadpleging (GET) verzoek ](#lookup) uitvoeren gebruikend URL-gecodeerde `$id` URI om de nieuwe gebiedsgroep direct te bekijken.

## Een veldgroep bijwerken {#put}

U kunt een volledige gebiedsgroep door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een gebiedsgroep door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die zouden worden vereist wanneer [ creërend een nieuwe gebiedsgroep ](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een gebiedsgroep wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [ het bijwerken van een gedeelte van een gebiedsgroep ](#patch).

**API formaat**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de veldgroep die u opnieuw wilt schrijven. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een bestaande veldgroep opnieuw geschreven en wordt een nieuw `propertyCountry` -veld toegevoegd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "propertyCountry": {
                    "title": "Property Country",
                    "description": "Country where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
                  },
                  "propertyType": {
                    "type": "string",
                    "title": "Property Type",
                    "description": "Type and primary use of property.",
                    "enum": [
                        "retail",
                        "yoga",
                        "fitness"
                    ],
                    "meta:enum": {
                        "retail": "Retail Store",
                        "yoga": "Yoga Studio",
                        "fitness": "Fitness Center"
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**Reactie**

Met een geslaagde reactie worden de details van de bijgewerkte veldgroep geretourneerd.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
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
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een gedeelte van een veldgroep bijwerken {#patch}

U kunt een gedeelte van een veldgroep bijwerken met een PATCH-aanvraag. [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add` , `remove` en `replace` . Voor meer informatie over Reparatie JSON, zie de [ API fundamentals gids ](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledig middel met nieuwe waarden in plaats van het bijwerken van individuele gebieden wilt vervangen, zie de sectie op [ het vervangen van een gebiedsgroep gebruikend een verrichting van de PUT ](#put).

**API formaat**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de veldgroep die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt de `description` van een bestaande veldgroep bijgewerkt en wordt een nieuw `propertyCity` -veld toegevoegd.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk voorwerp omvat uit te voeren verrichting (`op`), welk gebied de verrichting zou moeten worden uitgevoerd (`path`), en welke informatie in die verrichting (`value`) zou moeten worden omvat.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**Reactie**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. `description` is bijgewerkt en `propertyCountry` is toegevoegd onder `definitions` .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
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
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een veldgroep verwijderen {#delete}

Soms is het nodig een veldgroep uit het schemaregister te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met gebiedsgroep identiteitskaart uit te voeren die in de weg wordt verstrekt.

**API formaat**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de veldgroep die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door het verzoek van de a [ raadpleging (GET) ](#lookup) aan de gebiedsgroep te proberen. U moet een header `Accept` in de aanvraag opnemen, maar u moet de HTTP-status 404 (Niet gevonden) ontvangen omdat de veldgroep uit de schemaregistratie is verwijderd.
