---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Grondbeginselen van Experience Platform API
description: Dit document biedt een kort overzicht van enkele onderliggende technologieën en syntaxis die van toepassing zijn op Experience Platform-API's.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen voor een effectief beheer van op JSON gebaseerde [!DNL Platform] bronnen. Dit document bevat een kort overzicht van deze technologieën en koppelingen naar externe documentatie voor meer informatie.

## JSON-aanwijzer {#json-pointer}

JSON Aanwijzer is een gestandaardiseerde koordsyntaxis ([ RFC 6901 ](https://tools.ietf.org/html/rfc6901)) voor het identificeren van specifieke waarden binnen JSON documenten. Een JSON-aanwijzer is een tekenreeks met tokens die door `/` -tekens worden gescheiden. Hiermee worden objectsleutels of arrayindexen opgegeven. De tokens kunnen een tekenreeks of een getal zijn. JSON-aanwijzertekenreeksen worden gebruikt in vele PATCH-bewerkingen voor [!DNL Platform] API&#39;s, zoals verderop in dit document wordt beschreven. Voor meer informatie over Aanwijzer JSON, gelieve te verwijzen naar de [ documentatie van het overzicht van de Aanwijzer JSON ](https://rapidjson.org/md_doc_pointer.html).

### Voorbeeld-JSON-schemaobject

De volgende JSON vertegenwoordigt een vereenvoudigd XDM-schema waarvan met behulp van JSON-aanwijzertekenreeksen naar velden kan worden verwezen. Alle velden die zijn toegevoegd met behulp van aangepaste schemaveldgroepen (zoals `loyaltyLevel` ), krijgen een naamruimte onder een `_{TENANT_ID}` -object, terwijl velden die zijn toegevoegd met behulp van kernveldgroepen (zoals `fullName` ) dat niet doen.

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

| JSON-aanwijzer | Oplossingen voor |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Retourneert een verwijzing naar het veld `fullName` , opgegeven door een kernveldgroep.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Retourneert een verwijzing naar het veld `loyaltyLevel` , opgegeven door een aangepaste veldgroep.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Wanneer het behandelen van `xdm:sourceProperty` en `xdm:destinationProperty` attributen van [!DNL Experience Data Model] (XDM) beschrijvers, moeten om het even welke `properties` sleutels **** van het koord van de Aanwijzer JSON worden uitgesloten. Zie de [!DNL Schema Registry] sub-gids van de ontwikkelaar van API op [ beschrijvers ](../xdm/api/descriptors.md) voor meer informatie.

## JSON Patch {#json-patch}

Er zijn veel PATCH-bewerkingen voor API&#39;s van [!DNL Platform] die JSON Patch-objecten accepteren voor hun aanvraaglading. JSON Reparatie is een gestandaardiseerd formaat ([ RFC 6902 ](https://tools.ietf.org/html/rfc6902)) voor het beschrijven van veranderingen in een JSON- document. Hiermee kunt u gedeeltelijke updates voor JSON definiëren zonder dat u het gehele document in een aanvraaginstantie hoeft te verzenden.

### Voorbeeld van JSON Patch-object

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Het type patchbewerking. Hoewel JSON Patch verschillende bewerkingstypen ondersteunt, zijn niet alle PATCH-bewerkingen in [!DNL Platform] API&#39;s compatibel met elk bewerkingstype. Beschikbare bewerkingstypen zijn:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Het deel van de structuur JSON dat moet worden bijgewerkt, gebruikend [ JSON ](#json-pointer) aantekening van de Aanwijzer wordt geïdentificeerd.

Afhankelijk van het type bewerking dat in `op` wordt aangegeven, heeft het JSON-object Patch mogelijk aanvullende eigenschappen nodig. Voor meer informatie over de verschillende verrichtingen van het Reparatie JSON en hun vereiste syntaxis, gelieve te verwijzen naar de [ documentatie van het Reparatie JSON ](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON Schema {#json-schema}

JSON-schema is een indeling waarmee de structuur van JSON-gegevens wordt beschreven en gevalideerd. [ Model van de Gegevens van de Ervaring (XDM) ](../xdm/home.md) hefboomwerkingen JSON de mogelijkheden van het Schema om beperkingen op de structuur en het formaat van ingebedde gegevens van de klantenervaring af te dwingen. Voor meer informatie over Schema JSON, gelieve te verwijzen naar de [ officiële documentatie ](https://json-schema.org/).

## Volgende stappen

In dit document worden enkele technologieën en syntaxis geïntroduceerd die betrokken zijn bij het beheer van JSON-bronnen voor [!DNL Experience Platform] . Verwijs naar de [ begonnen gids ](api-guide.md) voor meer informatie bij het werken met Platform APIs, met inbegrip van beste praktijken. Voor antwoorden op vaak gestelde vragen, verwijs naar de [ het oplossen van problemengids van het Platform ](troubleshooting.md).
