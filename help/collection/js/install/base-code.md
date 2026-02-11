---
title: Basiscode
description: De bevelen van de rij (laarzentrekker) terwijl de bibliotheek van de gegevensinzameling asynchroon laadt.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Basiscode

De basiscode laat bootstrapping toe door bevelen een rij te vormen terwijl het Web SDK van Adobe Experience Platform asynchroon laadt. Nadat de basiscode is uitgevoerd, kunt u elke opdracht zoals [`configure`](../commands/configure/overview.md) of [`sendEvent`](../commands/sendevent/overview.md) direct aanroepen zonder dat u zich zorgen hoeft te maken over de raycondities of de timing van de bibliotheek wanneer deze klaar is met laden. Wanneer het Web SDK klaar is met laden, voeren een rij gevormde bevelen in een eerste-binnen, uit orde uit (de zelfde orde dat zij een rij werden gevormd).

Opdrachten retourneren Promises, zelfs wanneer een wachtrij wordt geplaatst. Als een bevel een rij wordt gevormd, lost het Beleggen of verwerpt na het bevellooppas wanneer het Web SDK klaar is met laden. Als de Web SDK nooit klaar is met laden (de bibliotheek kan bijvoorbeeld niet worden geladen), blijven Promises in de wachtrij staan.

## Basiscode toevoegen

Plaats de basiscode zo hoog mogelijk in de `<head>` -tag, vóór alle scripts die de Web SDK kunnen aanroepen.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Na het toevoegen van de basiscode, laad SDK van het Web gebruikend uw gekozen methode ([ de bibliotheeklader van JavaScript ](library.md) of [ Markeringen bedden code ](/help/tags/extensions/client/web-sdk/getting-started.md) in). Voor op tag-gebaseerde implementaties, wordt de basiscode gesteund in de de markeringsuitbreiding van SDK van het Web 2.34.0 en later.

Deze basiscode wordt **niet** vereist in de volgende scenario&#39;s:

* Als u de JavaScript-bibliotheek synchroon laadt. Synchrone laadblokken die parseren terwijl de bibliotheek wordt opgehaald en uitgevoerd.
* Als het gebruiken van de markeringsuitbreiding, worden alle vraag aan het Web SDK gemaakt binnen markeringsregels of acties. U hoeft alleen de basiscode op te nemen als uw implementatie verwijst naar de Web SDK buiten uw tagbibliotheek. De meeste markeringsimplementaties roepen typisch niet het Web SDK buiten de markeringsbibliotheek, zodat vereisen de meeste markeringsimplementaties niet de basiscode.

## Voorbeelden

Zie de commentaren binnen dit codevoorbeeld om de timing van te begrijpen hoe de bevelen een rij worden gevormd en worden opgelost. Dit voorbeeld is van toepassing op zowel de JavaScript-bibliotheek als de tagextensie:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Naam SDK-instantie wijzigen

U kunt de naam wijzigen van de algemene functie die u aanroept door de laatste regel van de basiscode te wijzigen. Wijzigen:

```js
(window,["alloy"]);
```

Aan:

```js
(window,["ingot"]);
```

Door deze wijziging kunt u opdrachten aanroepen met `ingot` in plaats van `alloy` :

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Meerdere SDK-instanties

U kunt optioneel de basiscode gebruiken om meerdere SDK-instanties op een pagina te configureren. Zie [ de veelvoudige instanties van SDK van het Web van het Gebruik ](../../use-cases/multiple-instances.md) voor meer informatie.
