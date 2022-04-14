---
title: Voorgestelde waarden toevoegen aan een veld
description: Leer hoe u voorgestelde waarden toevoegt aan een tekenreeksveld in de API voor schemaregistratie.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Voorgestelde waarden aan een veld toevoegen

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een enumgebied een koordgebied dat tot een vooraf bepaalde ondergroep van waarden wordt beperkt. Enum-velden kunnen validatie bieden om ervoor te zorgen dat ingesloten gegevens voldoen aan een set geaccepteerde waarden. U kunt echter ook een set voorgestelde waarden voor een tekenreeksveld definiëren zonder deze als beperkingen in te stellen.

In de [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)worden de beperkte waarden voor een opsommingsveld weergegeven door een `enum` array, terwijl een `meta:enum` -object biedt vriendelijke weergavenamen voor deze waarden:

```json
"exampleStringField": {
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

Voor opsommingsvelden is het schemaregister niet toegestaan `meta:enum` die verder gaan dan de in `enum`, omdat pogingen om tekenreekswaarden buiten deze beperkingen in te voeren geen validatie zouden doorstaan.

U kunt ook een tekenreeksveld definiëren dat geen `enum` -array en gebruikt alleen de `meta:enum` object voor het aangeven van voorgestelde waarden:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Aangezien de tekenreeks geen `enum` array om beperkingen te definiëren, `meta:enum` Deze eigenschap kan worden uitgebreid met nieuwe waarden. In deze zelfstudie wordt uitgelegd hoe u voorgestelde waarden kunt toevoegen aan standaard- en aangepaste tekenreeksvelden in de API voor schemaregistratie.

## Vereisten

Deze gids veronderstelt u met de elementen van schemacompositie in XDM vertrouwd bent en hoe te om de Registratie API van het Schema te gebruiken om middelen tot stand te brengen en uit te geven XDM. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [Basisbeginselen van de schemacompositie](../schema/composition.md)
* [Handleiding Schema Registry API](../api/overview.md)

## Voorgestelde waarden toevoegen aan een standaardveld

De `meta:enum` van een standaardtekenreeksveld kunt u een [beschrijvingsbestand vriendelijke naam](../api/descriptors.md#friendly-name) voor het betrokken veld in een bepaald schema.

>[!NOTE]
>
>Voorgestelde waarden voor tekenreeksvelden kunnen alleen op schemaniveau worden toegevoegd. Met andere woorden, de uitbreiding van de `meta:enum` van een standaardgebied in één schema beïnvloedt geen andere schema&#39;s die het zelfde standaardgebied gebruiken.

In het volgende verzoek worden voorgestelde waarden aan de norm toegevoegd `eventType` veld (verstrekt door de [XDM ExperienceEvent, klasse](../classes/experienceevent.md)) voor het schema dat onder `sourceSchema`:

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

## Voorgestelde waarden toevoegen aan een aangepast veld

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

Deze gids besprak hoe te om voorgestelde waarden aan koordgebieden in de Registratie API van het Schema toe te voegen. Zie de handleiding op [aangepaste velden in de API definiëren](./custom-fields-api.md) voor meer informatie over het maken van verschillende veldtypen.
