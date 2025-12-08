---
title: De Web SDK JavaScript-bibliotheek installeren
description: Verwijs naar de bibliotheek van SDK van het Web gebruikend een standalone CDN dossier.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# De Web SDK JavaScript-bibliotheek installeren

Een alternatief aan het installeren van het Web SDK zonder [ het gebruiken van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/overview.md) moet de bibliotheek van JavaScript van het Web van verwijzingen voorzien die op een CDN wordt ontvangen. U kunt rechtstreeks naar de bibliotheek verwijzen of deze downloaden en op uw eigen infrastructuur hosten. Het is beschikbaar in geminiatuurde en volledige formaten.

De Web SDK-bibliotheek is beschikbaar via de volgende URL-structuur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Volledig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Zie de [ versienota&#39;s ](../release-notes.md) voor de recentste versie om in URL te omvatten. De URL voor de volledige versie van versie 2.19.1 is bijvoorbeeld `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js` .

## De code toevoegen

Voeg het volgende codeblok zo hoog mogelijk toe in de tag `<head>` van uw HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Met deze code wordt asynchroon een `alloy` -object gemaakt waarmee u een Web SDK-opdracht kunt aanroepen. Als u het Web SDK synchroon wilt laden, kunt u het kenmerk `async` verwijderen in de laatste regel van het codeblok. Als u het kenmerk `async` verwijdert, wordt de rest van het HTML-document niet geparseerd en gerenderd door de browser totdat de bibliotheek wordt geladen en uitgevoerd. Deze extra vertraging voordat de primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de behoeften van uw organisatie, zinvol zijn.
