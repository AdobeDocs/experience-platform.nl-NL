---
title: Persoonlijke inhoud renderen met de SDK van het Adobe Experience Platform-web
description: Leer hoe u persoonlijke inhoud kunt renderen met de SDK van Adobe Experience Platform Web.
keywords: personalisatie;renderDecisions;sendEvent;DecisionScopes;proposities;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5d4214c1f9dc8476dd946559f602591c6e929cb1
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# Aangepaste inhoud renderen

Adobe Experience Platform Web SDK steunt het terugwinnen van gepersonaliseerde inhoud van verpersoonlijkingsoplossingen bij Adobe, met inbegrip van [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) en [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=nl). Inhoud die is gemaakt in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kan automatisch worden opgehaald en gerenderd door de SDK. Inhoud die is gemaakt in Adobe Target [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) of Offer decisioning kan niet automatisch worden gerenderd door de SDK. In plaats daarvan moet u deze inhoud aanvragen met de SDK en de inhoud vervolgens zelf handmatig renderen.

## Inhoud automatisch renderen

Wanneer u gebeurtenissen naar de server verzendt, kunt u `renderDecisions` optie voor `true`. Hierdoor wordt de SDK gedwongen om alle gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering, automatisch te renderen.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
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

Het renderen van gepersonaliseerde inhoud is asynchroon, dus u zou geen veronderstellingen moeten maken met betrekking tot wanneer een bepaald stuk van inhoud het teruggeven zal hebben voltooid.

## Inhoud handmatig renderen

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, kunt u een callback functie verstrekken, die zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. Uw callback wordt verstrekt a `result` object, dat een `propositions` eigenschap met geretourneerde personalisatie-inhoud. Hieronder ziet u hoe u een callback-functie kunt gebruiken bij het verzenden van een gebeurtenis.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In dit voorbeeld: `result.propositions`, als deze bestaat, is een array met personalisatievoorstellen die betrekking hebben op de gebeurtenis. Standaard worden alleen voorstellingen opgenomen die in aanmerking komen voor automatische rendering.

De `propositions` array kan er ongeveer als volgt uitzien:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

In het voorbeeld wordt `renderDecisions` optie is niet ingesteld op `true` wanneer de `sendEvent` is uitgevoerd, zodat de SDK niet heeft geprobeerd om inhoud automatisch te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering. U hebt deze opgehaald om de inhoud handmatig te renderen als u dat wilt. Merk op dat elk projectobject zijn `renderAttempted` eigenschap ingesteld op `false`.

Als u in plaats daarvan de opdracht `renderDecisions` optie voor `true` bij het verzenden van de gebeurtenis zou de SDK hebben geprobeerd om alle voorstellingen die in aanmerking komen voor automatische rendering, te renderen (zoals eerder beschreven). Dientengevolge zou elk van de propositievoorwerpen zijn hebben `renderAttempted` eigenschap ingesteld op `true`. In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot dusver, hebben wij slechts verpersoonlijkingsinhoud besproken die voor automatische teruggeven (namelijk om het even welke inhoud die in Adobe Target Visual Experience Composer wordt gecreeerd) verkiest. Om het even welke verpersoonlijkingsinhoud terug te winnen _niet_ geschikt voor automatische rendering, moet u de inhoud opvragen door de `decisionScopes` wanneer u de gebeurtenis verzendt. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

Hier volgt een voorbeeld:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In dit voorbeeld, als de voorstellen op de server worden gevonden die overeenkomt met `salutation` of `discount` bereik, worden ze geretourneerd en opgenomen in de `result.propositions` array. Houd er rekening mee dat voorstellingen die in aanmerking komen voor automatische rendering, ook in de toekomst worden opgenomen in de `propositions` array, ongeacht hoe u configureert `renderDecisions` of `decisionScopes` opties. De `propositions` array, in dit geval, zou er hetzelfde uitzien als in dit voorbeeld:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld komt de voorgestelde toepassing overeen met de `discount` bereik is een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Ervan uitgaande dat u een element op uw pagina hebt met de id van `daily-special` en de inhoud van de `discount` voorstel in de `daily-special` -element, ga als volgt te werk:

1. Proposities verwijderen uit de `result` object.
1. Lijn door elk voorstel, zoekend het voorstel met een werkingsgebied van `discount`.
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat de inhoud van HTML is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u de `daily-special` -element op de pagina en vervang de HTML door de gepersonaliseerde inhoud.
1. Nadat de inhoud is gerenderd, verzendt u een `display` gebeurtenis.

Uw code ziet er als volgt uit:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Als u Adobe Target gebruikt, komen bereiken overeen met de boxes op de server, behalve dat ze allemaal tegelijk worden aangevraagd in plaats van afzonderlijk. De globale box wordt altijd geretourneerd.

### flikkering beheren

De SDK biedt faciliteiten aan [flikkering beheren](../personalization/manage-flicker.md) tijdens het verpersoonlijkingsproces.
