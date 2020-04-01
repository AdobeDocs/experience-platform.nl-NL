---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een klasse maken
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba

---


# Een klasse maken

De primaire bouwsteen van een schema is een klasse. De klasse bevat de minimale set velden die moet worden gedefinieerd om de kerngegevens van een schema vast te leggen. Als u bijvoorbeeld een schema voor auto&#39;s en vrachtwagens zou ontwerpen, zou het meest waarschijnlijk een klasse gebruiken met de naam Vehicle die de algemene basiseigenschappen van alle voertuigen beschrijft.

Er zijn verschillende standaardklassen die door Adobe en andere partners van het Platform van de Ervaring worden verstrekt, maar u kunt uw eigen klassen ook bepalen en hen bewaren aan de Registratie van het Schema. Vervolgens kunt u een schema samenstellen waarmee de gemaakte klasse wordt geïmplementeerd en combinaties definiëren die compatibel zijn met de zojuist gedefinieerde klasse.

>[!NOTE] Wanneer het samenstellen van een schema dat op een klasse wordt gebaseerd die u bepaalt, zult u geen standaardmengen kunnen gebruiken. Elke mix definieert de klassen waarmee ze compatibel zijn in hun `meta:intendedToExtend` kenmerk. Zodra u begint bepalend mengen die met uw nieuwe klasse (door de nieuwe klasse op het `$id` `meta:intendedToExtend` gebied van het mengen te gebruiken) compatibel zijn, zult u die mixins kunnen opnieuw gebruiken telkens als u een schema bepaalt dat de klasse uitvoert u bepaalde. Zie de secties over het [creëren van mengen](create-mixin.md) en het [creëren van schema](create-schema.md) &#39;s voor meer informatie.

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

De aanvraag om een klasse te maken (POST) moet een `allOf` attribuut bevatten dat een `$ref` tot een van twee waarden bevat: `https://ns.adobe.com/xdm/data/record` of `https://ns.adobe.com/xdm/data/time-series`. Deze waarden vertegenwoordigen het gedrag waarop de klasse is gebaseerd (record- of tijdreeks, respectievelijk). Voor meer informatie over de verschillen tussen verslaggegevens en tijdreeksgegevens, zie de sectie over gedragstypes binnen de [grondbeginselen van schemacompositie](../schema/composition.md).

Wanneer u een klasse definieert, kunt u ook mixins of aangepaste velden opnemen in de klassendefinitie. Hierdoor worden de toegevoegde mixins en velden opgenomen in alle schema&#39;s die de klasse implementeren. In het volgende voorbeeldverzoek wordt een klasse met de naam &quot;Eigenschap&quot; gedefinieerd, die informatie vastlegt over verschillende eigenschappen die eigendom zijn van en worden beheerd door een bedrijf. Het bevat een `propertyId` veld dat wordt opgenomen telkens wanneer de klasse wordt gebruikt.

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
| `_{TENANT_ID}` | De `TENANT_ID` naamruimte voor uw organisatie. Alle middelen die door uw organisatie worden gecreeerd moeten dit bezit omvatten om botsingen met andere middelen in de Registratie van het Schema te vermijden. |
| `allOf` | Een lijst met bronnen waarvan de eigenschappen door de nieuwe klasse moeten worden overgeërfd. Een van de `$ref` objecten in de array definieert het gedrag van de klasse. In dit voorbeeld overerft de klasse het gedrag &#39;record&#39;. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van de nieuwe klasse, inclusief de klasse `$id`, `meta:altId`en `version`. Deze drie waarden zijn read-only en door de Registratie van het Schema toegewezen.

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

Het uitvoeren van een GET verzoek om van alle klassen in de huurderscontainer een lijst te maken zou nu de klasse van het Bezit omvatten. U kunt ook een opzoekaanvraag (GET) uitvoeren met de URL-gecodeerde `$id` URI om de nieuwe klasse rechtstreeks weer te geven. Zorg ervoor dat u de code opneemt `version` in de koptekst Accepteren wanneer u een opzoekverzoek uitvoert.
