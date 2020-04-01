---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een mix maken
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8

---


# Een mix maken

Mixins zijn een set velden die worden gebruikt om een bepaald concept te beschrijven, zoals &quot;adres&quot; of &quot;profielvoorkeuren&quot;. Er zijn talrijke standaardmixins beschikbaar, of u kunt uw bepalen wanneer u wenst om informatie te vangen die voor uw organisatie uniek is. Elke mix bevat een `meta:intendedToExtend` veld met de klassen waarmee de mix compatibel is.

Het kan handig zijn om alle beschikbare combinaties te bekijken om uzelf bekend te maken met de velden die in de verschillende combinaties zijn opgenomen. U kunt (KRIJGEN) van alle mengen een lijst maken compatibel met een bepaalde klasse door een verzoek tegen elk van de &quot;globale&quot;en &quot;huurder&quot;containers uit te voeren, die slechts die mengen terugkeren waar het &quot;meta:intendedToExtend&quot;gebied de klasse aanpast u gebruikt. De voorbeelden hieronder zullen alle mengen terugkeren die met de individuele klasse van het Profiel XDM kunnen worden gebruikt:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

Het voorbeeld API verzoek leidt hieronder tot een nieuwe mengeling in de huurderscontainer.

**API-indeling**

```http
POST /tenant/mixins
```

**Verzoek**

Wanneer u een nieuwe mix definieert, moet deze een `meta:intendedToExtend` kenmerk bevatten met een overzicht `$id` van de klassen waarmee de mix compatibel is. In dit voorbeeld is de mix compatibel met de klasse Property die u eerder hebt gedefinieerd. Aangepaste velden moeten onder `_{TENANT_ID}` (zoals in het voorbeeld) worden genest om conflicten met andere combinaties of velden uit de klasseschema&#39;s te voorkomen. Het `propertyConstruction` veld is een verwijzing naar het gegevenstype dat in de vorige aanroep is gemaakt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
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

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de zojuist gemaakte mix, inclusief de combinatie `$id`, `meta:altId`en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door het schemaregister.

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
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
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
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Het uitvoeren van een GET verzoek om van alle mengen in de huurderscontainer een lijst te maken zou nu de mengeling van de Details van het Voertuig omvatten, of u kunt een raadpleging (KRIJGEN) verzoek uitvoeren gebruikend URL-Gecodeerde `$id` URI om de nieuwe mengeling direct te bekijken. Vergeet niet de header Accepteren op te nemen `version` in alle opzoekverzoeken.
