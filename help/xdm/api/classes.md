---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Klasse Register;Schema Register;klasse;Klasse;klassen;Classes;create
solution: Experience Platform
title: Klassen-API-eindpunt
description: Het /classes eindpunt in de Registratie API van het Schema staat u toe om klassen programmatically te beheren XDM binnen uw ervaringstoepassing.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 0%

---

# Klassen, eindpunt

Alle schema&#39;s van het Gegevensmodel van de Ervaring (XDM) moeten op een klasse worden gebaseerd. Een klasse bepaalt de basisstructuur van gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd moeten bevatten, evenals welke groepen van het schemagebied voor gebruik in die schema&#39;s geschikt zijn. Bovendien bepaalt de klasse van een schema de gedragsaspecten van de gegevens die een schema zal bevatten, waarvan er twee types zijn:

* **[!UICONTROL Record]**: biedt informatie over de kenmerken van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **[!UICONTROL Time-series]**: biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

>[!NOTE]
>
>Voor meer informatieklassen over gegevensgedrag in termen van hoe zij schemacompositie beïnvloeden, verwijs naar de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../schema/composition.md).

Met het eindpunt `/classes` in de [!DNL Schema Registry] API kunt u klassen programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met klassen ophalen {#list}

U kunt alle klassen onder de container `global` of `tenant` weergeven door een aanvraag voor een GET in te dienen bij respectievelijk `/global/classes` of `/tenant/classes` .

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [&#x200B; vraagparameters &#x200B;](./appendix.md#query) in het bijlage document voor meer informatie.

**API formaat**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarvan u klassen wilt ophalen: `global` voor klassen die zijn gemaakt met een Adobe of `tenant` voor klassen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie het [&#x200B; bijlage document &#x200B;](./appendix.md#query) voor een lijst van beschikbare parameters. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een lijst met klassen opgehaald uit de container `tenant` . Hierbij wordt een `orderby` query-parameter gebruikt om de klassen op hun `title` -kenmerk te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` headers zijn beschikbaar voor aanbiedingsklassen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-klasse voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

In de bovenstaande aanvraag is de header `application/vnd.adobe.xed-id+json` `Accept` gebruikt en daarom bevat de reactie alleen de kenmerken `title` , `$id` , `meta:altId` en `version` voor elke klasse. Wanneer u de andere `Accept` header (`application/vnd.adobe.xed+json` ) gebruikt, worden alle kenmerken van elke klasse geretourneerd. Selecteer de juiste `Accept` header, afhankelijk van de informatie die u in uw reactie nodig hebt.

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

## Een klasse opzoeken {#lookup}

U kunt een specifieke klasse opzoeken door de id van de klasse op te nemen in het pad van een GET-aanvraag.

**API formaat**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container die de klasse bevat die u wilt ophalen: `global` voor een klasse die is gemaakt met een Adobe of `tenant` voor een klasse die eigendom is van uw organisatie. |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de klasse die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een klasse opgehaald op basis van de `meta:altId` -waarde die in het pad is opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Een geslaagde reactie retourneert de details van de klasse. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende kopteksten van `Accept` om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

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
  "imsOrg":"{ORG_ID}",
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

## Een klasse maken {#create}

U kunt een aangepaste klasse definiëren onder de `tenant` -container door een POST aan te vragen.

>[!IMPORTANT]
>
>Wanneer u een schema samenstelt dat is gebaseerd op een aangepaste klasse die u definieert, kunt u geen standaardveldgroepen gebruiken. Elke veldgroep definieert de klassen waarmee ze compatibel zijn in het kenmerk `meta:intendedToExtend` . Wanneer u begint met het definiëren van veldgroepen die compatibel zijn met uw nieuwe klasse (met behulp van `$id` van de nieuwe klasse in het veld `meta:intendedToExtend` van de veldgroep), kunt u deze veldgroepen telkens opnieuw gebruiken wanneer u een schema definieert dat de door u gedefinieerde klasse implementeert. Zie de secties op [&#x200B; creërend gebiedsgroepen &#x200B;](./field-groups.md#create) en [&#x200B; creërend schema&#39;s &#x200B;](./schemas.md#create) in hun respectieve eindpuntgidsen voor meer informatie.
>
>Als u schema&#39;s wilt gebruiken die op douaneklassen in het Profiel van de Klant in real time worden gebaseerd, is het ook belangrijk om in mening te houden dat de verenigingsschema&#39;s slechts gebaseerd op schema&#39;s zijn die de zelfde klasse delen. Als u een schema van de douane-klasse in de unie voor een andere klasse zoals [!UICONTROL XDM Individual Profile] of [!UICONTROL XDM ExperienceEvent] wilt omvatten, moet u een verband met een ander schema vestigen dat die klasse gebruikt. Zie het leerprogramma op [&#x200B; het vestigen van een verband tussen twee schema&#39;s in API &#x200B;](../tutorials/relationship-api.md) voor meer informatie.

**API formaat**

```http
POST /tenant/classes
```

**Verzoek**

De aanvraag om een klasse te maken (POST) moet een `allOf` -kenmerk bevatten met een `$ref` naar een van de volgende twee waarden: `https://ns.adobe.com/xdm/data/record` of `https://ns.adobe.com/xdm/data/time-series` . Deze waarden vertegenwoordigen het gedrag waarop de klasse is gebaseerd (record- of tijdreeks, respectievelijk). Voor meer informatie over de verschillen tussen verslaggegevens en tijdreeksgegevens, zie de sectie over gedragstypes binnen de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../schema/composition.md).

Wanneer u een klasse definieert, kunt u ook veldgroepen of aangepaste velden opnemen in de klassendefinitie. Hierdoor worden de toegevoegde veldgroepen en velden opgenomen in alle schema&#39;s die de klasse implementeren. In het volgende voorbeeldverzoek wordt een klasse met de naam &quot;Eigenschap&quot; gedefinieerd, die informatie vastlegt over verschillende eigenschappen die eigendom zijn van en worden beheerd door een bedrijf. De klasse bevat een `propertyId` -veld dat moet worden opgenomen telkens wanneer de klasse wordt gebruikt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | De naamruimte `TENANT_ID` voor uw organisatie. Alle bronnen die door uw organisatie worden gemaakt, moeten deze eigenschap bevatten om conflicten met andere bronnen in de [!DNL Schema Registry] te voorkomen. |
| `allOf` | Een lijst met bronnen waarvan de eigenschappen door de nieuwe klasse moeten worden overgeërfd. Een van de `$ref` -objecten in de array definieert het gedrag van de klasse. In dit voorbeeld overerft de klasse het gedrag &#39;record&#39;. |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de nieuwe klasse, inclusief de `$id` , `meta:altId` en `version` . Deze drie waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

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
  "imsOrg": "{ORG_ID}",
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

Het uitvoeren van een verzoek van de GET aan [&#x200B; lijst alle klassen &#x200B;](#list) in de `tenant` container zou nu de klasse van het Bezit omvatten. U kunt ook [&#x200B; een raadpleging (GET) verzoek &#x200B;](#lookup) uitvoeren gebruikend URL-Gecodeerd `$id` om de nieuwe klasse direct te bekijken.

## Een klasse bijwerken {#put}

U kunt een volledige klasse door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een klasse door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die zouden worden vereist wanneer [&#x200B; creërend een nieuwe klasse &#x200B;](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een klasse wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [&#x200B; het bijwerken van een gedeelte van een klasse &#x200B;](#patch).

**API formaat**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de klasse die u opnieuw wilt schrijven. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een bestaande klasse opnieuw geschreven, waarbij de waarden `description` en `title` van een van de velden worden gewijzigd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

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
  "imsOrg": "{ORG_ID}",
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

## Een gedeelte van een klasse bijwerken {#patch}

U kunt een deel van een klasse bijwerken door een verzoek van PATCH te gebruiken. [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add` , `remove` en `replace` . Voor meer informatie over Reparatie JSON, zie de [&#x200B; API fundamentals gids &#x200B;](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledig middel met nieuwe waarden in plaats van het bijwerken van individuele gebieden wilt vervangen, zie de sectie op [&#x200B; het vervangen van een klasse gebruikend een verrichting van de PUT &#x200B;](#put).

**API formaat**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de klasse die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

In de onderstaande voorbeeldaanvraag worden de `description` van een bestaande klasse en de `title` van een van de velden bijgewerkt.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk voorwerp omvat uit te voeren verrichting (`op`), welk gebied de verrichting zou moeten worden uitgevoerd (`path`), en welke informatie in die verrichting (`value`) zou moeten worden omvat.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Reactie**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De `description` is samen met de `title` van het `propertyId` veld bijgewerkt.

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
  "imsOrg": "{ORG_ID}",
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

## Een klasse verwijderen {#delete}

Het kan soms nodig zijn om een klasse uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met klassenidentiteitskaart uit te voeren die in de weg wordt verstrekt.

**API formaat**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de klasse die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door a [&#x200B; raadpleging (GET) verzoek &#x200B;](#lookup) voor de klasse te proberen. U moet een header `Accept` in de aanvraag opnemen, maar u moet de HTTP-status 404 (Niet gevonden) ontvangen omdat de klasse uit de schemaregistratie is verwijderd.
