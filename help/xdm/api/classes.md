---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Een klasse maken
description: Het /classes eindpunt in de Registratie API van het Schema staat u toe om klassen programmatically te beheren XDM binnen uw ervaringstoepassing.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# Klassen, eindpunt

Alle schema&#39;s van het Gegevensmodel van de Ervaring (XDM) moeten op een klasse worden gebaseerd. Een klasse bepaalt de basisstructuur van gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd moeten bevatten, evenals welke mengen geschikt voor gebruik in die schema&#39;s zijn. Bovendien bepaalt de klasse van een schema de gedragsaspecten van de gegevens die een schema zal bevatten, waarvan er twee types zijn:

* **[!UICONTROL Opnemen]**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **[!UICONTROL Tijdreeks]**: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

>[!NOTE]
>
>Voor meer informatieklassen over gegevensgedrag in termen van hoe zij schemacompositie beïnvloeden, verwijs naar [grondbeginselen van schemacompositie](../schema/composition.md).

Het `/classes` eindpunt in [!DNL Schema Registry] API staat u toe om klassen binnen uw ervaringstoepassing programmatically te beheren.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

## Een lijst met klassen {#list} ophalen

U kunt alle klassen weergeven onder de container `global` of `tenant` door een GET-aanvraag in te dienen bij `/global/classes` of `/tenant/classes`.

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [query parameters](./appendix.md#query) in het bijlage document voor meer informatie.

**API-indeling**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarvan u klassen wilt ophalen: `global` voor klassen die met Adobe zijn gemaakt of `tenant` voor klassen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie [appendix document](./appendix.md#query) voor een lijst van beschikbare parameters. |

**Verzoek**

Het volgende verzoek wint een lijst van klassen van de `tenant` container terug, gebruikend een `orderby` vraagparameter om de klassen door hun `title` attribuut te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de koptekst `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor lijstklassen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-klasse voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

**Antwoord**

In de bovenstaande aanvraag is de `application/vnd.adobe.xed-id+json` `Accept`-header gebruikt. Daarom bevat de reactie alleen de `title`-, `$id`-, `meta:altId`- en `version`-kenmerken voor elke klasse. Als u de andere `Accept`-header (`application/vnd.adobe.xed+json`) gebruikt, worden alle kenmerken van elke klasse geretourneerd. Selecteer de juiste `Accept` header afhankelijk van de informatie die u in de reactie nodig hebt.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Een klasse {#lookup} opzoeken

U kunt een specifieke klasse opzoeken door de id van de klasse op te nemen in het pad van een GET-aanvraag.

**API-indeling**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container die de klasse bevat die u wilt ophalen: `global` voor een door Adobe gemaakte klasse of `tenant` voor een klasse die eigendom is van uw organisatie. |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de klasse die u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt een klasse opgehaald op basis van de waarde `meta:altId` in het pad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de koptekst `Accept` die in de aanvraag wordt verzonden. Alle opzoekverzoeken vereisen een `version` worden opgenomen in de `Accept` koptekst. De volgende `Accept` kopteksten zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Onbewerkt met `$ref` en `allOf` heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Ruwe met `$ref` en `allOf`, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` en  `allOf` opgelost, beschrijving inbegrepen. |

**Antwoord**

Een geslaagde reactie retourneert de details van de klasse. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende `Accept` kopteksten om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Een klasse {#create} maken

U kunt een aangepaste klasse definiëren onder de container `tenant` door een POST-aanvraag in te dienen.

>[!IMPORTANT]
>
>Wanneer het samenstellen van een schema dat op een douaneklasse wordt gebaseerd die u bepaalt, zult u geen standaardmengen kunnen gebruiken. Elke mix definieert de klassen waarmee ze compatibel zijn in hun `meta:intendedToExtend`-kenmerk. Zodra u begint bepalend mengen die met uw nieuwe klasse (door `$id` van uw nieuwe klasse in het `meta:intendedToExtend` gebied van de mix te gebruiken) compatibel zijn, zult u die mixins kunnen opnieuw gebruiken telkens als u een schema bepaalt dat de klasse uitvoert u bepaalde. Zie de secties op [het creëren van mixins](./mixins.md#create) en [het creëren van schema&#39;s](./schemas.md#create) in hun respectieve eindpuntgidsen voor meer informatie.
>
>Als u schema&#39;s wilt gebruiken die op douaneklassen in het Profiel van de Klant in real time worden gebaseerd, is het ook belangrijk om in mening te houden dat de verenigingsschema&#39;s slechts gebaseerd op schema&#39;s zijn die de zelfde klasse delen. Als u een douane-klasse schema in de unie voor een andere klasse zoals [!UICONTROL XDM Individueel Profiel] of [!UICONTROL XDM ExperienceEvent] wilt omvatten, moet u een verhouding met een ander schema vestigen dat die klasse aanwendt. Zie de zelfstudie over [het bepalen van een relatie tussen twee schema&#39;s in API](../tutorials/relationship-api.md) voor meer informatie.

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

De aanvraag om een klasse te maken (POST) moet een `allOf`-kenmerk bevatten dat een `$ref` tot een van twee waarden bevat: `https://ns.adobe.com/xdm/data/record` of `https://ns.adobe.com/xdm/data/time-series`. Deze waarden vertegenwoordigen het gedrag waarop de klasse is gebaseerd (record- of tijdreeks, respectievelijk). Voor meer informatie over de verschillen tussen verslaggegevens en tijdreeksgegevens, zie de sectie over gedragstypes binnen de [grondbeginselen van schemacompositie](../schema/composition.md).

Wanneer u een klasse definieert, kunt u ook mixins of aangepaste velden opnemen in de klassendefinitie. Hierdoor worden de toegevoegde mixins en velden opgenomen in alle schema&#39;s die de klasse implementeren. In het volgende voorbeeldverzoek wordt een klasse met de naam &quot;Eigenschap&quot; gedefinieerd, die informatie vastlegt over verschillende eigenschappen die eigendom zijn van en worden beheerd door een bedrijf. Het bevat een veld `propertyId` dat moet worden opgenomen telkens wanneer de klasse wordt gebruikt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `_{TENANT_ID}` | De naamruimte `TENANT_ID` voor uw organisatie. Alle middelen die door uw organisatie worden gecreeerd moeten dit bezit omvatten om botsingen met andere middelen in [!DNL Schema Registry] te vermijden. |
| `allOf` | Een lijst met bronnen waarvan de eigenschappen door de nieuwe klasse moeten worden overgeërfd. Een van de `$ref`-objecten in de array definieert het gedrag van de klasse. In dit voorbeeld overerft de klasse het gedrag &#39;record&#39;. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de nieuwe klasse, zoals `$id`, `meta:altId` en `version`. Deze drie waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Wanneer u een GET-aanvraag uitvoert om alle klassen [weer te geven in de container `tenant`, wordt nu de klasse Property opgenomen. ](#list) U kunt [een raadpleging (GET) verzoek ](#lookup) ook uitvoeren gebruikend URL-Gecodeerd `$id` om de nieuwe klasse direct te bekijken.

## Een klasse {#put} bijwerken

U kunt een volledige klasse door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een klasse door een PUT verzoek, moet het lichaam alle gebieden omvatten die wanneer [het creëren van een nieuwe klasse](#create) in een POST verzoek worden vereist.

>[!NOTE]
>
>Als u slechts een deel van een klasse wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [het bijwerken van een gedeelte van een klasse](#patch).

**API-indeling**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de klasse u wilt herschrijven. |

**Verzoek**

In het volgende verzoek wordt een bestaande klasse opnieuw geschreven, waarbij de `description` en `title` van een van de velden worden gewijzigd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de bijgewerkte klasse.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Een gedeelte van een klasse {#patch} bijwerken

U kunt een deel van een klasse bijwerken door een verzoek van PATCH te gebruiken. [!DNL Schema Registry] steunt alle standaardverrichtingen van het Reparatie JSON, met inbegrip van `add`, `remove`, en `replace`. Voor meer informatie over Reparatie JSON, zie [API fundamentals gids](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u de sectie over [het vervangen van een klasse met een PUT-bewerking](#put).

**API-indeling**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de klasse u wilt bijwerken. |

**Verzoek**

In de onderstaande voorbeeldaanvraag worden `description` van een bestaande klasse en `title` van een van de velden bijgewerkt.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk object bevat de uit te voeren bewerking (`op`), in welk veld de bewerking moet worden uitgevoerd (`path`) en welke informatie in die bewerking moet worden opgenomen (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Antwoord**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De `description` is bijgewerkt, samen met `title` van het `propertyId` gebied.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Een klasse {#delete} verwijderen

Het kan soms nodig zijn om een klasse uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met klassenidentiteitskaart uit te voeren die in de weg wordt verstrekt.

**API-indeling**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de klasse die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door [lookup (GET) verzoek](#lookup) voor de klasse te proberen. U zult een `Accept` kopbal in het verzoek moeten omvatten, maar zou een status 404 van HTTP (niet Gevonden) moeten ontvangen omdat de klasse uit de Registratie van het Schema is verwijderd.