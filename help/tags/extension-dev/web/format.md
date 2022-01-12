---
title: Bibliotheekmodules in webextensies
description: Leer hoe u bibliotheekmodules kunt opmaken voor webextensies in Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Bibliotheekmodules in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie de gids op [opmaken van Edge-uitbreidingsmodules](../edge/format.md) in plaats daarvan.

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform. Deze bibliotheek wordt vervolgens op de website van de client uitgevoerd. Bijvoorbeeld een `gesture` gebeurtenistype heeft een bibliotheekmodule die op de website van de client wordt uitgevoerd en gebruikersbewegingen detecteert.

De module Bibliotheek is gestructureerd als een [CommonJS-module](https://nodejs.org/api/modules.html#modules-commonjs-modules). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## [!DNL require]

A `require` -functie is beschikbaar voor u:

1. Kernmodules geleverd door tags. Deze modules kunnen worden betreden door te gebruiken `require('@adobe/reactor-name-of-module')`. Het document is beschikbaar [kernmodules](./core.md) voor meer informatie .
1. Andere modules in uw extensie. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../`.

Voorbeeld:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

Een gratis variabele met de naam `module` is beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

Een gratis variabele met de naam `exports` is beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
exports.sayHello = function(…) { … }
```

Dit is een alternatief voor `module.exports` maar heeft een beperkter gebruik. Lees [Het begrip module.export en de uitvoer in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de hiermee samenhangende waarschuwingen bij het gebruik `exports`. Als u twijfelt, maak dan uw leven makkelijker en gebruik `module.exports` eerder dan `exports`.

## Uitvoering en caching

Wanneer de tagruntime-bibliotheek wordt uitgevoerd, worden de modules onmiddellijk &quot;geïnstalleerd&quot; en wordt de exportcache van deze modules geplaatst. Uitgaande van de volgende module:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` wordt onmiddellijk gelogd, terwijl `runs when necessary` wordt alleen geregistreerd als de geëxporteerde functie wordt aangeroepen door de tagengine. Hoewel dit niet nodig kan zijn voor het doel van uw specifieke module, kunt u hiervan profiteren door de vereiste instellingen uit te voeren voordat u de functie exporteert.
