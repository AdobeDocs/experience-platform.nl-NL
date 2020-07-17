---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grondbeginselen van Adobe Experience Platform API
topic: getting started
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---


# Grondbeginselen van Adobe Experience Platform API

Adobe Experience Platform-API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen voor een effectief beheer van JSON- [!DNL Platform] bronnen. Dit document bevat een kort overzicht van deze technologieën en koppelingen naar externe documentatie voor meer informatie.

## JSON-aanwijzer {#json-pointer}

JSON Pointer is een gestandaardiseerde tekenreekssyntaxis ([RFC 6901](https://tools.ietf.org/html/rfc6901)) voor het identificeren van specifieke waarden in JSON-documenten. Een JSON-aanwijzer is een tekenreeks met tokens die door `/` tekens worden gescheiden. Hiermee worden objectsleutels of arrayindexen opgegeven. De tokens kunnen een tekenreeks of een getal zijn. JSON-aanwijzertekenreeksen worden in veel PATCH-bewerkingen voor API&#39; [!DNL Platform] s gebruikt, zoals verderop in dit document wordt beschreven. Raadpleeg de overzichtsdocumentatie [van de](https://rapidjson.org/md_doc_pointer.html)JSON-aanwijzer voor meer informatie over JSON-aanwijzer.

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
>
>
>Wanneer u werkt met de `xdm:sourceProperty` en `xdm:destinationProperty` kenmerken van [!DNL Experience Data Model] (XDM)-descriptors, moeten alle `properties` sleutels worden **uitgesloten** van de JSON-pointer-tekenreeks. Zie de subhandleiding voor [!DNL Schema Registry] API-ontwikkelaars voor [beschrijvingen](../xdm/api/descriptors.md) voor meer informatie.

## JSON Patch

Er zijn veel PATCH-bewerkingen voor API&#39; [!DNL Platform] s die JSON Patch-objecten accepteren voor hun verzoek-lading. JSON Patch is een gestandaardiseerde indeling ([RFC 6902](https://tools.ietf.org/html/rfc6902)) voor het beschrijven van wijzigingen in een JSON-document. Hiermee kunt u gedeeltelijke updates voor JSON definiëren zonder dat u het gehele document in een aanvraaginstantie hoeft te verzenden.

### Voorbeeld van JSON Patch-object

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Het type patchbewerking. Hoewel JSON Patch verschillende bewerkingstypen ondersteunt, zijn niet alle PATCH-bewerkingen in API&#39; [!DNL Platform] s compatibel met elk bewerkingstype. Beschikbare bewerkingstypen zijn:
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

In dit document worden enkele technologieën en syntaxis geïntroduceerd die betrokken zijn bij het beheer van JSON-bronnen voor [!DNL Experience Platform]. Raadpleeg de handleiding voor het oplossen van problemen bij [!DNL Platform] Platforms voor meer informatie over het werken met API&#39;s, inclusief tips en trucs en antwoorden op veelgestelde vragen [](troubleshooting.md).