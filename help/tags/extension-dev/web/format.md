---
title: Bibliotheekmodules in webextensies
description: Leer hoe u bibliotheekmodules kunt opmaken voor webextensies in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Bibliotheekmodules in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie in plaats daarvan de gids op [het formatteren van de modules van de randuitbreiding](../edge/format.md).

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform. Deze bibliotheek wordt vervolgens op de website van de client uitgevoerd. Een `gesture`-gebeurtenistype heeft bijvoorbeeld een bibliotheekmodule die wordt uitgevoerd op de website van de client en waarmee bewegingen van de gebruiker worden gedetecteerd.

De bibliotheekmodule is gestructureerd als [CommonJS module](http://wiki.commonjs.org/wiki/Modules/1.1.1). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## [!DNL require]

U hebt toegang tot een functie `require`:

1. Kernmodules geleverd door tags. Deze modules kunnen worden betreden door `require('@adobe/reactor-name-of-module')` te gebruiken. Zie het document over beschikbare [kernmodules](./core.md) voor meer informatie.
1. Andere modules in uw extensie. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../`.

Voorbeeld:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

Er is een gratis variabele met de naam `module` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

Er is een gratis variabele met de naam `exports` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
exports.sayHello = function(…) { … }
```

Dit is een alternatief voor `module.exports` maar het gebruik ervan is beperkter. Lees [Understanding module.export and exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de verwante bedenkingen met het gebruiken van `exports`. Als u twijfelt, maakt u uw leven makkelijker en gebruikt u `module.exports` in plaats van `exports`.

## Uitvoering en caching

Wanneer de tagruntime-bibliotheek wordt uitgevoerd, worden de modules onmiddellijk &quot;geïnstalleerd&quot; en wordt de exportcache van deze modules geplaatst. Uitgaande van de volgende module:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` worden onmiddellijk geregistreerd, maar  `runs when necessary` worden pas geregistreerd wanneer de geëxporteerde functie wordt aangeroepen door de tagengine. Hoewel dit niet nodig kan zijn voor het doel van uw specifieke module, kunt u hiervan profiteren door de vereiste instellingen uit te voeren voordat u de functie exporteert.
