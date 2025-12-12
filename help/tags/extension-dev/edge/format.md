---
title: Bibliotheekmodules in Edge-extensies
description: Bibliotheekmodules opmaken voor tagextensies in een randeigenschap.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Bibliotheekmodules in Edge-extensies

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor randextensies besproken. Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids op [&#x200B; het formatteren van de modules van de Webuitbreiding &#x200B;](../web/format.md).

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform (de bibliotheek die op het randknooppunt wordt uitgevoerd). Een actietype `sendBeacon` heeft bijvoorbeeld een bibliotheekmodule die op het randknooppunt wordt uitgevoerd en een baken verzendt.

De bibliotheekmodule is gestructureerd als module a [&#x200B; CommonJS &#x200B;](https://nodejs.org/api/modules.html#modules-commonjs-modules). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## [!DNL require]

Er is een functie `require` beschikbaar waarmee u toegang krijgt tot modules in uw extensie. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../` .

Voorbeeld:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Er is een gratis variabele met de naam `module` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Er is een gratis variabele met de naam `exports` beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```js
exports.sayHello = (…) => { … }
```

Dit is een alternatief voor `module.exports` maar het gebruik ervan is beperkter. Gelieve te lezen [&#x200B; Begrijpend module.exporting en de uitvoer in node.js &#x200B;](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de verwante bedenkingen met het gebruiken `exports`. Als u twijfelt, maakt u uw leven makkelijker en gebruikt u `module.exports` in plaats van `exports` .

## Handtekening van de module Server-side

Alle moduletypes (gegevenselementen, voorwaarden, of acties) die door uw uitbreiding worden verstrekt zullen met de zelfde parameters worden geroepen: [&#x200B; context &#x200B;](./context.md).

```js
exports.sayHello = (context) => { … }
```
