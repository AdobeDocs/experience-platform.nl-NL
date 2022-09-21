---
title: De SDK van Adobe Experience Platform Web installeren
description: Leer hoe te om het Web SDK van het Experience Platform te installeren.
keywords: web sdk installatie;installeren web sdk;Internet Explorer;promise;npm pakket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# De SDK installeren {#installing-the-sdk}

Er zijn drie ondersteunde manieren om Adobe Experience Platform Web SDK te gebruiken:

1. De aangewezen manier om het Web SDK van Adobe Experience Platform te gebruiken is via de UI van de Inzameling van Gegevens of Experience Platform UI.
1. De SDK van het Web van Adobe Experience Platform is ook beschikbaar op een netwerk van de inhoudslevering (CDN) voor u aan gebruik.
1. Gebruik de NPM-bibliotheek die EcmaScript 5- en EcmaScript 2015 (ES6)-modules exporteert.

## Optie 1: De tagextensie installeren

Raadpleeg voor documentatie over de tagextensie de [documentatie starten](../../tags/extensions/web/sdk/overview.md)

## Optie 2: De vooraf gebouwde zelfstandige versie installeren

De vooraf gebouwde versie is beschikbaar op een CDN. U kunt de bibliotheek op CDN rechtstreeks op uw pagina van verwijzingen voorzien, of het downloaden en ontvangen op uw eigen infrastructuur. Het is beschikbaar in geminiatuurde en ongeminificeerde formaten. De ongeminificeerde versie is handig voor foutopsporingsdoeleinden.

URL-structuur: https://cdn1.adoberesources.net/alloy/[VERSIE]/alloy.min.js OR alloy.js voor de niet-geminificeerde versie.

Bijvoorbeeld:


* Gepiliseerd: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Niet-geminificeerd: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### De code toevoegen {#adding-the-code}

Voor de vooraf samengestelde zelfstandige versie is een &quot;basiscode&quot; vereist die rechtstreeks aan de pagina wordt toegevoegd. Kopieer en plak de volgende &quot;basiscode&quot; zo hoog mogelijk in het deelvenster `<head>` tag van uw HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

De &quot;basiscode&quot; maakt een algemene functie met de naam `alloy`. Gebruik deze functie om te communiceren met de SDK. Als u de algemene functie een andere naam wilt geven, wijzigt u de instelling `alloy` naam als volgt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

In dit voorbeeld wordt de naam van de algemene functie gewijzigd `mycustomname`, in plaats van `alloy`.

>[!IMPORTANT]
>
>U voorkomt mogelijke problemen door een naam te gebruiken die ten minste één teken bevat dat geen cijfer is en dat niet conflicteert met de naam van een eigenschap die al is gevonden op `window`.

Deze basiscode laadt, naast het maken van een algemene functie, ook aanvullende code in een extern bestand \(`alloy.js`\) gehost op een server. Deze code wordt standaard asynchroon geladen, zodat de webpagina zo goed mogelijk presteert. Dit is de aanbevolen implementatie.

### Ondersteuning voor Internet Explorer {#support-internet-explore}

