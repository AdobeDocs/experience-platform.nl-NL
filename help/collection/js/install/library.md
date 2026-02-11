---
title: De Web SDK JavaScript-bibliotheek installeren
description: Verwijs naar de bibliotheek van SDK van het Web gebruikend een standalone CDN dossier.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# De Web SDK JavaScript-bibliotheek installeren

Als u verkiest om de [&#x200B; de markeringsuitbreiding van SDK van het Web niet te gebruiken &#x200B;](/help/tags/extensions/client/web-sdk/overview.md), kunt u SDK van het Web installeren door naar de standalone bibliotheek van JavaScript te verwijzen die op Adobe CDN wordt ontvangen. U kunt rechtstreeks naar de bibliotheek verwijzen of deze downloaden en op uw eigen infrastructuur hosten. Het is beschikbaar in geminiatuurde en volledige formaten.

De Web SDK-bibliotheek is beschikbaar via de volgende URL-structuur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Volledig**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Zie de [&#x200B; de versienota&#39;s van SDK van het Web &#x200B;](../release-notes.md) voor de recentste versie om in URL te omvatten. De URL voor de volledige versie van versie 2.19.1 is bijvoorbeeld `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js` .

## Basiscode en bibliotheeklader toevoegen

De toe te voegen code bestaat uit twee secties:

* **code van de Basis**: Staat bootstrapping door bevelen een rij te vormen toe terwijl het Web SDK asynchroon laadt. Zie [&#x200B; code van de Basis &#x200B;](base-code.md) voor meer informatie. Adobe raadt u aan de basiscode te gebruiken wanneer u de bibliotheek asynchroon laadt om rassenomstandigheden te voorkomen wanneer u de opdrachten van Web SDK aanroept tijdens het laden van de pagina.
* **de lader van de Bibliotheek**: Laadt de volledige bibliotheek van JavaScript.

Voeg het volgende codeblok zo hoog mogelijk toe in de tag `<head>` vóór alle scripts die de Web SDK kunnen aanroepen:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Als u het Web SDK synchroon wilt laden, kunt u het kenmerk `async` verwijderen bij het laden van de bibliotheek. Als u het kenmerk `async` verwijdert, wordt HTML niet geparseerd terwijl de browser de bibliotheek ophaalt en uitvoert. Deze extra vertraging voordat de primaire inhoud aan gebruikers wordt weergegeven, wordt doorgaans afgeraden, maar kan, afhankelijk van de behoeften van uw organisatie, zinvol zijn.
