---
title: Aangepaste inhoud renderen
seo-title: Adobe Experience Platform Web SDK Persoonlijke inhoud renderen
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Platform van de Ervaring terug te geven
seo-description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Platform van de Ervaring terug te geven
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bèta) Aangepaste inhoud renderen

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De SDK rendert automatisch gepersonaliseerde inhoud wanneer u een gebeurtenis naar de server verzendt en instelt `viewStart` op `true` als optie voor de gebeurtenis.

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Het renderen van gepersonaliseerde inhoud is asynchroon, dus er mag geen enkele veronderstelling bestaan wanneer een bepaald stuk inhoud deel uitmaakt van de pagina.

## Flikkering beheren

Wanneer de SDK probeert om personalisatie-inhoud te renderen, moet deze ervoor zorgen dat er geen flikkering optreedt. De flikkering, ook FOOC genoemd (Flits van Originele Inhoud), is wanneer een originele inhoud kort wordt getoond alvorens het alternatief tijdens het testen of verpersoonlijking verschijnt. De SDK probeert CSS-stijlen toe te passen op elementen van de pagina om ervoor te zorgen dat deze elementen worden verborgen totdat de personalisatie-inhoud is gerenderd.

De functie voor flikkerbeheer heeft een aantal fasen:

1. Voorverbergen
1. Voorbewerken
1. Renderen

### Voorverbergen

Tijdens de voorbereidingsfase gebruikt de SDK de `prehidingStyle` configuratieoptie om een HTML-stijltag te maken en deze toe te voegen aan de DOM om ervoor te zorgen dat grote delen van de pagina worden verborgen. Als u niet zeker weet welke delen van de pagina u wilt aanpassen, kunt u het beste instellen `prehidingStyle` op `body { opacity: 0 !important }`. Zo weet u zeker dat de hele pagina verborgen is. Dit heeft echter het nadeel van het leiden tot slechtere weergaveprestaties voor pagina&#39;s die worden gemeld door gereedschappen zoals Lighthouse, Webpaginatests, enzovoort. Voor de beste weergaveprestaties van de pagina wordt aangeraden een lijst met containerelementen in te stellen die de delen van de pagina bevatten die worden aangepast. `prehidingStyle`

Ervan uitgaande dat u een HTML-pagina hebt zoals de onderstaande, en u weet dat alleen `bar` en `bazz` containerelementen ooit zullen worden aangepast:

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

Dan `prehidingStyle` zou het aan iets als `#bar, #bazz { opacity: 0 !important }`moeten worden geplaatst.

### Voorbewerken

De voorbereidingsfase begint zodra SDK de gepersonaliseerde inhoud van de server heeft ontvangen. Tijdens deze fase, wordt de reactie vooraf verwerkt, ervoor zorgend dat de elementen die gepersonaliseerde inhoud moeten bevatten worden verborgen. Nadat deze elementen zijn verborgen, wordt de HTML-stijltag die is gemaakt op basis van de `prehidingStyle` configuratieoptie verwijderd en wordt de HTML-hoofdtekst of de verborgen containerelementen weergegeven.

### Renderen

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

Om ervoor te zorgen dat de HTML-hoofdtekst of de containerelementen gedurende langere tijd niet worden verborgen, gebruikt het voorverborgen fragment een timer die het fragment standaard na `3000` milliseconden verwijdert. De `3000` milliseconden is de maximale wachttijd. Als de reactie van de server eerder is ontvangen en verwerkt, wordt de voorverborgen HTML-stijltag zo snel mogelijk verwijderd.
