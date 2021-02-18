---
title: De SDK van Adobe Experience Platform Web installeren
description: Leer hoe te om het Web SDK van het Experience Platform te installeren.
keywords: web sdk installatie;installeren web sdk;Internet Explorer;promise;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# SDK {#installing-the-sdk} installeren

De aangewezen manier om SDK van het Web van Adobe Experience Platform te gebruiken is via [Adobe Experience Platform Launch](http://launch.adobe.com/). Zoek naar `AEP Web SDK` in de catalogus van uitbreidingen, installeer dan de uitbreiding.

Adobe Experience Platform Web SDK is ook beschikbaar op een CDN voor u aan gebruik. U kunt naar dit bestand verwijzen of het downloaden en op uw eigen infrastructuur hosten. Het is beschikbaar in een geminificeerde en niet-geminiaterde versie. De niet-geminificeerde versie is handig voor foutopsporingsdoeleinden.

URL-structuur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OF alloy.js voor de niet-geminificeerde versie.

Bijvoorbeeld:

* Gepiliseerd: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* Niet-geminificeerd: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## De code {#adding-the-code} toevoegen

De eerste stap bij het implementeren van Adobe Experience Platform [!DNL Web SDK] bestaat uit het zo hoog mogelijk kopiëren en plakken van de volgende &quot;basiscode&quot; in de tag `<head>` van uw HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

De basiscode maakt een algemene functie met de naam `alloy`. Gebruik deze functie om te communiceren met de SDK. Als u de algemene functie een andere naam wilt geven, kunt u de naam `alloy` als volgt wijzigen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

In dit voorbeeld wordt de naam van de algemene functie gewijzigd in `mycustomname` in plaats van `alloy`.

>[!IMPORTANT]
>
>Om potentiële problemen te vermijden, gebruik een naam die minstens één karakter bevat dat geen cijfer is en dat niet met de naam van een bezit strijdig is dat reeds op `window` wordt gevonden.

Deze basiscode laadt, naast het maken van een algemene functie, ook extra code in een extern bestand \(`alloy.js`\) dat op een server wordt gehost. Deze code wordt standaard asynchroon geladen, zodat de webpagina zo goed mogelijk presteert. Dit is de aanbevolen implementatie.

## Ondersteuning voor Internet Explorer {#support-internet-explore}

Deze SDK maakt gebruik van beloften, een methode om de voltooiing van asynchrone taken mee te delen. De [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers behalve [!DNL Internet Explorer]. Als u de SDK op [!DNL Internet Explorer] wilt gebruiken, moet u `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill) hebben.

Bepalen of `window.Promise` al is gevuld:

1. Open uw website in [!DNL Internet Explorer].
1. Open de foutopsporingsconsole van de browser.
1. Typ `window.Promise` in de console en druk vervolgens op Enter.

Als er iets anders dan `undefined` wordt weergegeven, hebt u waarschijnlijk al een polyfill `window.Promise`. Een andere manier om te bepalen of `window.Promise` is gevuld, is door uw website te laden nadat u de bovenstaande installatie-instructies hebt voltooid. Als de SDK een fout genereert die iets over een belofte noemt, hebt u waarschijnlijk niet gepolymeerd `window.Promise`.

Als u hebt bepaald u `window.Promise` moet polyfill, omvat de volgende manuscriptmarkering boven de eerder verstrekte basiscode:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Hiermee wordt een script geladen dat ervoor zorgt dat `window.Promise` een geldige Promise-implementatie is.

>[!NOTE]
>
>Als u ervoor kiest om een andere Promise-implementatie te laden, moet u ervoor zorgen dat `Promise.prototype.finally` wordt ondersteund.

## Het JavaScript-bestand synchroon {#loading-javascript-synchronously} laden

Zoals uitgelegd in de sectie [De code toevoegen](#adding-the-code), laadt de basiscode u in HTML van uw website hebt gekopieerd en gekleefd een extern dossier met extra code. Deze extra code bevat de kernfunctionaliteit van de SDK. Elke opdracht die u probeert uit te voeren terwijl dit bestand wordt geladen, wordt in de wachtrij geplaatst en verwerkt nadat het bestand is geladen. Dit is de best presterende installatiemethode.

Onder bepaalde omstandigheden kunt u het bestand echter synchroon laden \(meer details over deze omstandigheden worden later gedocumenteerd\). Hierdoor wordt voorkomen dat de rest van het HTML-document door de browser wordt geparseerd en gerenderd totdat het externe bestand is geladen en uitgevoerd. Deze extra vertraging voordat primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de omstandigheden, zinvol zijn.

Als u het bestand synchroon in plaats van asynchroon wilt laden, verwijdert u het `async`-kenmerk uit de tweede `script`-tag, zoals hieronder wordt weergegeven:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
