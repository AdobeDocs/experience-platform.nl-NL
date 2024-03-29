---
title: Flicker beheren voor persoonlijke ervaringen met de SDK van Adobe Experience Platform Web
description: Leer hoe u de SDK van Adobe Experience Platform Web kunt gebruiken om flikkering op gebruikerservaring te beheren.
keywords: target;flicker;prehideStyle;asynchroon;asynchroon;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# flikkering beheren

Wanneer de SDK probeert om personalisatie-inhoud te renderen, moet deze ervoor zorgen dat er geen flikkering optreedt. De flikkering, ook FOOC genoemd (Flash van Originele Inhoud), is wanneer een originele inhoud kort wordt getoond alvorens het alternatief tijdens het testen/verpersoonlijken verschijnt. De SDK probeert CSS-stijlen toe te passen op elementen van de pagina om ervoor te zorgen dat deze elementen worden verborgen totdat de personalisatie-inhoud is gerenderd.

Hoe u flikkering beheert, hangt af van of u SDK van het Web synchroon of asynchroon opstelt. Controleer de `<head>` tag waar u implementeert `alloy.js` of de tagloader. De aanwezigheid van de `async` in het dialoogvenster `<script>` -tag bepaalt of de Web SDK asynchroon wordt geladen.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Flikkering beheren voor synchrone implementaties

Synchroon flikkerbeheer bestaat uit drie fasen:

1. Voorverbergen
1. Voorbewerken
1. Renderen

Tijdens de **voorbedekfase**, gebruikt de SDK de [`prehidingStyle`](../commands/configure/prehidingstyle.md) configuratie-eigenschap om een HTML-stijltag te maken en deze toe te voegen aan de DOM om ervoor te zorgen dat de gewenste gedeelten van de pagina worden verborgen. Als u niet zeker weet welke delen van de pagina u wilt aanpassen, kunt u het beste `prehidingStyle` tot `body { opacity: 0 !important }`. Zo weet u zeker dat de hele pagina verborgen is. Dit heeft echter het nadeel van het leiden tot slechtere weergaveprestaties voor pagina&#39;s die worden gemeld door gereedschappen zoals Lighthouse, Webpaginatests, enzovoort. Voor de beste renderingprestaties van de pagina wordt aangeraden `prehidingStyle` aan een lijst van containerelementen die de delen van de pagina bevatten die zullen worden gepersonaliseerd.

Ervan uitgaande dat u een HTML-pagina hebt, zoals hieronder, en u weet dat alleen `bar` en `bazz` containerelementen zullen ooit worden gepersonaliseerd :

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Vervolgens worden de `prehidingStyle` moet worden ingesteld op iets als `#bar, #bazz { opacity: 0 !important }`.

Zodra de SDK gepersonaliseerde inhoud van de server heeft ontvangen, **voorbewerkingsfase** start. Tijdens deze fase, wordt de reactie vooraf verwerkt, ervoor zorgend dat de elementen die gepersonaliseerde inhoud moeten bevatten worden verborgen. Nadat deze elementen zijn verborgen, wordt de stijltag HTML gemaakt op basis van de `prehidingStyle` De configuratieoptie wordt verwijderd en de hoofdtekst van de HTML of de verborgen containerelementen worden weergegeven.

Nadat alle verpersoonlijkingsinhoud met succes is teruggegeven, of als er een fout was, **renderingfase** start. Alle eerder verborgen elementen worden weergegeven om er zeker van te zijn dat er geen verborgen elementen op de pagina staan die door de SDK zijn verborgen.

## Flicker beheren voor asynchrone implementaties

U wordt aangeraden de SDK altijd asynchroon te laden voor de beste weergaveprestaties van de pagina. Dit heeft echter enkele gevolgen voor de weergave van gepersonaliseerde inhoud. Wanneer de SDK asynchroon wordt geladen, is het vereist om het voorverborgen fragment te gebruiken. Het voorbeeldfragment moet worden toegevoegd vóór de SDK op de pagina HTML. Hier volgt een voorbeeldfragment dat het gehele lichaam verbergt:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Om ervoor te zorgen dat de hoofdtekst van de HTML of de containerelementen niet gedurende langere tijd verborgen zijn, gebruikt het prehide fragment een timer die het fragment standaard verwijdert na `3000` milliseconden. De `3000` milliseconden is de maximale wachttijd. Als de reactie van de server eerder is ontvangen en verwerkt, wordt de voorverborgen HTML-stijltag zo snel mogelijk verwijderd.
