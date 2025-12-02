---
title: bedrijf
description: Verkrijg informatie rond de organisatie IMS die het uitgevoerde markeringsbezit bezit.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

Het `_satellite.company` -object geeft informatie weer over de IMS-organisatie die eigenaar is van de eigenschap tag.

```ts
readonly _satellite.company: Company
```

## Beschikbare velden

De volgende velden zijn beschikbaar wanneer u dit object aanroept:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Naam | Type | Beschrijving |
| --- | --- | --- |
| **`orgId`** | `string` | De IMS org-id van de eigenschap tag. |
| **`dynamicCdnEnabled`** | `boolean` | Hiermee wordt bepaald of de eigenschap tag gebruikmaakt van de Adobe-functie voor het dynamisch wisselen van een CDN. Indien ingesteld op `true` , wordt automatisch de CDN gewijzigd die een bezoeker opvraagt van uw tag op basis van zijn locatie. |
| **`cdnAllowList`** | `string[]` | De toegelaten CDNs om uw markeringsbezit van te laden. |

Vergelijkbare informatie vindt u ook in `_satellite._container.company` . Zie [`_container`](container.md) voor meer informatie.
