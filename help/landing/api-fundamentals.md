---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Grondbeginselen van Experience Platform API
topic-legacy: getting started
description: Dit document biedt een kort overzicht van enkele onderliggende technologieën en syntaxis die van toepassing zijn op Experience Platform-API's.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen voor een effectief beheer van JSON [!DNL Platform] middelen. Dit document bevat een kort overzicht van deze technologieën en koppelingen naar externe documentatie voor meer informatie.

## JSON-aanwijzer {#json-pointer}

JSON Pointer is een gestandaardiseerde tekenreekssyntaxis ([RFC 6901](https://tools.ietf.org/html/rfc6901)) voor het identificeren van specifieke waarden in JSON-documenten. Een JSON-aanwijzer is een reeks tokens gescheiden door `/` tekens, die objectsleutels of array-indexen opgeven, en tokens kunnen een tekenreeks of een getal zijn. JSON-aanwijzertekenreeksen worden in veel PATCH-bewerkingen gebruikt voor [!DNL Platform] API&#39;s, zoals verderop in dit document wordt beschreven. Voor meer informatie over JSON-aanwijzer raadpleegt u de [Overzicht van JSON-aanwijzer](https://rapidjson.org/md_doc_pointer.html).

### Voorbeeld-JSON-schemaobject

De volgende JSON vertegenwoordigt een vereenvoudigd XDM-schema waarvan met behulp van JSON-aanwijzertekenreeksen naar velden kan worden verwezen. Merk op dat alle gebieden die gebruikend de groepen van het douaneschema gebied (zoals zijn toegevoegd `loyaltyLevel`) worden genoemd onder a `_{TENANT_ID}` object, terwijl velden die zijn toegevoegd met behulp van kernveldgroepen (zoals `fullName`) niet.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Voorbeeld-JSON-aanwijzers op basis van een schemaobject

| JSON-aanwijzer | Oplossen naar |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Retourneert een verwijzing naar de `fullName` veld, verstrekt door een kernveldgroep.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retourneert een verwijzing naar de `loyaltyLevel` veld, opgegeven door een aangepaste veldgroep.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Wanneer u werkt met de `xdm:sourceProperty` en `xdm:destinationProperty` kenmerken van [!DNL Experience Data Model] (XDM)-descriptors, alle `properties` sleutels moeten **uitgesloten** uit de JSON-pointer-tekenreeks. Zie de [!DNL Schema Registry] Subhandleiding voor API-ontwikkelaars ingeschakeld [beschrijvingen](../xdm/api/descriptors.md) voor meer informatie .

## JSON Patch {#json-patch}

Er zijn veel PATCH-bewerkingen voor [!DNL Platform] API&#39;s die JSON Patch-objecten accepteren voor hun aanvraaglading. JSON Patch is een gestandaardiseerde indeling ([RFC 6902](https://tools.ietf.org/html/rfc6902)) voor het beschrijven van wijzigingen in een JSON-document. Hiermee kunt u gedeeltelijke updates voor JSON definiëren zonder dat u het gehele document in een aanvraaginstantie hoeft te verzenden.

### Voorbeeld van JSON Patch-object

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Het type patchbewerking. Hoewel JSON Patch verschillende bewerkingstypen ondersteunt, worden niet alle PATCH-bewerkingen in [!DNL Platform] API&#39;s zijn compatibel met elk type bewerking. Beschikbare bewerkingstypen zijn:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Het deel van de JSON-structuur dat moet worden bijgewerkt, geïdentificeerd aan de hand van [JSON-aanwijzer](#json-pointer) notatie.

Afhankelijk van het type bewerking dat in `op`heeft het JSON-object Patch mogelijk aanvullende eigenschappen nodig. Raadpleeg voor meer informatie over de verschillende JSON-patchbewerkingen en de bijbehorende syntaxis de [JSON-patchdocumentatie](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON Schema {#json-schema}

JSON-schema is een indeling waarmee de structuur van JSON-gegevens wordt beschreven en gevalideerd. [Experience Data Model (XDM)](../xdm/home.md) hefboomwerkingen de mogelijkheden van het Schema JSON om beperkingen op de structuur en het formaat van ingebedde gegevens van de klantenervaring af te dwingen. Voor meer informatie over JSON-schema raadpleegt u de [officiële documentatie](https://json-schema.org/).

## Volgende stappen

In dit document worden enkele technologieën en syntaxis geïntroduceerd die van belang zijn voor het beheer van JSON-bronnen voor [!DNL Experience Platform]. Zie de [gids Aan de slag](api-guide.md) voor meer informatie over het werken met Platform APIs, met inbegrip van beste praktijken. Voor antwoorden op veelgestelde vragen raadpleegt u de [Handleiding voor het oplossen van problemen met Platforms](troubleshooting.md).
