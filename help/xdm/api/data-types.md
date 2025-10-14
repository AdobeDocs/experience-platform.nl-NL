---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Data Type Register;Schema Register;Gegevenstype;Gegevenstype;Gegevenstypen;Gegevenstypen;Maken
solution: Experience Platform
title: API-eindpunt voor gegevenstypen
description: Het /datatypes eindpunt in de Registratie API van het Schema staat u toe om gegevenstypes programmatically te beheren XDM binnen uw ervaringstoepassing.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Gegevenstypen eindpunt

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als velden van het verwijzingstype in klassen of schemaveldgroepen. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Hoewel gelijkaardig aan gebiedsgroepen in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de gebiedsgroepen slechts op het wortelniveau kunnen worden toegevoegd. Met het eindpunt `/datatypes` in de [!DNL Schema Registry] API kunt u gegevenstypen programmatisch beheren binnen uw ervaringstoepassing.

>[!NOTE]
>
>Als een veld is gedefinieerd als een specifiek gegevenstype, kunt u niet hetzelfde veld met een ander gegevenstype in een ander schema maken. Deze beperking geldt voor de huurder van uw organisatie.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met gegevenstypen ophalen {#list}

U kunt alle gegevenstypen weergeven onder de container `global` of `tenant` door een GET-aanvraag in te dienen bij respectievelijk `/global/datatypes` of `/tenant/datatypes` .

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [&#x200B; vraagparameters &#x200B;](./appendix.md#query) in het bijlage document voor meer informatie.

**API formaat**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarvan u gegevenstypen wilt ophalen: `global` voor gegevenstypen die zijn gemaakt met een Adobe of `tenant` voor gegevenstypen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie het [&#x200B; bijlage document &#x200B;](./appendix.md#query) voor een lijst van beschikbare parameters. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een lijst met gegevenstypen opgehaald uit de `tenant` -container. Hierbij wordt een `orderby` query-parameter gebruikt om de gegevenstypen op hun `title` -kenmerk te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` headers zijn beschikbaar voor gegevenstypen van lijsten:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-gegevenstype voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

In de bovenstaande aanvraag is de header `application/vnd.adobe.xed-id+json` `Accept` gebruikt en daarom bevat de reactie alleen de kenmerken `title` , `$id` , `meta:altId` en `version` voor elk gegevenstype. Wanneer u de andere `Accept` header (`application/vnd.adobe.xed+json` ) gebruikt, worden alle kenmerken van elk gegevenstype geretourneerd. Selecteer de juiste `Accept` header, afhankelijk van de informatie die u in uw reactie nodig hebt.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Een gegevenstype opzoeken {#lookup}

U kunt een specifiek gegevenstype opzoeken door identiteitskaart van het gegevenstype in de weg van een verzoek van de GET op te nemen.

**API formaat**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin het gegevenstype is opgeslagen dat u wilt ophalen: `global` voor een door Adobe gemaakt gegevenstype of `tenant` voor een gegevenstype dat eigendom is van uw organisatie. |
| `{DATA_TYPE_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het gegevenstype dat u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een gegevenstype opgehaald op basis van de `meta:altId` -waarde die in het pad is opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Voor alle opzoekverzoeken moet een `version` worden opgenomen in de `Accept` -koptekst. De volgende `Accept` headers zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Met `$ref` en `allOf` heeft Raw titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` en `allOf` resolve, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkt met `$ref` en `allOf` , geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` en `allOf` opgelost, inclusief beschrijvingen. |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert de details van het gegevenstype. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende kopteksten van `Accept` om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een gegevenstype maken {#create}

U kunt een aangepast gegevenstype definiëren onder de `tenant` -container door een POST aan te vragen.

**API formaat**

```http
POST /tenant/datatypes
```

**Verzoek**

In tegenstelling tot veldgroepen vereist het definiëren van een gegevenstype niet dat `meta:extends` - of `meta:intendedToExtend` -velden zijn vereist. Velden hoeven ook niet te zijn genest om conflicten te voorkomen.

Wanneer u de veldstructuur van het gegevenstype zelf definieert, kunt u primitieve typen gebruiken (zoals `string` of `object` ) of kunt u naar andere bestaande gegevenstypen verwijzen via `$ref` -kenmerken. Zie de gids op [&#x200B; bepalend douaneXDM gebieden in API &#x200B;](../tutorials/custom-fields-api.md) voor gedetailleerde begeleiding op het verwachte formaat voor verschillende XDM gebiedstypes.

Met de volgende aanvraag wordt een gegevenstype &quot;Property Construction&quot; gemaakt met subeigenschappen `yearBuilt` , `propertyType` en `location` :

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van het nieuwe gegevenstype, inclusief `$id` , `meta:altId` en `version` . Deze drie waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Het uitvoeren van een verzoek van de GET aan [&#x200B; lijst alle gegevenstypes &#x200B;](#list) in de huurderscontainer zou nu het gegevenstype van de Details van het Bezit omvatten, of u kunt [&#x200B; een raadpleging (GET) verzoek &#x200B;](#lookup) uitvoeren gebruikend URL-Gecodeerde `$id` URI om het nieuwe gegevenstype direct te bekijken.

## Een gegevenstype bijwerken {#put}

U kunt een volledig gegevenstype door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een gegevenstype door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die zouden worden vereist wanneer [&#x200B; creërend een nieuw gegevenstype &#x200B;](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een gegevenstype wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [&#x200B; het bijwerken van een gedeelte van een gegevenstype &#x200B;](#patch).

**API formaat**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_TYPE_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het gegevenstype dat u opnieuw wilt schrijven. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een bestaand gegevenstype opnieuw geschreven en wordt een nieuw veld `floorSize` toegevoegd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Reactie**

Een geslaagde reactie retourneert de details van het bijgewerkte gegevenstype.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een gedeelte van een gegevenstype bijwerken {#patch}

U kunt een gedeelte van een gegevenstype bijwerken door een verzoek van PATCH te gebruiken. [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add` , `remove` en `replace` . Voor meer informatie over Reparatie JSON, zie de [&#x200B; API fundamentals gids &#x200B;](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledig middel met nieuwe waarden in plaats van het bijwerken van individuele gebieden wilt vervangen, zie de sectie op [&#x200B; het vervangen van een gegevenstype gebruikend een verrichting van de PUT &#x200B;](#put).

**API formaat**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_TYPE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het gegevenstype dat u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt de `description` van een bestaand gegevenstype bijgewerkt en wordt een nieuw `floorSize` -veld toegevoegd.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk voorwerp omvat uit te voeren verrichting (`op`), welk gebied de verrichting zou moeten worden uitgevoerd (`path`), en welke informatie in die verrichting (`value`) zou moeten worden omvat.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Reactie**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. `description` is bijgewerkt en `floorSize` is toegevoegd onder `definitions` .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
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

## Een gegevenstype verwijderen {#delete}

Het kan soms noodzakelijk zijn om een gegevenstype uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met gegevenstype identiteitskaart uit te voeren die in de weg wordt verstrekt.

**API formaat**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_TYPE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het gegevenstype dat u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door het verzoek van de a [&#x200B; raadpleging (GET) &#x200B;](#lookup) aan het gegevenstype te proberen. U moet een header `Accept` in de aanvraag opnemen, maar u moet de HTTP-status 404 (Niet gevonden) ontvangen omdat het gegevenstype is verwijderd uit de schemaregistratie.