Deze SDK gebruikt beloftes, die een methode zijn om de voltooiing van asynchrone taken mee te delen. De [beloften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers, behalve [!DNL Internet Explorer]. De SDK gebruiken op [!DNL Internet Explorer]moet u `window.Promise` [polygevuld](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Bepalen of u al `window.Promise` polygevuld:

1. Uw website openen in [!DNL Internet Explorer].
1. Open de foutopsporingsconsole van de browser.
1. Type `window.Promise` in de console, dan druk binnengaan.

Als iets anders dan `undefined` wordt weergegeven, hebt u waarschijnlijk al een polyvulling `window.Promise`. Een andere manier om te bepalen of `window.Promise` wordt gevuld door uw website te laden nadat u de bovenstaande installatie-instructies hebt voltooid. Als de SDK een fout genereert die iets over een belofte vermeldt, hebt u waarschijnlijk niet gepolymeerd `window.Promise`.

Als u hebt bepaald moet u polyfill `window.Promise`neemt u de volgende scripttag op boven de eerder opgegeven basiscode:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Met deze tag wordt een script geladen dat ervoor zorgt dat `window.Promise` is een geldige Promise-implementatie.

>[!NOTE]
>
>Als u een andere Promise-implementatie wilt laden, moet u ervoor zorgen dat deze ondersteuning biedt `Promise.prototype.finally`.

### Het JavaScript-bestand synchroon laden {#loading-javascript-synchronously}

Zoals uitgelegd in de sectie [De code toevoegen](#adding-the-code)Met de basiscode die u hebt gekopieerd en in de HTML van uw website hebt geplakt, wordt een extern bestand geladen. Het externe bestand bevat de kernfunctionaliteit van de SDK. Elke opdracht die u probeert uit te voeren terwijl dit bestand wordt geladen, wordt in de wachtrij geplaatst en verwerkt nadat het bestand is geladen. Het asynchroon laden van het bestand is de best presterende installatiemethode.

Onder bepaalde omstandigheden kunt u het bestand echter synchroon laden \(meer details over deze omstandigheden worden later gedocumenteerd\). Als u dit doet, wordt de rest van het HTML-document niet geparseerd en gerenderd door de browser totdat het externe bestand is geladen en uitgevoerd. Deze extra vertraging voordat primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de omstandigheden, zinvol zijn.

Als u het bestand synchroon in plaats van asynchroon wilt laden, verwijdert u de knop `async` kenmerk van de tweede `script` tag zoals hieronder weergegeven:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## Optie 3: Het NPM-pakket gebruiken

Adobe Experience Platform Web SDK is ook beschikbaar als een NPM-pakket. [NPM](https://www.npmjs.com) is pakketbeheer voor JavaScript. Door het NPM-pakket te installeren, hebt u controle over het ontwikkelproces voor de Adobe Experience Platform Web SDK JavaScript. Het NPM-pakket stelt EcmaScript versie 5-modules of EcmaScript versie 2015 (ES6)-modules beschikbaar die in de browser moeten worden uitgevoerd.

```bash
npm install @adobe/alloy
```

Het NPM-pakket van de Adobe Experience Platform Web SDK stelt een `createInstance` functie. Deze functie wordt gebruikt om een instantie te maken. De naamoptie die aan de functie wordt doorgegeven, bepaalt het voorvoegsel dat wordt gebruikt bij het vastleggen. Hieronder staan voorbeelden van het gebruik van het pakket.

### Het pakket gebruiken als een ECMAScript 2015 (ES6)-module

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Het NPM-pakket is gebaseerd op CommonJS-modules; daarom wanneer het gebruiken van een bundelaar, zorg ervoor de bundelaar modules CommonJS steunt. Sommige bundels, zoals [Rollup](https://rollupjs.org)vereist een [insteekmodule](https://www.npmjs.com/package/@rollup/plugin-commonjs) die ondersteuning biedt voor CommonJS.

### Het pakket gebruiken als een ECMAScript 5-module

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Ondersteuning voor Internet Explorer

De Adobe Experience Platform SDK gebruikt beloftes, die een manier zijn om de voltooiing van asynchrone taken mee te delen. De [beloften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers, behalve [!DNL Internet Explorer]. De SDK gebruiken op [!DNL Internet Explorer]moet u `window.Promise` [polygevuld](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Eén bibliotheek die u kunt gebruiken voor veelvuldige beloftes is promise-polyfill. Zie de [promise-polyfill-documentatie](https://www.npmjs.com/package/promise-polyfill) voor meer informatie over het installeren met NPM.

>[!NOTE]
>
>Als u een andere Promise-implementatie wilt laden, moet u ervoor zorgen dat deze ondersteuning biedt `Promise.prototype.finally`.
