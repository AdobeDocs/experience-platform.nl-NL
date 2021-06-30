---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Registry;field Group;Field group;Field groups;create
solution: Experience Platform
title: API-eindpunt voor veldgroepen
description: Het /fieldgroups eindpunt in de Registratie API van het Schema staat u toe om groepen van het XDM schemagebied binnen uw ervaringstoepassing programmatically te beheren.
topic-legacy: developer guide
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---


# Het eindpunt van schemaveldgroepen

De de gebiedsgroepen van het schema zijn herbruikbare componenten die één of meerdere gebieden bepalen die een bepaald concept, zoals een individuele persoon, een postadres, of een milieu van Webbrowser vertegenwoordigen. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Het `/fieldgroups` eindpunt in [!DNL Schema Registry] API staat u toe om gebiedsgroepen binnen uw ervaringstoepassing programmatically te beheren.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

## Een lijst met veldgroepen ophalen {#list}

U kunt alle veldgroepen weergeven onder de container `global` of `tenant` door een GET-aanvraag in te dienen bij `/global/fieldgroups` of `/tenant/fieldgroups`.

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [query parameters](./appendix.md#query) in het bijlage document voor meer informatie.

**API-indeling**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waaruit u veldgroepen wilt ophalen: `global` voor door Adobe gemaakte veldgroepen of `tenant` voor veldgroepen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie [appendix document](./appendix.md#query) voor een lijst van beschikbare parameters. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

De volgende aanvraag wint een lijst van gebiedsgroepen van de `tenant` container terug, gebruikend een `orderby` vraagparameter om de gebiedsgroepen door hun `title` attribuut te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de koptekst `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor het vermelden van gebiedsgroepen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-veldgroep voor elke bron, inclusief het origineel `$ref` en `allOf`. (Limiet: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

In de bovenstaande aanvraag is de `application/vnd.adobe.xed-id+json` `Accept`-header gebruikt. Daarom bevat de reactie alleen de `title`-, `$id`-, `meta:altId`- en `version`-kenmerken voor elke veldgroep. Als u de andere `Accept`-header (`application/vnd.adobe.xed+json`) gebruikt, worden alle kenmerken van elke veldgroep geretourneerd. Selecteer de juiste `Accept` header afhankelijk van de informatie die u in de reactie nodig hebt.

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

**API-indeling**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container die de veldgroep bevat die u wilt ophalen: `global` voor een door Adobe gemaakte veldgroep of `tenant` voor een veldgroep die eigendom is van uw organisatie. |
| `{FIELD_GROUP_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de veldgroep die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een veldgroep opgehaald op basis van de waarde `meta:altId` in het pad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de koptekst `Accept` die in de aanvraag wordt verzonden. Alle opzoekverzoeken vereisen een `version` in `Accept` kopbal worden omvat. De volgende `Accept` kopteksten zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Onbewerkt met `$ref` en `allOf` heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Ruwe met `$ref` en `allOf`, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, beschrijving inbegrepen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Als de reactie is geslaagd, worden de details van de veldgroep geretourneerd. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende `Accept` kopteksten om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

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
  "imsOrg": "{IMS_ORG}",
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

U kunt een aangepaste veldgroep definiëren onder de container `tenant` door een POST-aanvraag in te dienen.

**API-indeling**

```http
POST /tenant/fieldgroups
```

**Verzoek**

Wanneer u een nieuwe veldgroep definieert, moet deze een `meta:intendedToExtend`-kenmerk bevatten met een lijst van de `$id` van de klassen waarmee de veldgroep compatibel is. In dit voorbeeld is de veldgroep compatibel met een klasse `Property` die eerder is gedefinieerd. Aangepaste velden moeten worden genest onder `_{TENANT_ID}` (zoals in het voorbeeld wordt getoond) om conflicten met vergelijkbare velden te voorkomen die door klassen en andere veldgroepen worden verschaft.

>[!NOTE]
>
>Voor details op hoe te om verschillende gebiedstypes te bepalen om in uw gebiedsgroep te omvatten, zie [de gids van gebiedsbeperkingen](../schema/field-constraints.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de nieuwe veldgroep, inclusief `$id`, `meta:altId` en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry].

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
  "imsOrg": "{IMS_ORG}",
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

Als u een verzoek van de GET om alle veldgroepen [in de huurderscontainer te vermelden nu uitvoert, bevat dit de veldgroep Eigenschapdetails, of u kunt [een opzoekverzoek (GET) uitvoeren](#lookup) met de URL-gecodeerde `$id` URI om de nieuwe veldgroep direct weer te geven.](#list)

## Een veldgroep bijwerken {#put}

U kunt een volledige gebiedsgroep door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een gebiedsgroep door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die worden vereist wanneer [het creëren van een nieuwe gebiedsgroep](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een gebiedsgroep wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [het bijwerken van een gedeelte van een gebiedsgroep](#patch).

**API-indeling**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de veldgroep die u opnieuw wilt schrijven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In het volgende verzoek wordt een bestaande veldgroep opnieuw geschreven en wordt een nieuw veld `propertyCountry` toegevoegd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

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
  "imsOrg": "{IMS_ORG}",
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

U kunt een gedeelte van een veldgroep bijwerken met een PATCH-aanvraag. [!DNL Schema Registry] steunt alle standaardverrichtingen van het Reparatie JSON, met inbegrip van `add`, `remove`, en `replace`. Voor meer informatie over Reparatie JSON, zie [API fundamentals gids](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u de sectie over [het vervangen van een veldgroep met behulp van een PUT-bewerking](#put).

**API-indeling**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de veldgroep die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt `description` van een bestaande veldgroep bijgewerkt en wordt een nieuw veld `propertyCity` toegevoegd.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk object bevat de uit te voeren bewerking (`op`), in welk veld de bewerking moet worden uitgevoerd (`path`) en welke informatie in die bewerking moet worden opgenomen (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De `description` is bijgewerkt en `propertyCountry` is toegevoegd onder `definitions`.

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
  "imsOrg": "{IMS_ORG}",
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

**API-indeling**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de veldgroep die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door [lookup (GET) verzoek](#lookup) aan de gebiedsgroep te proberen. U zult een `Accept` kopbal in het verzoek moeten omvatten, maar zou een status 404 van HTTP (niet Gevonden) moeten ontvangen omdat de gebiedsgroep uit de Registratie van het Schema is verwijderd.