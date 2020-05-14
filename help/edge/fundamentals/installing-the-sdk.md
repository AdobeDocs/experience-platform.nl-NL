---
title: De Adobe Experience Platform Web SDK installeren
seo-title: De SDK van Adobe Experience Platform Web SDK installeren
description: Leer hoe u de Experience Platform Web SDK installeert
seo-description: Leer hoe u de Experience Platform Web SDK installeert
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# De SDK installeren

De eerste stap bij de implementatie van de Adobe Experience Platform Web SDK is het zo hoog mogelijk kopiëren en plakken van de volgende &quot;basiscode&quot; in de `<head>` tag van uw HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

De basiscode maakt een algemene functie met de naam `alloy`. Gebruik deze functie om te communiceren met de SDK. Als u de algemene functie een andere naam wilt geven, kunt u de `alloy` naam als volgt wijzigen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

In dit voorbeeld wordt de naam van de algemene functie gewijzigd `mycustomname`in plaats van `alloy`.

>[!IMPORTANT]
>U voorkomt mogelijke problemen door een naam te gebruiken die ten minste één teken bevat dat geen cijfer is en dat niet conflicteert met de naam van een eigenschap die al is gevonden op `window`.

Deze basiscode laadt, naast het maken van een algemene functie, ook extra code in een extern bestand \(`alloy.js`\) dat op een server wordt gehost. Deze code wordt standaard asynchroon geladen, zodat de webpagina zo goed mogelijk presteert. Dit is de aanbevolen implementatie.

## Ondersteuning voor Internet Explorer

Deze SDK maakt gebruik van beloften, een methode om de voltooiing van asynchrone taken mee te delen. De [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) -implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers behalve Internet Explorer. Als u de SDK in Internet Explorer wilt gebruiken, moet u over `window.Promise` veelvouden [](https://remysharp.com/2010/10/08/what-is-a-polyfill)beschikken.

U kunt als volgt bepalen of u al een `window.Promise` polyvulling hebt:

1. Open uw website in Internet Explorer.
1. Open de foutopsporingsconsole van de browser.
1. Typ `window.Promise` de code in de console en druk op Enter.

Als er iets anders dan `undefined` wordt weergegeven, hebt u waarschijnlijk al een polyvulling `window.Promise`. Een andere manier om te bepalen of `window.Promise` er al dan niet meerdere ingevulde gegevens zijn, is door uw website te laden nadat u de bovenstaande installatie-instructies hebt uitgevoerd. Als de SDK een fout genereert die iets over een belofte vermeldt, hebt u waarschijnlijk niet gepolymeerd `window.Promise`.

Als u hebt vastgesteld dat u moet polyfill `window.Promise`, neemt u de volgende scripttag op boven de eerder opgegeven basiscode:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dit laadt een manuscript dat ervoor zorgt dat dat een geldige implementatie van het Vermogen `window.Promise` is.

## Het JavaScript-bestand synchroon laden

Zoals eerder is uitgelegd, laadt de basiscode die u hebt gekopieerd en in de HTML van uw website hebt geplakt een extern bestand met extra code. Deze extra code bevat de kernfunctionaliteit van de SDK. Elke opdracht die u probeert uit te voeren terwijl dit bestand wordt geladen, wordt in de wachtrij geplaatst en verwerkt nadat het bestand is geladen. Dit is de best presterende installatiemethode.

Onder bepaalde omstandigheden kunt u het bestand echter synchroon laden \(meer details over deze omstandigheden worden later gedocumenteerd\). Hierdoor wordt voorkomen dat de rest van het HTML-document door de browser wordt geparseerd en gerenderd totdat het externe bestand is geladen en uitgevoerd. Deze extra vertraging voordat primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan afhankelijk van de omstandigheden zinvol zijn.

Als u het bestand synchroon in plaats van asynchroon wilt laden, verwijdert u het `async` kenmerk uit de tweede `script` tag, zoals hieronder wordt weergegeven:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
