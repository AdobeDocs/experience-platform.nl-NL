---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een bron bijwerken
topic: developer guide
translation-type: tm+mt
source-git-commit: 0d3bee939226d9ef4ac1672b71e0d240f32c5dcf

---


# Een bron bijwerken

U kunt middelen in de huurderscontainer wijzigen of bijwerken gebruikend een verzoek van de PATCH. Het register van het Schema steunt alle standaard verrichtingen van de Reparatie JSON, met inbegrip van toevoegen, verwijderen en vervangen.

Raadpleeg de officiële [JSON Patch-documentatie](http://jsonpatch.com/)voor meer informatie over JSON Patch, inclusief beschikbare bewerkingen.

>[!NOTE] Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u het document over het [vervangen van een bron met behulp van een PUT-bewerking](replace-resource.md).

## Mengsels toevoegen aan een schema

Één van de gemeenschappelijkste verrichtingen van de PATCH impliceert het toevoegen van eerder bepaalde mengelingen aan een schema XDM, zoals aangetoond door het hieronder voorbeeld.

**API-indeling**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_TYPE}` | Het type bron dat vanuit de Schemabibliotheek moet worden bijgewerkt. Geldige typen zijn `datatypes`, `mixins`, `schemas`en `classes`. |
| `{RESOURCE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de bron. |

**Verzoek**

Met behulp van een PATCH-bewerking kunt u een schema bijwerken en velden opnemen die zijn gedefinieerd in een eerder gemaakte mix. Hiervoor moet u een PATCH-aanvraag naar het schema uitvoeren met behulp van de URL `meta:altId` of de URL-gecodeerde `$id` URI.

De aanvraaginstantie bevat de bewerking (`op`) die u wilt uitvoeren, waarbij (`path`) u de bewerking wilt uitvoeren en welke informatie (`value`) u in de bewerking wilt opnemen. In dit voorbeeld wordt de `$id` waarde van de mix toegevoegd aan zowel de `meta:extends` als de `allOf` velden voor het doelschema.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**Antwoord**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De mix `$id` is toegevoegd aan de `meta:extends` array en er wordt`$ref`nu een verwijzing ( `$id` ) naar de mix in de `allOf` array weergegeven.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Afzonderlijke velden voor een bron bijwerken

U kunt PATCH- verzoeken ook verzenden die veelvoudige veranderingen in individuele gebieden binnen een middel van de Registratie van het Schema aanbrengen.

**API-indeling**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_TYPE}` | Het type bron dat vanuit de Schemabibliotheek moet worden bijgewerkt. Geldige typen zijn `datatypes`, `mixins`, `schemas`en `classes`. |
| `{RESOURCE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de bron. |

**Verzoek**

De aanvraaginstantie bevat de bewerking (`op`), locatie (`path`) en informatie (`value`) die nodig is om de mix bij te werken. Dit verzoek werkt de mengsel van de Details van het Bezit bij om het &quot;propertyCity&quot;gebied te verwijderen en een nieuw &quot;propertyAddress&quot;gebied toe te voegen dat een standaardgegevenstype verwijzingen dat adresinformatie bevat. Er wordt ook een nieuw veld E-mailadres toegevoegd dat verwijst naar een standaardgegevenstype met e-mailgegevens.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Antwoord**

Een succesvol antwoord laat zien dat de bewerkingen zijn voltooid omdat de nieuwe velden aanwezig zijn en het veld &quot;propertyCity&quot; is verwijderd.

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
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
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
