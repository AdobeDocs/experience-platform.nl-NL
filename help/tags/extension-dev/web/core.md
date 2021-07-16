---
title: Core Library Modules voor Web Extensions
description: Leer meer over de kernbibliotheekmodules die u kunt gebruiken in uw webextensies.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Kernbibliotheekmodules voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document bevat een lijst met kernmodules voor bibliotheken die u kunt gebruiken in uw webextensies. U kunt tot deze modules toegang hebben gebruikend `require('@adobe/{MODULE}')`, waar `{MODULE}` de naam van de kernmodule die wil gebruiken is.

## [!DNL reactor-object-assign]

`reactor-object-assign` Hiermee wordt de native  [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) methode nagebootst door eigenschappen van bronobjecten naar een doelobject te kopiëren.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

Het object `reactor-cookie` is een hulpprogramma voor het lezen en schrijven van cookies. Zie [js-cookie npm package](https://www.npmjs.com/package/js-cookie) voor meer informatie.

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` vertegenwoordigt het  [`Document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) object. Dit kan nuttig zijn wanneer het testen van de module door tests toe te staan om een mock `document` voorwerp te injecteren gebruikend nut zoals [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` is een nut voor het ontleden en het rangschikken van  [vraagkoorden](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

Het hulpprogramma heeft de volgende methoden:

* `queryString.parse({STRING})`: Parseert een queryreeks in een object. Voorlooptekens `?`, `#` en `&` in de queryreeks worden genegeerd.
* `queryString.stringify({OBJECT})`: Hiermee wordt een object geordend in een queryreeks.

### [!DNL reactor-load-script]

`reactor-load-script` is een functie die een script laadt wanneer een URL wordt opgegeven. Er wordt een scripttag gemaakt en in het knooppunt `head` van het document geplaatst. Een [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) zal worden teruggekeerd die u kunt gebruiken om te bepalen wanneer het laden van het manuscript slaagt of ontbreekt.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` is een constructor die de  [Promise ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) APInative in ECMAScript 6 nabootst. Als de native Promise-API beschikbaar is, wordt deze geretourneerd.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` vertegenwoordigt het  [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) object. Dit kan nuttig zijn wanneer het testen van de module door tests toe te staan om een mock `Window` voorwerp te injecteren gebruikend nut zoals [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
