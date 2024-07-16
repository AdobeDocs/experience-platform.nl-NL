---
title: De SDK van het web installeren met de JavaScript-bibliotheek
description: Verwijs naar de bibliotheek van SDK van het Web gebruikend een standalone CDN dossier.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# De SDK van het web installeren met de JavaScript-bibliotheek

Een alternatief aan het installeren van SDK van het Web zonder [ het gebruiken van de markeringsuitbreiding ](extension.md) moet de bibliotheek van JavaScript van verwijzingen voorzien die op een CDN wordt ontvangen. U kunt rechtstreeks naar de bibliotheek verwijzen of deze downloaden en op uw eigen infrastructuur hosten. Het is beschikbaar in geminiatuurde en volledige formaten.

De SDK-bibliotheek van Web is beschikbaar via de volgende URL-structuur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Volledig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Zie de [ versienota&#39;s ](../release-notes.md) voor de recentste versie om in URL te omvatten. De URL voor de volledige versie van versie 2.19.1 is bijvoorbeeld `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js` .

## De code toevoegen

Voeg het volgende codeblok zo hoog mogelijk toe in de tag `<head>` van de HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Deze code leidt asynchroon tot een voorwerp `alloy` dat u toestaat om het even welk bevel van SDK van het Web te roepen. Als u de SDK van het Web synchroon wilt laden, kunt u het `async` attribuut in de laatste lijn van het codeblok verwijderen. Als u het kenmerk `async` verwijdert, wordt de rest van het HTML-document niet geparseerd en gerenderd door de browser totdat de bibliotheek wordt geladen en uitgevoerd. Deze extra vertraging voordat de primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de behoeften van uw organisatie, zinvol zijn.
