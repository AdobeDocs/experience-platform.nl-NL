---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Klasse Register;Schema Register;klasse;Klasse;klassen;Classes;create
solution: Experience Platform
title: Klassen API-eindpunt
description: Het /classes eindpunt in de Registratie API van het Schema staat u toe om klassen programmatically te beheren XDM binnen uw ervaringstoepassing.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 0%

---

# Klassen, eindpunt

Alle schema&#39;s van het Gegevensmodel van de Ervaring (XDM) moeten op een klasse worden gebaseerd. Een klasse bepaalt de basisstructuur van gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd moeten bevatten, evenals welke groepen van het schemagebied voor gebruik in die schema&#39;s geschikt zijn. Bovendien bepaalt de klasse van een schema de gedragsaspecten van de gegevens die een schema zal bevatten, waarvan er twee types zijn:

* **[!UICONTROL Record]**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **[!UICONTROL Time-series]**: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

>[!NOTE]
>
>Voor meer informatieklassen over gegevensgedrag in termen van hoe zij schemacompositie beïnvloeden, verwijs naar [grondbeginselen van de schemacompositie](../schema/composition.md).

De `/classes` in de [!DNL Schema Registry] Met API kunt u klassen programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een lijst met klassen ophalen {#list}

U kunt alle klassen weergeven onder de klasse `global` of `tenant` container door een GET-aanvraag in te dienen bij `/global/classes` of `/tenant/classes`, respectievelijk.

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [queryparameters](./appendix.md#query) voor meer informatie.

**API-indeling**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarvan u klassen wilt ophalen: `global` voor klassen die door Adobe zijn gemaakt of `tenant` voor klassen die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de [bijgevoegd document](./appendix.md#query) voor een lijst met beschikbare parameters. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een lijst met klassen opgehaald uit de `tenant` container gebruiken `orderby` query-parameter om de klassen op basis van hun te sorteren `title` kenmerk.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Het volgende `Accept` Kopteksten zijn beschikbaar voor aanbiedingsklassen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-klasse voor elke bron, met origineel `$ref` en `allOf` opgenomen. (Limiet: 300) |

{style="table-layout:auto"}

**Antwoord**

In bovengenoemd verzoek werd gebruikgemaakt van de `application/vnd.adobe.xed-id+json` `Accept` header, daarom bevat de reactie alleen de `title`, `$id`, `meta:altId`, en `version` kenmerken voor elke klasse. Het andere gebruiken `Accept` header (`application/vnd.adobe.xed+json`) retourneert alle kenmerken van elke klasse. Selecteer de juiste `Accept` afhankelijk van de informatie die u in uw reactie nodig hebt.

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

**API-indeling**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container die de klasse bevat die u wilt ophalen: `global` voor een door Adobe gemaakte klasse of `tenant` voor een klasse die eigendom is van uw organisatie. |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerd `$id` van de klasse die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een klasse opgehaald op basis van `meta:altId` waarde opgegeven in het pad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Alle opzoekverzoeken vereisen een `version` worden opgenomen in de `Accept` header. Het volgende `Accept` Kopteksten zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkt met `$ref` en `allOf`, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` en `allOf` heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkt met `$ref` en `allOf`, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` en `allOf` opgelost, beschrijving inbegrepen. |

{style="table-layout:auto"}

**Antwoord**

Een geslaagde reactie retourneert de details van de klasse. De geretourneerde velden zijn afhankelijk van de `Accept` in de aanvraag verzonden. Experimenteer met andere `Accept` Kopteksten om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

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

U kunt een aangepaste klasse definiëren onder de categorie `tenant` door een POST aan te vragen.

>[!IMPORTANT]
>
>Wanneer u een schema samenstelt dat is gebaseerd op een aangepaste klasse die u definieert, kunt u geen standaardveldgroepen gebruiken. Elke veldgroep definieert met welke klassen ze compatibel zijn `meta:intendedToExtend` kenmerk. Wanneer u begint met het definiëren van veldgroepen die compatibel zijn met uw nieuwe klasse (door het gereedschap `$id` van uw nieuwe klasse in `meta:intendedToExtend` (veld van de veldgroep), kunt u deze veldgroepen telkens opnieuw gebruiken wanneer u een schema definieert dat de door u gedefinieerde klasse implementeert. Zie de secties op [maken, veldgroepen](./field-groups.md#create) en [schema&#39;s maken](./schemas.md#create) in hun respectieve eindpuntgidsen voor meer informatie.
>
>Als u schema&#39;s wilt gebruiken die op douaneklassen in het Profiel van de Klant in real time worden gebaseerd, is het ook belangrijk om in mening te houden dat de verenigingsschema&#39;s slechts gebaseerd op schema&#39;s zijn die de zelfde klasse delen. Als u een schema van de douane-klasse in de unie voor een andere klasse wilt omvatten zoals [!UICONTROL XDM Individual Profile] of [!UICONTROL XDM ExperienceEvent], moet u een verband met een ander schema vestigen dat die klasse aanwendt. Zie de zelfstudie aan [het tot stand brengen van een verband tussen twee schema&#39;s in API](../tutorials/relationship-api.md) voor meer informatie .

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

De aanvraag om een klasse te maken (POST) moet een klasse bevatten met een `allOf` kenmerk met een `$ref` tot één van twee waarden: `https://ns.adobe.com/xdm/data/record` of `https://ns.adobe.com/xdm/data/time-series`. Deze waarden vertegenwoordigen het gedrag waarop de klasse is gebaseerd (record- of tijdreeks, respectievelijk). Zie de sectie over gedragstypen in de [grondbeginselen van de schemacompositie](../schema/composition.md).

Wanneer u een klasse definieert, kunt u ook veldgroepen of aangepaste velden opnemen in de klassendefinitie. Hierdoor worden de toegevoegde veldgroepen en velden opgenomen in alle schema&#39;s die de klasse implementeren. In het volgende voorbeeldverzoek wordt een klasse met de naam &quot;Eigenschap&quot; gedefinieerd, die informatie vastlegt over verschillende eigenschappen die eigendom zijn van en worden beheerd door een bedrijf. Het omvat een `propertyId` veld dat moet worden opgenomen telkens wanneer de klasse wordt gebruikt.

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
| `_{TENANT_ID}` | De `TENANT_ID` naamruimte voor uw organisatie. Alle die middelen door uw organisatie worden gecreeerd moeten dit bezit omvatten om botsingen met andere middelen in te vermijden [!DNL Schema Registry]. |
| `allOf` | Een lijst met bronnen waarvan de eigenschappen door de nieuwe klasse moeten worden overgeërfd. Een van de `$ref` objecten binnen de array definiëren het gedrag van de klasse. In dit voorbeeld overerft de klasse het gedrag &#39;record&#39;. |

{style="table-layout:auto"}

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de zojuist gemaakte klasse, inclusief de `$id`, `meta:altId`, en `version`. Deze drie waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry].

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

Een GET-aanvraag uitvoeren op [lijst alle klassen](#list) in de `tenant` container zou nu de klasse Property bevatten. U kunt ook [een opzoekverzoek (GET) uitvoeren](#lookup) URL-gecodeerd gebruiken `$id` om de nieuwe klasse rechtstreeks weer te geven.

## Een klasse bijwerken {#put}

U kunt een volledige klasse door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een klasse door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die wanneer zouden worden vereist [een nieuwe klasse maken](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een klasse wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [het bijwerken van een gedeelte van een klasse](#patch).

**API-indeling**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `meta:altId` of URL-gecodeerd `$id` van de klasse die u opnieuw wilt schrijven. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een bestaande klasse opnieuw geschreven, waarbij de klasse wordt gewijzigd `description` en de `title` van een van de velden.

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

U kunt een deel van een klasse bijwerken door een verzoek van PATCH te gebruiken. De [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add`, `remove`, en `replace`. Voor meer informatie over JSON Patch raadpleegt u de [Handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u de sectie over [het vervangen van een klasse die een verrichting van de PUT gebruikt](#put).

**API-indeling**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van de klasse die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

Met de onderstaande voorbeeldaanvraag wordt het `description` van een bestaande klasse, en `title` van een van de velden.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk object bevat de uit te voeren bewerking (`op`), welk veld de bewerking moet worden uitgevoerd (`path`) en welke informatie in die operatie moet worden opgenomen (`value`).

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

**Antwoord**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De `description` samen met de `title` van de `propertyId` veld.

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

**API-indeling**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van de klasse die u wilt verwijderen. |

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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de verwijdering bevestigen door een [opzoekverzoek (GET)](#lookup) voor de klasse. U moet een `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the class has been removed from the Schema Registry.
