---
title: De SDK van Adobe Experience Platform Web installeren
description: Leer hoe te om het Web SDK van het Experience Platform te installeren.
keywords: web sdk installatie;installeren web sdk;Internet Explorer;promise;npm pakket
translation-type: tm+mt
source-git-commit: 63c0c5cae5ca2800b1f049b2b33e2a6f36ee7255
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---


# SDK {#installing-the-sdk} installeren

Er zijn drie ondersteunde manieren om Adobe Experience Platform Web SDK te gebruiken:

1. De aangewezen manier om SDK van het Web van Adobe Experience Platform te gebruiken is via [Adobe Experience Platform Launch](https://launch.adobe.com/).
1. De SDK van het Web van Adobe Experience Platform is ook beschikbaar op een netwerk van de inhoudslevering (CDN) voor u aan gebruik.
1. Gebruik de NPM-bibliotheek die EcmaScript 5- en EcmaScript 2015 (ES6)-modules exporteert.

## Optie 1: De Adobe Experience Platform Launch-extensie installeren

Raadpleeg de [startdocumentatie](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) voor documentatie over de Adobe Experience Platform Launch-extensie

## Optie 2: De vooraf gebouwde zelfstandige versie installeren

De vooraf gebouwde versie is beschikbaar op een CDN. U kunt de bibliotheek op CDN rechtstreeks op uw pagina van verwijzingen voorzien, of het downloaden en ontvangen op uw eigen infrastructuur. Het is beschikbaar in geminiatuurde en ongeminificeerde formaten. De ongeminificeerde versie is handig voor foutopsporingsdoeleinden.

URL-structuur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OF alloy.js voor de niet-geminificeerde versie.

Bijvoorbeeld:


* Gepiliseerd: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js)
* Niet-geminificeerd: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js)


### De code {#adding-the-code} toevoegen

Voor de vooraf samengestelde zelfstandige versie is een &quot;basiscode&quot; vereist die rechtstreeks aan de pagina wordt toegevoegd. Kopieer en plak de volgende &quot;basiscode&quot; zo hoog mogelijk in de `<head>`-tag van uw HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

De &quot;basiscode&quot; maakt een algemene functie met de naam `alloy`. Gebruik deze functie om te communiceren met de SDK. Als u de algemene functie een andere naam wilt geven, wijzigt u de naam `alloy` als volgt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

In dit voorbeeld wordt de naam van de algemene functie gewijzigd in `mycustomname` in plaats van `alloy`.

>[!IMPORTANT]
>
>Om potentiële problemen te vermijden, gebruik een naam die minstens één karakter bevat dat geen cijfer is en dat niet met de naam van een bezit strijdig is dat reeds op `window` wordt gevonden.

Deze basiscode laadt, naast het maken van een algemene functie, ook extra code in een extern bestand \(`alloy.js`\) dat op een server wordt gehost. Deze code wordt standaard asynchroon geladen, zodat de webpagina zo goed mogelijk presteert. Dit is de aanbevolen implementatie.

### Ondersteuning voor Internet Explorer {#support-internet-explore}

Deze SDK gebruikt beloftes, die een methode zijn om de voltooiing van asynchrone taken mee te delen. De [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers behalve [!DNL Internet Explorer]. Als u de SDK op [!DNL Internet Explorer] wilt gebruiken, moet u `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill) hebben.

Bepalen of `window.Promise` al is gevuld:

1. Open uw website in [!DNL Internet Explorer].
1. Open de foutopsporingsconsole van de browser.
1. Typ `window.Promise` in de console en druk vervolgens op Enter.

Als er iets anders dan `undefined` wordt weergegeven, hebt u waarschijnlijk al een polyfill `window.Promise`. Een andere manier om te bepalen of `window.Promise` is gevuld, is door uw website te laden nadat u de bovenstaande installatie-instructies hebt voltooid. Als de SDK een fout genereert die iets over een belofte noemt, hebt u waarschijnlijk niet gepolymeerd `window.Promise`.

Als u hebt bepaald dat u `window.Promise` moet opvullen, omvat de volgende manuscriptmarkering boven de eerder verstrekte basiscode:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Met deze tag wordt een script geladen waarmee wordt gegarandeerd dat `window.Promise` een geldige Promise-implementatie is.

>[!NOTE]
>
>Als u ervoor kiest om een andere Promise-implementatie te laden, moet u ervoor zorgen dat `Promise.prototype.finally` wordt ondersteund.

### Het JavaScript-bestand synchroon {#loading-javascript-synchronously} laden

Zoals uitgelegd in de sectie [De code toevoegen](#adding-the-code), laadt de basiscode u in HTML van uw website hebt gekopieerd en gekleefd een extern dossier. Het externe bestand bevat de kernfunctionaliteit van de SDK. Elke opdracht die u probeert uit te voeren terwijl dit bestand wordt geladen, wordt in de wachtrij geplaatst en verwerkt nadat het bestand is geladen. Het asynchroon laden van het bestand is de best presterende installatiemethode.

Onder bepaalde omstandigheden kunt u het bestand echter synchroon laden \(meer details over deze omstandigheden worden later gedocumenteerd\). Hierdoor wordt voorkomen dat de rest van het HTML-document door de browser wordt geparseerd en gerenderd totdat het externe bestand is geladen en uitgevoerd. Deze extra vertraging voordat primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de omstandigheden, zinvol zijn.

Als u het bestand synchroon in plaats van asynchroon wilt laden, verwijdert u het `async`-kenmerk uit de tweede `script`-tag, zoals hieronder wordt weergegeven:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js"></script>
```

## Optie 3: Het NPM-pakket gebruiken

Adobe Experience Platform Web SDK is ook beschikbaar als een NPM-pakket. [](https://www.npmjs.com) NPMis pakketbeheer voor JavaScript. Door het NPM-pakket te installeren, hebt u controle over het ontwikkelproces voor de Adobe Experience Platform Web SDK JavaScript. Het NPM-pakket stelt EcmaScript versie 5-modules of EcmaScript versie 2015 (ES6)-modules beschikbaar die in de browser moeten worden uitgevoerd.

```bash
npm install @adobe/alloy
```

Het NPM-pakket van de Adobe Experience Platform Web SDK stelt een functie `createInstance` beschikbaar. Deze functie wordt gebruikt om een instantie te maken. De naamoptie die aan de functie wordt doorgegeven, bepaalt het voorvoegsel dat wordt gebruikt bij het vastleggen. Hieronder staan voorbeelden van het gebruik van het pakket.

### Het pakket gebruiken als een ECMAScript 2015 (ES6)-module

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Het pakket gebruiken als een ECMAScript 5-module

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Ondersteuning voor Internet Explorer

De Adobe Experience Platform SDK gebruikt beloftes, die een manier zijn om de voltooiing van asynchrone taken mee te delen. De [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers behalve [!DNL Internet Explorer]. Als u de SDK op [!DNL Internet Explorer] wilt gebruiken, moet u `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill) hebben.

Eén bibliotheek die u kunt gebruiken voor veelvuldige beloftes is promise-polyfill. Raadpleeg de [promise-polyfill documentatie](https://www.npmjs.com/package/promise-polyfill) voor meer informatie over het installeren met NPM.

>[!NOTE]
>
>Als u ervoor kiest om een andere Promise-implementatie te laden, moet u ervoor zorgen dat `Promise.prototype.finally` wordt ondersteund.