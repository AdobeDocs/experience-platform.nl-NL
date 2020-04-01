---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Basisprincipes van de API van het Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: c94f065a5d56ac495dd2d541531aaec94c187612

---


# Basisprincipes van de API van het Adobe Experience Platform

Adobe Experience Platform-API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen voor een effectief beheer van JSON-gebaseerde platformbronnen. Dit document bevat een kort overzicht van deze technologieën en koppelingen naar externe documentatie voor meer informatie.

## JSON-aanwijzer {#json-pointer}

JSON Pointer is een gestandaardiseerde tekenreekssyntaxis ([RFC 6901](https://tools.ietf.org/html/rfc6901)) voor het identificeren van specifieke waarden in JSON-documenten. Een JSON-aanwijzer is een tekenreeks met tokens die door `/` tekens worden gescheiden. Hiermee worden objectsleutels of arrayindexen opgegeven. De tokens kunnen een tekenreeks of een getal zijn. JSON-aanwijzertekenreeksen worden gebruikt in veel PATCH-bewerkingen voor platform-API&#39;s, zoals verderop in dit document wordt beschreven. Raadpleeg de overzichtsdocumentatie [van de](https://rapidjson.org/md_doc_pointer.html)JSON-aanwijzer voor meer informatie over JSON-aanwijzer.

### Voorbeeld-JSON-schemaobject

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
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
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Voorbeeld-JSON-aanwijzers op basis van een schemaobject

| JSON-aanwijzer | Oplossen naar |
|--- | ---|
| `"/title"` | &quot;Details van het lid Loyalty&quot; |
| `"/definitions/loyalty"` | (Retourneert de inhoud van het `loyalty` object) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Nofferte]
>Wanneer u omgaat met de `xdm:sourceProperty` en `xdm:destinationProperty` kenmerken van XDM-beschrijvingen (Experience Data Model), moeten alle `properties` sleutels worden **uitgesloten** van de JSON-aanwijzertekenreeks. Zie de subhandleiding voor ontwikkelaars van de API voor het schemaregister voor [beschrijvingen](../xdm/api/descriptors.md) voor meer informatie.

## JSON Patch

Er zijn veel PATCH-bewerkingen voor platform-API&#39;s die JSON Patch-objecten accepteren voor hun verzoek-lading. JSON Patch is een gestandaardiseerde indeling ([RFC 6902](https://tools.ietf.org/html/rfc6902)) voor het beschrijven van wijzigingen in een JSON-document. Hiermee kunt u gedeeltelijke updates voor JSON definiëren zonder dat u het gehele document in een aanvraaginstantie hoeft te verzenden.

### Voorbeeld van JSON Patch-object

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Het type patchbewerking. Hoewel JSON Patch verschillende verrichtingstypes steunt, zijn niet alle verrichtingen van de PATCH in Platform APIs compatibel met elk verrichtingstype. Beschikbare bewerkingstypen zijn:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Het gedeelte van de JSON-structuur dat moet worden bijgewerkt, geïdentificeerd met [JSON-aanwijzernotatie](#json-pointer) .

Afhankelijk van het type bewerking dat in `op`dit voorbeeld wordt aangegeven, heeft het JSON-object Patch mogelijk aanvullende eigenschappen nodig. Raadpleeg de documentatie bij [JSON Patch voor meer informatie over de verschillende JSON-patchbewerkingen en de bijbehorende syntaxis](http://jsonpatch.com/).

## JSON Schema

JSON-schema is een indeling waarmee de structuur van JSON-gegevens wordt beschreven en gevalideerd. [Het Model van de Gegevens van de ervaring (XDM)](../xdm/home.md) hefboomwerkingen JSON de mogelijkheden van het Schema om beperkingen op de structuur en het formaat van ingebedde gegevens van de klantenervaring af te dwingen. Raadpleeg de [officiële documentatie](https://json-schema.org/)voor meer informatie over JSON-schema.

## Volgende stappen

In dit document worden enkele technologieën en syntaxis geïntroduceerd die betrokken zijn bij het beheer van JSON-bronnen voor Experience Platform. Raadpleeg voor meer informatie over het werken met platform-API&#39;s, waaronder best practices en antwoorden op veelgestelde vragen, de handleiding voor het oplossen van problemen bij [platformen](troubleshooting.md).