---
title: Core Library Modules voor Web Extensions
description: Leer meer over de kernbibliotheekmodules die u kunt gebruiken in uw webextensies.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Kernbibliotheekmodules voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document bevat een lijst met kernmodules voor bibliotheken die u kunt gebruiken in uw webextensies. U kunt deze modules gebruiken `require('@adobe/{MODULE}')`, waarbij `{MODULE}` is de naam van de kernmodule die u wilt gebruiken.

## [!DNL reactor-object-assign]

`reactor-object-assign` native simuleren [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) door eigenschappen van bronobjecten naar een doelobject te kopiëren.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

De `reactor-cookie` -object is een hulpprogramma voor het lezen en schrijven van cookies. Zie de [npm-pakket js-cookie](https://www.npmjs.com/package/js-cookie) voor meer informatie .

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` vertegenwoordigt [`Document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) object. Dit kan nuttig zijn bij het testen van de module door tests toe te staan om een mock te injecteren `document` object met hulpprogramma&#39;s als [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` is een nut voor het ontleden en het rangschikken [querytekenreeksen](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

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

* `queryString.parse({STRING})`: Parseert een queryreeks in een object. Regelafstand `?`, `#`, en `&` tekens in de queryreeks worden genegeerd.
* `queryString.stringify({OBJECT})`: Hiermee wordt een object geordend in een queryreeks.

### [!DNL reactor-load-script]

`reactor-load-script` is een functie die een script laadt wanneer een URL wordt opgegeven. Er wordt een scripttag gemaakt en in het dialoogvenster `head` van het document. A [beloven](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) worden geretourneerd die u kunt gebruiken om te bepalen wanneer het laden van het script slaagt of mislukt.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` is een constructor die de [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) in ECMAScript 6. Als de native Promise-API beschikbaar is, wordt deze geretourneerd.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` vertegenwoordigt [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) object. Dit kan nuttig zijn bij het testen van de module door tests toe te staan om een mock te injecteren `Window` object met hulpprogramma&#39;s als [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
