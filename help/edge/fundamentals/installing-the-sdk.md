---
title: De SDK van het Web Adobe Experience Platform installeren
seo-title: Adobe Experience Platform Web SDK die SDK installeert
description: Leer hoe te om SDK van het Web van het Experience Platform te installeren
seo-description: Leer hoe te om SDK van het Web van het Experience Platform te installeren
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# De SDK installeren {#installing-the-sdk}

Het Adobe Experience Platform [!DNL Web SDK] is beschikbaar op een netwerk van de inhoudslevering (CDN) voor u aan gebruik. U kunt naar dit bestand verwijzen of het downloaden en op uw eigen infrastructuur hosten. Het is beschikbaar in een geminificeerde en niet-geminiaterde versie. De niet-geminificeerde versie is handig voor foutopsporingsdoeleinden.

* GeMinificeerde versie: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)
* Niet-geminificeerde versie: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## De code toevoegen {#adding-the-code}

De eerste stap bij het implementeren van het Adobe Experience Platform [!DNL Web SDK] is het zo hoog mogelijk kopiëren en plakken van de volgende &quot;basiscode&quot; in de `<head>` tag van uw HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

De basiscode maakt een algemene functie met de naam `alloy`. Gebruik deze functie om te communiceren met de SDK. Als u de algemene functie een andere naam wilt geven, kunt u de `alloy` naam als volgt wijzigen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

In dit voorbeeld wordt de naam van de algemene functie gewijzigd `mycustomname`in plaats van `alloy`.

>[!IMPORTANT]
>U voorkomt mogelijke problemen door een naam te gebruiken die ten minste één teken bevat dat geen cijfer is en dat niet conflicteert met de naam van een eigenschap die al is gevonden op `window`.

Deze basiscode laadt, naast het maken van een algemene functie, ook extra code in een extern bestand \(`alloy.js`\) dat op een server wordt gehost. Deze code wordt standaard asynchroon geladen, zodat de webpagina zo goed mogelijk presteert. Dit is de aanbevolen implementatie.

## Ondersteuning voor Internet Explorer {#support-internet-explore}

Deze SDK maakt gebruik van beloften, een methode om de voltooiing van asynchrone taken mee te delen. De [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) -implementatie die door de SDK wordt gebruikt, wordt native ondersteund door alle doelbrowsers behalve [!DNL Internet Explorer]. Als u de SDK wilt gebruiken [!DNL Internet Explorer], moet u `window.Promise` gepolymeerd [](https://remysharp.com/2010/10/08/what-is-a-polyfill)zijn.

U kunt als volgt bepalen of u al een `window.Promise` polyvulling hebt:

1. Open uw website in [!DNL Internet Explorer].
1. Open de foutopsporingsconsole van de browser.
1. Typ `window.Promise` de code in de console en druk op Enter.

Als er iets anders dan `undefined` wordt weergegeven, hebt u waarschijnlijk al een polyvulling `window.Promise`. Een andere manier om te bepalen of `window.Promise` er al dan niet meerdere ingevulde gegevens zijn, is door uw website te laden nadat u de bovenstaande installatie-instructies hebt uitgevoerd. Als de SDK een fout genereert die iets over een belofte vermeldt, hebt u waarschijnlijk niet gepolymeerd `window.Promise`.

Als u hebt vastgesteld dat u moet polyfill `window.Promise`, neemt u de volgende scripttag op boven de eerder opgegeven basiscode:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dit laadt een manuscript dat ervoor zorgt dat dat een geldige implementatie van het Vermogen `window.Promise` is.

## Het JavaScript-bestand synchroon laden {#loading-javascript-synchronously}

Zoals uitgelegd in de sectie [De code](#adding-the-code)toevoegen, laadt de basiscode die u hebt gekopieerd en in HTML van uw website hebt geplakt een extern bestand met extra code. Deze extra code bevat de kernfunctionaliteit van de SDK. Elke opdracht die u probeert uit te voeren terwijl dit bestand wordt geladen, wordt in de wachtrij geplaatst en verwerkt nadat het bestand is geladen. Dit is de best presterende installatiemethode.

Onder bepaalde omstandigheden kunt u het bestand echter synchroon laden \(meer details over deze omstandigheden worden later gedocumenteerd\). Hierdoor wordt voorkomen dat de rest van het HTML-document door de browser wordt geparseerd en gerenderd totdat het externe bestand is geladen en uitgevoerd. Deze extra vertraging voordat primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan afhankelijk van de omstandigheden zinvol zijn.

Als u het bestand synchroon in plaats van asynchroon wilt laden, verwijdert u het `async` kenmerk uit de tweede `script` tag, zoals hieronder wordt weergegeven:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
