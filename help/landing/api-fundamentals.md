---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Grondbeginselen van Experience Platform API
topic: getting started
description: Dit document biedt een kort overzicht van enkele onderliggende technologieën en syntaxis die van toepassing zijn op Experience Platform-API's.
translation-type: tm+mt
source-git-commit: 8c98632b67ddae4fb7800e80fb8c83aca9bfa291
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen voor een effectief beheer van op JSON gebaseerde [!DNL Platform]-bronnen. Dit document bevat een kort overzicht van deze technologieën en koppelingen naar externe documentatie voor meer informatie.

## JSON-aanwijzer {#json-pointer}

JSON-aanwijzer is een gestandaardiseerde tekenreekssyntaxis ([RFC 6901](https://tools.ietf.org/html/rfc6901)) voor het identificeren van specifieke waarden in JSON-documenten. Een JSON-aanwijzer is een tekenreeks met tokens die door `/` tekens worden gescheiden. Deze tekens geven objectsleutels of arrayindexen op en de tokens kunnen een tekenreeks of een getal zijn. JSON-aanwijzertekenreeksen worden gebruikt in vele PATCH-bewerkingen voor API&#39;s van [!DNL Platform], zoals verderop in dit document wordt beschreven. Raadpleeg de documentatie [JSON-aanwijzer voor meer informatie over JSON-aanwijzer](https://rapidjson.org/md_doc_pointer.html).

### Voorbeeld-JSON-schemaobject

De volgende JSON vertegenwoordigt een vereenvoudigd XDM-schema waarvan met behulp van JSON-aanwijzertekenreeksen naar velden kan worden verwezen. Merk op dat alle gebieden die gebruikend douanemixins (zoals `loyaltyLevel`) zijn toegevoegd namespaced onder een `_{TENANT_ID}` voorwerp, terwijl de gebieden die zijn toegevoegd gebruikend kernmengen (zoals `fullName`) niet zijn.

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
| `"/properties/person/properties/name/properties/fullName"` | (Retourneert een verwijzing naar het veld `fullName`, opgegeven door een kernmix.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retourneert een verwijzing naar het veld `loyaltyLevel`, opgegeven door een aangepaste mix.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Wanneer u omgaat met de `xdm:sourceProperty`- en `xdm:destinationProperty`-kenmerken van [!DNL Experience Data Model] (XDM)-descriptors, moeten `properties`-toetsen **uitgesloten** zijn van de JSON-pointer-tekenreeks. Zie de [!DNL Schema Registry] API-handleiding voor ontwikkelaars in [descriptors](../xdm/api/descriptors.md) voor meer informatie.

## JSON-patch {#json-patch}

Er zijn vele verrichtingen van PATCH voor [!DNL Platform] APIs die voorwerpen van de Reparatie JSON voor hun verzoeklading goedkeuren. JSON Patch is een gestandaardiseerde indeling ([RFC 6902](https://tools.ietf.org/html/rfc6902)) voor het beschrijven van wijzigingen in een JSON-document. Hiermee kunt u gedeeltelijke updates voor JSON definiëren zonder dat u het gehele document in een aanvraaginstantie hoeft te verzenden.

### Voorbeeld van JSON Patch-object

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Het type patchbewerking. Hoewel JSON Patch verschillende verrichtingstypes steunt, zijn niet alle verrichtingen van de PATCH in [!DNL Platform] APIs compatibel met elk verrichtingstype. Beschikbare bewerkingstypen zijn:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Het deel van de JSON-structuur dat moet worden bijgewerkt, geïdentificeerd met behulp van  [JSON-](#json-pointer) pointernotatie.

Afhankelijk van het type bewerking dat wordt aangegeven in `op`, heeft het JSON-object Patch mogelijk aanvullende eigenschappen nodig. Raadpleeg de [JSON Patch-documentatie](http://jsonpatch.com/) voor meer informatie over de verschillende JSON Patch-bewerkingen en de bijbehorende syntaxis.

## JSON-schema {#json-schema}

JSON-schema is een indeling waarmee de structuur van JSON-gegevens wordt beschreven en gevalideerd. [Het Model van de Gegevens van de ervaring (XDM) ](../xdm/home.md) hefboomwerkingen JSON de mogelijkheden van het Schema om beperkingen op de structuur en het formaat van ingebedde gegevens van de klantenervaring af te dwingen. Raadpleeg de [officiële documentatie](https://json-schema.org/) voor meer informatie over JSON-schema.

## Volgende stappen

In dit document worden enkele technologieën en syntaxis geïntroduceerd die betrokken zijn bij het beheer van JSON-bronnen voor [!DNL Experience Platform]. Raadpleeg de [handleiding voor het oplossen van Platforms](troubleshooting.md) voor meer informatie over het werken met API&#39;s van [!DNL Platform], inclusief best practices en antwoorden op veelgestelde vragen.