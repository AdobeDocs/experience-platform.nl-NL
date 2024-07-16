---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;xdm;ervaringsgegevensmodel;naamruimte;naamruimte;compatibiliteitsmodus;Gereed;
solution: Experience Platform
title: Naamruimte in XDM (Experience Data Model)
description: Leer hoe het namespacing in het Model van de Gegevens van de Ervaring (XDM) u toestaat om uw schema's uit te breiden en gebiedsbotsingen te verhinderen aangezien de verschillende schemacomponenten samen worden gebracht.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Naamruimte in XDM (Experience Data Model)

>[!IMPORTANT]
>
>In XDM, wordt namespace (het onderwerp van deze pagina) gebruikt om gebieden in een schema te onderscheiden. Dit is verschillend aan het concept identiteitsnamespace in de Dienst van de Identiteit, waar namespace wordt gebruikt om identiteitswaarden te onderscheiden. Lees de documentatie over [ namespace in de Dienst van de Identiteit ](../../identity-service/features/namespaces.md) voor meer informatie.

Aan alle velden in XDM-schema&#39;s (Experience Data Model) is een naamruimte gekoppeld. Deze namespaces staan u toe om uw schema&#39;s uit te breiden en gebiedsbotsingen te verhinderen aangezien de verschillende schemacomponenten samen worden gebracht. Dit document verstrekt een overzicht van namespaces in XDM en hoe zij in de [ Registratie API van het Schema ](../api/overview.md) worden vertegenwoordigd.

Met naamruimte kunt u een veld in één naamruimte definiëren als iets anders dan hetzelfde veld in een andere naamruimte. In de praktijk geeft de naamruimte van een veld aan wie het veld heeft gemaakt (bijvoorbeeld standaard-XDM (Adobe), een leverancier of uw organisatie).

Neem bijvoorbeeld een XDM-schema dat gebruikmaakt van de [[!UICONTROL Personal Contact Details] veldgroep ](../field-groups/profile/demographic-details.md) , die een standaard `mobilePhone` veld heeft dat in de `xdm` naamruimte bestaat. In het zelfde schema, bent u ook vrij om een afzonderlijk `mobilePhone` gebied onder een verschillende namespace (uw [ huurder identiteitskaart ](../api/getting-started.md#know-your-tenant_id)) tot stand te brengen. Beide velden kunnen naast elkaar bestaan terwijl ze verschillende onderliggende betekenissen of beperkingen hebben.

## Syntaxis naamruimte

In de volgende secties ziet u hoe naamruimten worden toegewezen in XDM-syntaxis.

### Standaard XDM {#standard}

De standaard syntaxis XDM verstrekt inzicht in hoe namespaces in schema&#39;s (met inbegrip van [ worden vertegenwoordigd hoe zij in Adobe Experience Platform ](#compatibility) worden vertaald).

Standaard XDM gebruikt [ JSON-LD ](https://www.w3.org/TR/json-ld11/#basic-concepts) syntaxis om namespaces aan gebieden toe te wijzen. Deze naamruimte wordt geleverd in de vorm van een URI (bijvoorbeeld `https://ns.adobe.com/xdm` voor de `xdm` naamruimte) of als een voorvoegsel dat wordt geconfigureerd in het `@context` -kenmerk van een schema.

Hier volgt een voorbeeldschema voor een product in de standaard XDM-syntaxis. Met uitzondering van `@id` (de unieke id zoals gedefinieerd door de JSON-LD-specificatie), begint elk veld onder `properties` met een naamruimte en eindigt het met de veldnaam. Als u een voorvoegsel gebruikt dat is gedefinieerd onder `@context` , worden de naamruimte en de veldnaam gescheiden door een dubbele punt ( `:` ). Als u geen voorvoegsel gebruikt, worden de naamruimte en de veldnaam gescheiden door een schuine streep (`/`).

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
| `@context` | Een object dat de steno-voorvoegsels definieert die kunnen worden gebruikt in plaats van een volledige naamruimte-URI onder `properties` . |
| `@id` | Een uniek herkenningsteken voor het verslag zoals die door [ wordt bepaald JSON-LD spec ](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Een voorbeeld van een veld dat een voorvoegsel uit de steno gebruikt om een naamruimte aan te duiden. In dit geval is `xdm` de naamruimte (`https://ns.adobe.com/xdm`) en is `sku` de veldnaam. |
| `https://ns.adobe.com/xdm/channels/application` | Een voorbeeld van een veld dat de volledige naamruimte-URI gebruikt. In dit geval is `https://ns.adobe.com/xdm/channels` de naamruimte en is `application` de veldnaam. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Velden die worden geleverd door bronnen van leveranciers, gebruiken hun eigen unieke naamruimten. In dit voorbeeld is `https://ns.adobe.com/vendorA/product` de naamruimte van de leverancier en is `stockNumber` de veldnaam. |
| `tenantId:internalSku` | De gebieden die door uw organisatie worden bepaald gebruiken uw unieke huurdersidentiteitskaart als hun namespace. In dit voorbeeld is `tenantId` de naamruimte voor huurders ( `https://ns.adobe.com/tenantId` ) en is `internalSku` de veldnaam. |

{style="table-layout:auto"}

### Compatibiliteitsmodus {#compatibility}

In Adobe Experience Platform, worden de schema&#39;s XDM vertegenwoordigd in [ syntaxis van de Wijze van de Verenigbaarheid ](../api/appendix.md#compatibility), die niet de JSON-LD syntaxis gebruikt om namespaces te vertegenwoordigen. In plaats daarvan converteert Platform de naamruimte naar een bovenliggend veld (te beginnen met een onderstrepingsteken) en nest het de onderliggende velden.

De standaard-XDM `repo:createdDate` wordt bijvoorbeeld omgezet in `_repo.createdDate` en wordt weergegeven onder de volgende structuur in de compatibiliteitsmodus:

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

De gebieden die `xdm` gebruiken namespace verschijnen als wortelgebieden onder `properties` en laten vallen `xdm:` prefix die in [ standaardXDM syntaxis ](#standard) zou verschijnen. `xdm:sku` wordt bijvoorbeeld gewoon weergegeven als `sku` .

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

Deze handleiding biedt een overzicht van XDM-naamruimten en hoe deze worden weergegeven in JSON. Voor meer informatie over hoe te om schema&#39;s XDM te vormen gebruikend API, zie de [ gids van de Registratie API van het Schema ](../api/overview.md).
