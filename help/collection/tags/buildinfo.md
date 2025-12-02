---
title: buildInfo
description: Verkrijg informatie over de tag die op uw site is geïmplementeerd.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

Het `_satellite.buildInfo` -object bevat informatie over de build van de geïmplementeerde eigenschap tag. Dit object is vooral handig bij het opsporen van fouten in veelvuldige builds om ervoor te zorgen dat u de meest recente versie gebruikt.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Beschikbare velden

De volgende velden zijn beschikbaar wanneer u dit object aanroept.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Naam | Type | Beschrijving |
| --- | --- | --- |
| **`minified`** | `boolean` | Hiermee wordt aangegeven of de bibliotheek is geminiaterd. Productiebuilds worden doorgaans geminiateerd (`true`), terwijl ontwikkelings- en staging builds doorgaans niet (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | De datum en tijd waarop uw JavaScript-bestand is gemaakt en gepubliceerd. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [&#x200B; Turbine &#x200B;](https://github.com/adobe/reactor-turbine) is de motor van Adobe die markeringsregels verwerkt en logica delegeert aan markeringsuitbreidingen. Dit gebied bevat de datum en de tijd van de Turbine bouwstijl die wordt gebruikt om uw markeringsbezit te publiceren. |
| **`turbineVersion`** | `string` | De versie van Turbine die wordt gebruikt om uw markeringsbezit te bouwen en te publiceren. |

Vergelijkbare informatie vindt u ook in `_satellite._container.buildInfo` . Zie [`_container`](container.md) voor meer informatie.
