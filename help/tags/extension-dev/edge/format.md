---
title: Bibliotheekmodules in Edge-extensies
description: Bibliotheekmodules opmaken voor tagextensies in een randeigenschap.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Bibliotheekmodules in Edge-extensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

>[!IMPORTANT]
>
>In dit document wordt de indeling van de module Bibliotheek voor randextensies besproken. Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids op [het formatteren van Webuitbreidingsmodules](../web/format.md).

Een bibliotheekmodule is een stuk herbruikbare code die door een extensie wordt geleverd en die wordt uitgegeven in de runtimebibliotheek van de tag in Adobe Experience Platform (de bibliotheek die op het randknooppunt wordt uitgevoerd). Bijvoorbeeld, zal een `sendBeacon` actietype een bibliotheekmodule hebben die op de randknoop zal lopen en een baken verzendt.

De bibliotheekmodule is gestructureerd als [CommonJS module](http://wiki.commonjs.org/wiki/Modules/1.1.1). Binnen een module CommonJS, zijn de volgende variabelen beschikbaar voor gebruik:

## [!DNL require]

Een functie `require` is beschikbaar voor u aan toegangsmodules binnen uw uitbreiding. Elke module in de extensie is toegankelijk via een relatief pad. Het relatieve pad moet beginnen met `./` of `../`.

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

Dit is een alternatief voor `module.exports` maar het gebruik ervan is beperkter. Lees [Understanding module.export and exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) voor een beter inzicht in de verschillen tussen `module.exports` en `exports` en de verwante bedenkingen met het gebruiken van `exports`. Als u twijfelt, maakt u uw leven makkelijker en gebruikt u `module.exports` in plaats van `exports`.

## Handtekening van de module Server-side

Alle moduletypes (gegevenselementen, voorwaarden, of acties) die door uw uitbreiding worden verstrekt zullen met de zelfde parameters worden geroepen: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
