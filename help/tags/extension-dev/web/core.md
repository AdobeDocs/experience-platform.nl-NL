---
title: Core Library Modules voor Web Extensions
description: Leer meer over de kernbibliotheekmodules die u kunt gebruiken in uw webextensies.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Kernbibliotheekmodules voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Dit document bevat een lijst met kernmodules voor bibliotheken die u kunt gebruiken in uw webextensies. U hebt toegang tot deze modules met `require('@adobe/{MODULE}')` , waarbij `{MODULE}` de naam is van de kernmodule die u wilt gebruiken.

## [!DNL reactor-object-assign]

`reactor-object-assign` imiteert de inheemse [`Object.assign` ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) methode door eigenschappen van bronvoorwerpen aan een doelvoorwerp te kopiëren.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

Het `reactor-cookie` -object is een hulpprogramma voor het lezen en schrijven van cookies. Zie het [ js-koekje npm pakket ](https://www.npmjs.com/package/js-cookie) voor meer informatie.

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` vertegenwoordigt het [`Document` ](https://developer.mozilla.org/en-US/docs/Web/API/Document) voorwerp. Dit kan nuttig zijn wanneer het testen van de module door tests toe te staan om een mock `document` voorwerp te injecteren gebruikend nut zoals [`inject-loader` ](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` is een nut voor het ontleden en het in series vervaardigen van [ vraagkoorden ](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

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

* `queryString.parse({STRING})` : hiermee wordt een queryreeks in een object geparseerd. Voorlooptekens `?` , `#` en `&` in de queryreeks worden genegeerd.
* `queryString.stringify({OBJECT})` : hiermee wordt een object in een queryreeks geordend.

### [!DNL reactor-load-script]

`reactor-load-script` is een functie die een script laadt wanneer een URL wordt opgegeven. Er wordt een scripttag gemaakt en in het knooppunt `head` van het document geplaatst. A [ belofte ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) zal zijn teruggekeerd die u kunt gebruiken om te bepalen wanneer het laden van het manuscript slaagt of ontbreekt.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` is een aannemer die [ Promise API ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) inheems in ECMAScript 6 nastreeft. Als de native Promise-API beschikbaar is, wordt deze geretourneerd.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` vertegenwoordigt het [`Window` ](https://developer.mozilla.org/en-US/docs/Web/API/Window) voorwerp. Dit kan nuttig zijn wanneer het testen van de module door tests toe te staan om een mock `Window` voorwerp te injecteren gebruikend nut zoals [`inject-loader` ](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
