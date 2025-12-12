---
title: Bibliotheekmodules in webextensies
description: Leer hoe u bibliotheekmodules kunt opmaken voor webextensies in Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Bibliotheekmodules in webextensies

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie in plaats daarvan de gids op [ het formatteren van de modules van de randuitbreiding ](../edge/format.md).

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform. Deze bibliotheek wordt vervolgens op de website van de client uitgevoerd. Een `gesture` -gebeurtenistype heeft bijvoorbeeld een bibliotheekmodule die wordt uitgevoerd op de website van de client en waarmee gebruikersbewegingen worden gedetecteerd.

De bibliotheekmodule is gestructureerd als module a [ CommonJS ](https://nodejs.org/api/modules.html#modules-commonjs-modules). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## `require`

U hebt toegang tot een functie `require` :

1. Kernmodules geleverd door tags. Deze modules zijn toegankelijk via `require('@adobe/reactor-name-of-module')` . Zie het document op beschikbare [ kernmodules ](./core.md) voor meer informatie.
1. Andere modules in uw extensie. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../` .

Voorbeeld:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

Er is een gratis variabele met de naam `module` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

Er is een gratis variabele met de naam `exports` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```javascript
exports.sayHello = function(…) { … }
```

Dit is een alternatief voor `module.exports` maar het gebruik ervan is beperkter. Gelieve te lezen [ Begrijpend module.exporting en de uitvoer in node.js ](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de verwante bedenkingen met het gebruiken `exports`. Als u twijfelt, maakt u uw leven makkelijker en gebruikt u `module.exports` in plaats van `exports` .

## Uitvoering en caching

Wanneer de tagruntime-bibliotheek wordt uitgevoerd, worden de modules onmiddellijk &quot;geïnstalleerd&quot; en wordt de exportcache van deze modules geplaatst. Uitgaande van de volgende module:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` wordt direct geregistreerd, terwijl `runs when necessary` alleen wordt vastgelegd wanneer de geëxporteerde functie wordt aangeroepen door de tagengine. Hoewel dit niet nodig kan zijn voor het doel van uw specifieke module, kunt u hiervan profiteren door de vereiste instellingen uit te voeren voordat u de functie exporteert.
