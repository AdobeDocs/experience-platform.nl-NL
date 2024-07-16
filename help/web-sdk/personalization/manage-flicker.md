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

Hoe u flikkering beheert, hangt af van of u SDK van het Web synchroon of asynchroon opstelt. Controleer de tag `<head>` op de plaats waar u `alloy.js` of de tagloader implementeert. De aanwezigheid van het kenmerk `async` in de tag `<script>` bepaalt of de SDK van het Web asynchroon wordt geladen.

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

Tijdens de **preHide fase**, gebruikt SDK het [`prehidingStyle`](../commands/configure/prehidingstyle.md) configuratiebezit om een de stijlmarkering van HTML tot stand te brengen en het aan DOM toe te voegen om ervoor te zorgen dat de gewenste secties van de pagina verborgen zijn. Als u niet zeker weet welke delen van de pagina u wilt aanpassen, kunt u het beste `prehidingStyle` op `body { opacity: 0 !important }` instellen. Zo weet u zeker dat de hele pagina verborgen is. Dit heeft echter het nadeel van het leiden tot slechtere weergaveprestaties voor pagina&#39;s die worden gemeld door gereedschappen zoals Lighthouse, Webpaginatests, enzovoort. Voor de beste weergaveprestaties van de pagina, is het raadzaam `prehidingStyle` in te stellen op een lijst met containerelementen die de delen van de pagina bevatten die worden aangepast.

Ervan uitgaande dat u een HTML-pagina hebt, zoals de pagina hieronder, en u weet dat alleen `bar` - en `bazz` -containerelementen ooit zullen worden aangepast:

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

Vervolgens moet de `prehidingStyle` worden ingesteld op iets als `#bar, #bazz { opacity: 0 !important }` .

Zodra SDK gepersonaliseerde inhoud van de server heeft ontvangen, begint de **preprocessing fase**. Tijdens deze fase, wordt de reactie vooraf verwerkt, ervoor zorgend dat de elementen die gepersonaliseerde inhoud moeten bevatten worden verborgen. Nadat deze elementen zijn verborgen, wordt de stijltag HTML die is gemaakt op basis van de configuratieoptie `prehidingStyle` verwijderd en worden de hoofdtekst van de HTML of de verborgen containerelementen weergegeven.

Nadat al verpersoonlijkingsinhoud met succes is teruggegeven, of als er om het even welke fout was, begint de **teruggevende fase**. Alle eerder verborgen elementen worden weergegeven om er zeker van te zijn dat er geen verborgen elementen op de pagina staan die door de SDK zijn verborgen.

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

Om ervoor te zorgen dat de hoofdtekst van de HTML of de containerelementen niet gedurende langere tijd verborgen zijn, gebruikt het voorverborgen fragment een timer die het fragment standaard na `3000` milliseconden verwijdert. De `3000` milliseconden is de maximale wachttijd. Als de reactie van de server eerder is ontvangen en verwerkt, wordt de voorverborgen HTML-stijltag zo snel mogelijk verwijderd.
