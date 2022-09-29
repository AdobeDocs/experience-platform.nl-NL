---
title: Voorgestelde waarden beheren in de API
description: Leer hoe u voorgestelde waarden toevoegt aan een tekenreeksveld in de API voor schemaregistratie.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 2f916ea4b05ca67c2b9e603512d732a2a3f7a3b2
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Aanbevolen waarden beheren in de API

Voor elk tekenreeksveld in het XDM (Experience Data Model) kunt u een **enum** dat de waarden die het veld kan invoeren, beperkt tot een vooraf gedefinieerde set. Als u probeert gegevens in te voeren in een opsommingsveld en de waarde niet overeenkomt met een van de gedefinieerde waarden in de configuratie, wordt invoer geweigerd.

In tegenstelling tot opsommingen, toevoegen **voorgestelde waarden** aan een tekenreeksveld te koppelen, beperkt niet de waarden die het kan invoeren. De voorgestelde waarden hebben daarentegen invloed op de beschikbare vooraf gedefinieerde waarden in het dialoogvenster [Segmenteringsinterface](../../segmentation/ui/overview.md) wanneer het tekenreeksveld wordt opgenomen als een kenmerk.

>[!NOTE]
>
>Er is een ongeveer vijf-minieme vertraging voor de bijgewerkte voorgestelde waarden van een gebied om in de Segmentatie UI worden weerspiegeld.

In deze handleiding wordt beschreven hoe u voorgestelde waarden kunt beheren met de [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Raadpleeg voor meer informatie over hoe u dit kunt doen in de gebruikersinterface van Adobe Experience Platform de [UI-handleiding voor opsommingen en voorgestelde waarden](../ui/fields/enum.md).

## Vereisten

Deze gids veronderstelt u met de elementen van schemacompositie in XDM vertrouwd bent en hoe te om de Registratie API van het Schema te gebruiken om middelen tot stand te brengen en uit te geven XDM. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [Basisbeginselen van de schemacompositie](../schema/composition.md)
* [Handleiding Schema Registry API](../api/overview.md)

U wordt ook ten zeerste aangeraden de [evolutieregels voor nummers en voorgestelde waarden](../ui/fields/enum.md#evolution) als u bestaande velden bijwerkt. Als u voorgestelde waarden voor schema&#39;s beheert die aan een unie deelnemen, zie [regels voor het samenvoegen van opsommingen en voorgestelde waarden](../ui/fields/enum.md#merging).

## Samenstelling

In de API kunnen de beperkte waarden voor een **enum** veld wordt weergegeven door een `enum` array, terwijl een `meta:enum` -object biedt vriendelijke weergavenamen voor deze waarden:

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

U kunt ook een tekenreeksveld definiëren dat geen `enum` -array en gebruikt alleen de `meta:enum` aan te duiden object **voorgestelde waarden**:

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

Aangezien de tekenreeks geen `enum` array om beperkingen te definiëren, `meta:enum` Deze eigenschap kan worden uitgebreid met nieuwe waarden.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Voorgestelde waarden toevoegen aan een standaardveld {#add-suggested-standard}

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Voorgestelde waarden voor een aangepast veld beheren {#suggested-custom}

Om het `meta:enum` van een aangepast veld kunt u de bovenliggende klasse, veldgroep of het gegevenstype van het veld bijwerken via een PATCH-aanvraag.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Deze gids behandelde hoe te om voorgestelde waarden voor koordgebieden in de Registratie API van het Schema te beheren. Zie de handleiding op [aangepaste velden in de API definiëren](./custom-fields-api.md) voor meer informatie over het maken van verschillende veldtypen.
