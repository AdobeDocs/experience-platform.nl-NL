---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;xdm;ervaringsgegevensmodel;naamruimte;naamruimte;compatibiliteitsmodus;Gereed;
solution: Experience Platform
title: Naamruimte in XDM (Experience Data Model)
topic-legacy: overviews
description: Leer hoe het namespacing in het Model van de Gegevens van de Ervaring (XDM) u toestaat om uw schema's uit te breiden en gebiedsbotsingen te verhinderen aangezien de verschillende schemacomponenten samen worden gebracht.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: bcffd3d38cecba38e1e57a44ce0febfd2cf0f8fb
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Naamruimte in XDM (Experience Data Model)

Aan alle velden in XDM-schema&#39;s (Experience Data Model) is een naamruimte gekoppeld. Deze namespaces staan u toe om uw schema&#39;s uit te breiden en gebiedsbotsingen te verhinderen aangezien de verschillende schemacomponenten samen worden gebracht. Dit document biedt een overzicht van naamruimten in XDM en hoe deze worden weergegeven in het dialoogvenster [Schema-register-API](../api/overview.md).

Met naamruimte kunt u een veld in één naamruimte definiëren als iets anders dan hetzelfde veld in een andere naamruimte. In de praktijk geeft de naamruimte van een veld aan wie het veld heeft gemaakt (bijvoorbeeld standaard-XDM (Adobe), een leverancier of uw organisatie).

Neem bijvoorbeeld een XDM-schema dat het [[!UICONTROL Personal Contact Details] veldgroep](../field-groups/profile/demographic-details.md), die een standaard heeft `mobilePhone` bestaat in het veld `xdm` naamruimte. In hetzelfde schema kunt u ook een aparte `mobilePhone` veld onder een andere naamruimte (uw [huurder-id](../api/getting-started.md#know-your-tenant_id)). Beide velden kunnen naast elkaar bestaan terwijl ze verschillende onderliggende betekenissen of beperkingen hebben.

## Syntaxis naamruimte

In de volgende secties ziet u hoe naamruimten worden toegewezen in XDM-syntaxis.

### Standaard XDM {#standard}

De standaard XDM syntaxis verstrekt inzicht in hoe namespaces in schema&#39;s (met inbegrip van [hoe ze in Adobe Experience Platform worden vertaald](#compatibility)).

Standaard XDM-gebruik [JSON-LD](https://json-ld.org/) syntaxis om naamruimten toe te wijzen aan velden. Deze naamruimte heeft de vorm van een URI (bijvoorbeeld `https://ns.adobe.com/xdm` voor de `xdm` namespace), of als steno prefix die in wordt gevormd `@context` kenmerk van een schema.

Hier volgt een voorbeeldschema voor een product in de standaard XDM-syntaxis. Met uitzondering van `@id` (de unieke id zoals gedefinieerd door de specificatie JSON-LD), elk veld onder `properties` begint met een naamruimte en eindigt met de veldnaam. Als u een korte prefix gebruikt die onder `@context`, de naamruimte en de veldnaam worden gescheiden door een dubbele punt (`:`). Als u geen voorvoegsel gebruikt, worden de naamruimte en de veldnaam gescheiden door een schuine streep (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@context` | Een object dat de steno-voorvoegsels definieert die kunnen worden gebruikt in plaats van een volledige naamruimte-URI onder `properties`. |
| `@id` | Een unieke id voor de record, zoals gedefinieerd door de [JSON-LD spec](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | Een voorbeeld van een veld dat een voorvoegsel uit de steno gebruikt om een naamruimte aan te duiden. In dit geval: `xdm` is de naamruimte (`https://ns.adobe.com/xdm`), en `sku` is de veldnaam. |
| `https://ns.adobe.com/xdm/channels/application` | Een voorbeeld van een veld dat de volledige naamruimte-URI gebruikt. In dit geval: `https://ns.adobe.com/xdm/channels` de naamruimte is, en `application` is de veldnaam. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Velden die worden geleverd door bronnen van leveranciers, gebruiken hun eigen unieke naamruimten. In dit voorbeeld: `https://ns.adobe.com/vendorA/product` de naamruimte van de leverancier is, en `stockNumber` is de veldnaam. |
| `tenantId:internalSku` | De gebieden die door uw organisatie worden bepaald gebruiken uw unieke huurdersidentiteitskaart als hun namespace. In dit voorbeeld: `tenantId` is de huurdersnaamruimte (`https://ns.adobe.com/tenantId`), en `internalSku` is de veldnaam. |

{style=&quot;table-layout:auto&quot;}

### Compatibiliteitsmodus {#compatibility}

In Adobe Experience Platform worden XDM-schema&#39;s weergegeven in [Compatibiliteitsmodus](../api/appendix.md#compatibility) syntaxis, waarbij de JSON-LD-syntaxis niet wordt gebruikt om naamruimten te vertegenwoordigen. In plaats daarvan wordt de naamruimte door het Platform omgezet in een bovenliggend veld (te beginnen met een onderstrepingsteken) en worden de onderliggende velden genest.

De standaard-XDM `repo:createdDate` wordt omgezet in `_repo.createdDate` en wordt weergegeven in de volgende structuur in de compatibiliteitsmodus:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Velden die de `xdm` naamruimte wordt weergegeven als hoofdvelden onder `properties` en zet de `xdm:` voorvoegsel dat wordt weergegeven in [standaard XDM-syntaxis](#standard). Bijvoorbeeld: `xdm:sku` is gewoon aangeboden als `sku` in plaats daarvan.

De volgende JSON vertegenwoordigt hoe het standaard XDM syntaxisvoorbeeld hierboven wordt getoond vertaald naar de Wijze van de Verenigbaarheid.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Volgende stappen

Deze handleiding biedt een overzicht van XDM-naamruimten en hoe deze worden weergegeven in JSON. Voor meer informatie over hoe te om schema&#39;s XDM te vormen gebruikend API, zie [Handleiding Schema Registry API](../api/overview.md).
