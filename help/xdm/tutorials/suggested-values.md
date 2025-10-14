---
title: Voorgestelde waarden beheren in de API
description: Leer hoe u voorgestelde waarden toevoegt aan een tekenreeksveld in de API voor schemaregistratie.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Aanbevolen waarden beheren in de API

Voor om het even welk koordgebied in het Model van de Gegevens van de Ervaring (XDM), kunt u een **opsomming** bepalen die de waarden beperkt die het gebied aan een vooraf bepaalde reeks kan opnemen. Als u probeert gegevens in te voeren in een opsommingsveld en de waarde niet overeenkomt met een van de gedefinieerde waarden in de configuratie, wordt invoer geweigerd.

In tegenstelling tot opsommingen, beperkt het toevoegen van **gesuggereerde waarden** aan een koordgebied niet de waarden die het kan opnemen. In plaats daarvan, beïnvloeden de voorgestelde waarden welke vooraf bepaalde waarden in [&#x200B; Segmentatie UI &#x200B;](../../segmentation/ui/overview.md) beschikbaar zijn wanneer het omvatten van het koordgebied als attribuut.

>[!NOTE]
>
>Er is een ongeveer vijf-minieme vertraging voor de bijgewerkte voorgestelde waarden van een gebied om in de Segmentatie UI worden weerspiegeld.

Deze gids behandelt hoe te om voorgestelde waarden te beheren gebruikend de [&#x200B; Registratie API van het Schema &#x200B;](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Voor stappen op hoe te om dit in het gebruikersinterface van Adobe Experience Platform te doen, zie de [&#x200B; gids UI op aantallen en voorgestelde waarden &#x200B;](../ui/fields/enum.md).

## Vereisten

Deze gids veronderstelt u met de elementen van schemacompositie in XDM vertrouwd bent en hoe te om de Registratie API van het Schema te gebruiken om middelen tot stand te brengen en uit te geven XDM. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [Basisbeginselen van de schemacompositie](../schema/composition.md)
* [Handleiding Schema Registry API](../api/overview.md)

Het wordt ook sterk geadviseerd dat u de [&#x200B; evolutieregels voor aantallen en gesuggereerde waarden &#x200B;](../ui/fields/enum.md#evolution) herziet als u bestaande gebieden bijwerkt. Als u voorgestelde waarden voor schema&#39;s beheert die aan een unie deelnemen, zie de [&#x200B; regels voor het samenvoegen van lijsten en voorgestelde waarden &#x200B;](../ui/fields/enum.md#merging).

## Samenstelling

In API, worden de beperkte waarden voor een **enum** gebied vertegenwoordigd door een `enum` serie, terwijl een `meta:enum` voorwerp vriendschappelijke vertoningsnamen voor die waarden verstrekt:

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

Voor opsommingsvelden staat het schemaregister niet toe dat `meta:enum` wordt uitgebreid tot meer dan de waarden in `enum` , omdat pogingen om tekenreekswaarden buiten deze beperkingen in te voeren, geen validatie zouden doorstaan.

Alternatief, kunt u een koordgebied bepalen dat geen `enum` serie bevat en slechts het `meta:enum` voorwerp gebruikt om **gesuggereerde waarden** aan te duiden:

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

Aangezien de tekenreeks geen `enum` -array heeft om beperkingen te definiëren, kan de eigenschap `meta:enum` worden uitgebreid met nieuwe waarden.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Voorgestelde waarden toevoegen aan een standaardveld {#add-suggested-standard}

Om `meta:enum` van een standaardkoordgebied uit te breiden, kunt u a [&#x200B; vriendschappelijke naambeschrijver &#x200B;](../api/descriptors.md#friendly-name) voor het gebied in kwestie in een bepaald schema tot stand brengen.

>[!NOTE]
>
>Voorgestelde waarden voor tekenreeksvelden kunnen alleen op schemaniveau worden toegevoegd. Met andere woorden, het uitbreiden van `meta:enum` van een standaardveld in één schema heeft geen invloed op andere schema&#39;s die hetzelfde standaardveld gebruiken.

Het volgende verzoek voegt gesuggereerde waarden aan het standaard `eventType` gebied (door de [&#x200B; klasse XDM ExperienceEvent &#x200B;](../classes/experienceevent.md) wordt verstrekt) voor het schema toe dat onder `sourceSchema` wordt geïdentificeerd:

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
>Als het standaardveld al waarden onder `meta:enum` bevat, overschrijven de nieuwe waarden van het descriptorbestand de bestaande velden niet en worden deze toegevoegd:
>
>```json
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

Als u de `meta:enum` van een aangepast veld wilt beheren, kunt u de bovenliggende klasse, veldgroep of het gegevenstype van het veld bijwerken via een PATCH-aanvraag.

>[!WARNING]
>
>In tegenstelling tot standaardvelden heeft het bijwerken van de `meta:enum` van een aangepast veld invloed op alle andere schema&#39;s waarin dat veld wordt gebruikt. Als u geen veranderingen over schema&#39;s wilt verspreiden, denk in plaats daarvan na creërend een nieuwe douanemiddel:
>
>* [&#x200B; creeer een douaneklasse &#x200B;](../api/classes.md#create)
>* [&#x200B; creeer een groep van het douanegebied &#x200B;](../api/field-groups.md#create)
>* [&#x200B; creeer een type van douanegegevens &#x200B;](../api/data-types.md#create)

Met de volgende aanvraag wordt de `meta:enum` van een veld voor een &quot;loyaliteitsniveau&quot; bijgewerkt dat door een aangepast gegevenstype wordt verschaft:

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

Deze gids behandelde hoe te om voorgestelde waarden voor koordgebieden in de Registratie API van het Schema te beheren. Zie de gids op [&#x200B; bepalend douanegebieden in API &#x200B;](./custom-fields-api.md) voor meer informatie over hoe te om verschillende gebiedstypes tot stand te brengen.
