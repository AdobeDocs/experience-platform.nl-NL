---
title: Bibliotheekmodules in Edge-extensies
description: Bibliotheekmodules opmaken voor tagextensies in een randeigenschap.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Bibliotheekmodules in Edge-extensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor randextensies besproken. Als u een webextensie ontwikkelt, raadpleegt u de handleiding op [opmaken van webextensiemodules](../web/format.md) in plaats daarvan.

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform (de bibliotheek die op het randknooppunt wordt uitgevoerd). Bijvoorbeeld een `sendBeacon` actietype zal een bibliotheekmodule hebben die op de randknoop zal lopen en een baken zal verzenden.

De module Bibliotheek is gestructureerd als een [CommonJS-module](https://nodejs.org/api/modules.html#modules-commonjs-modules). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## [!DNL require]

A `require` Deze functie is beschikbaar voor u om tot modules binnen uw uitbreiding toegang te hebben. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../`.

Voorbeeld:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Een gratis variabele met de naam `module` is beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Een gratis variabele met de naam `exports` is beschikbaar waarmee u de API van de module kunt exporteren.

Voorbeeld:

```js
exports.sayHello = (…) => { … }
```

Dit is een alternatief voor `module.exports` maar heeft een beperkter gebruik. Lees [Het begrip module.export en de uitvoer in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de hiermee samenhangende waarschuwingen bij het gebruik `exports`. Als u twijfelt, maak dan uw leven makkelijker en gebruik `module.exports` eerder dan `exports`.

## Handtekening van de module Server-side

Alle moduletypes (gegevenselementen, voorwaarden, of acties) die door uw uitbreiding worden verstrekt zullen met de zelfde parameters worden geroepen: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
