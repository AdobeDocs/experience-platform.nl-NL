---
title: Flicker beheren voor persoonlijke ervaringen met de SDK van Adobe Experience Platform Web
description: Leer hoe u de SDK van Adobe Experience Platform Web kunt gebruiken om flikkering op gebruikerservaring te beheren.
keywords: target;flicker;prehideStyle;asynchroon;asynchroon;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# flikkering beheren

Wanneer de SDK probeert om personalisatie-inhoud te renderen, moet deze ervoor zorgen dat er geen flikkering optreedt. De flikkering, ook FOOC genoemd (Flash van Originele Inhoud), is wanneer een originele inhoud kort wordt getoond alvorens het alternatief tijdens het testen/verpersoonlijken verschijnt. De SDK probeert CSS-stijlen toe te passen op elementen van de pagina om ervoor te zorgen dat deze elementen worden verborgen totdat de personalisatie-inhoud is gerenderd.

De functie voor flikkerbeheer heeft een aantal fasen:

1. Voorverbergen
1. Voorbewerken
1. Renderen

## Voorverbergen

Tijdens de voorbereidingsfase gebruikt de SDK de configuratieoptie `prehidingStyle` om een HTML-stijltag te maken en deze aan de DOM toe te voegen om ervoor te zorgen dat grote delen van de pagina worden verborgen. Als u niet zeker weet welke delen van de pagina worden aangepast, kunt u `prehidingStyle` het beste instellen op `body { opacity: 0 !important }`. Zo weet u zeker dat de hele pagina verborgen is. Dit heeft echter het nadeel van het leiden tot slechtere weergaveprestaties voor pagina&#39;s die worden gemeld door gereedschappen zoals Lighthouse, Webpaginatests, enzovoort. Als u de beste weergaveprestaties op de pagina wilt hebben, kunt u `prehidingStyle` het beste instellen op een lijst met containerelementen die de delen van de pagina bevatten die worden aangepast.

Ervan uitgaande dat u een HTML-pagina hebt zoals de onderstaande pagina en dat alleen `bar`- en `bazz`-containerelementen ooit zullen worden aangepast:

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

Dan `prehidingStyle` zou aan iets als `#bar, #bazz { opacity: 0 !important }` moeten worden geplaatst.

## Voorbewerken

De voorbereidingsfase tikt in zodra de SDK de gepersonaliseerde inhoud van de server heeft ontvangen. Tijdens deze fase, wordt de reactie vooraf verwerkt, ervoor zorgend dat de elementen die gepersonaliseerde inhoud moeten bevatten worden verborgen. Nadat deze elementen zijn verborgen, wordt de HTML-stijltag die is gemaakt op basis van de configuratieoptie `prehidingStyle` verwijderd en wordt de HTML-hoofdtekst of de verborgen containerelementen weergegeven.

## Renderen

Nadat alle verpersoonlijkingsinhoud met succes is teruggegeven, of als er om het even welke fout was, worden alle eerder verborgen elementen getoond om ervoor te zorgen dat er geen verborgen elementen op de pagina zijn die door SDK werden verborgen.

## Flicker beheren wanneer SDK asynchroon wordt geladen

U wordt aangeraden de SDK altijd asynchroon te laden voor de beste weergaveprestaties van de pagina. Dit heeft echter enkele gevolgen voor de weergave van gepersonaliseerde inhoud. Wanneer de SDK asynchroon wordt geladen, is het vereist om het voorverborgen fragment te gebruiken. Het voorbeeldfragment moet worden toegevoegd vóór de SDK in de HTML-pagina. Hier volgt een voorbeeldfragment dat het gehele lichaam verbergt:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Om ervoor te zorgen dat de HTML-hoofdtekst of de containerelementen gedurende langere tijd niet worden verborgen, gebruikt het voorverborgen fragment een timer die het fragment standaard na `3000` milliseconden verwijdert. De `3000` milliseconden is de maximumwachttijd. Als de reactie van de server eerder is ontvangen en verwerkt, wordt de voorverborgen HTML-stijltag zo snel mogelijk verwijderd.
