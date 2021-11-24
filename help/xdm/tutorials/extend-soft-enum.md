---
title: Een zacht Enum-veld uitbreiden
description: Leer hoe u een veld met een zachte opsomming kunt uitbreiden in de API voor schemaregistratie.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 9f275ba69c0310fb93ddec58c89259f25244ae23
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Een zacht opsommingsveld uitbreiden

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een enumgebied een koordgebied dat tot een vooraf bepaalde ondergroep van waarden wordt beperkt. Enum-velden kunnen validatie bieden om ervoor te zorgen dat ingesloten gegevens voldoen aan een set geaccepteerde waarden (aangeduid als een &quot;harde opsomming&quot;), of ze kunnen gewoon een set voorgestelde waarden vertegenwoordigen zonder beperkingen af te dwingen (bedoeld als een &quot;soft enum&quot;).

In de API van de Registratie van het Schema, worden de beperkte waarden voor harde enum vertegenwoordigd door `enum` array, terwijl een `meta:enum` -object biedt vriendelijke weergavenamen voor deze waarden:

```json
"sampleHardEnumField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Voor velden met harde getallen staat het schemaregister niet toe `meta:enum` die verder gaan dan de in `enum`, omdat pogingen om tekenreekswaarden buiten deze beperkingen in te voeren geen validatie zouden doorstaan.

Een veld met een zachte opsomming bevat daarentegen geen `enum` -array en gebruikt alleen de `meta:enum` object voor het aangeven van voorgestelde waarden:

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Aangezien zachte opsommingen niet dezelfde validatiebeperkingen hebben als harde opsommingen, hebben de `meta:enum` eigenschappen kunnen worden uitgebreid tot nieuwe waarden. In deze zelfstudie wordt uitgelegd hoe u standaard- en aangepaste schermopsommingsvelden in de API voor schemaregistratie kunt uitbreiden.

## Vereisten

Deze gids veronderstelt u met de elementen van schemacompositie in XDM vertrouwd bent en hoe te om de Registratie API van het Schema te gebruiken om middelen tot stand te brengen en uit te geven XDM. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [Basisbeginselen van de schemacompositie](../schema/composition.md)
* [Handleiding Schema Registry API](../api/overview.md)

## Een standaardveld voor zachte opsommingen uitbreiden

De `meta:enum` van een standaardtekenreeksveld kunt u een [beschrijvingsbestand vriendelijke naam](../api/descriptors.md#friendly-name) voor het betrokken veld in een bepaald schema.

>[!NOTE]
>
>Standaard zachte opsommingen kunnen alleen op schemaniveau worden uitgebreid. Met andere woorden, de uitbreiding van de `meta:enum` van een standaardgebied in één schema beïnvloedt geen andere schema&#39;s die het zelfde standaardgebied gebruiken.

Met de volgende aanvraag worden zachte opsommingswaarden aan de norm toegevoegd `eventType` veld (verstrekt door de [XDM ExperienceEvent, klasse](../classes/experienceevent.md)) voor het schema dat onder `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Nadat de descriptor is toegepast, reageert de schemaregistratie met het volgende wanneer het schema wordt opgehaald (reactie afgebroken voor ruimte):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Als het standaardveld al waarden bevat onder `meta:enum`De nieuwe waarden van de descriptor overschrijven de bestaande velden niet en worden in plaats daarvan toegevoegd:
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

## Een aangepast veld met een zachte opsomming uitbreiden

De `meta:enum` van een aangepast veld kunt u de bovenliggende klasse, veldgroep of het gegevenstype van het veld bijwerken via een PATCH-aanvraag.

>[!WARNING]
>
>In tegenstelling tot standaardvelden, kunt u de `meta:enum` van een aangepast veld beïnvloedt alle andere schema&#39;s waarin dat veld wordt gebruikt. Als u geen veranderingen over schema&#39;s wilt verspreiden, denk in plaats daarvan na creërend een nieuwe douanemiddel:
>
>* [Een aangepaste klasse maken](../api/classes.md#create)
>* [Een aangepaste veldgroep maken](../api/field-groups.md#create)
>* [Een aangepast gegevenstype maken](../api/data-types.md#create)


De volgende aanvraag werkt de `meta:enum` van een &quot;loyaliteitsniveau&quot;gebied dat door een type van douanegegevens wordt verstrekt:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Na het toepassen van de verandering, antwoordt de Registratie van het Schema met het volgende wanneer het terugwinnen van het schema (reactie beknot voor ruimte):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Volgende stappen

Deze gids besprak hoe te om zachte aantallen in de Registratie API van het Schema uit te breiden. Zie de handleiding voor meer informatie over het definiëren van verschillende veldtypen in de API [Beperkingen voor XDM-veldtypen](../schema/field-constraints.md#define-fields).
