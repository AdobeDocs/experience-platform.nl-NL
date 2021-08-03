---
title: Persoonlijke inhoud renderen met de SDK van het Adobe Experience Platform-web
description: Leer hoe u persoonlijke inhoud kunt renderen met de SDK van Adobe Experience Platform Web.
keywords: personalisatie;renderDecisions;sendEvent;DecisionScopes;proposities;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Aangepaste inhoud renderen

Adobe Experience Platform Web SDK ondersteunt het ophalen van gepersonaliseerde inhoud van personalisatieoplossingen op Adobe, inclusief [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) en [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=nl). Inhoud die is gemaakt in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kan automatisch worden opgehaald en gerenderd door de SDK. Inhoud die is gemaakt in Adobe Target [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) of Offer decisioning kan niet automatisch worden gerenderd door de SDK. In plaats daarvan moet u deze inhoud aanvragen met de SDK en de inhoud vervolgens zelf handmatig renderen.

## Inhoud automatisch renderen

Wanneer u gebeurtenissen naar de server verzendt, kunt u de optie `renderDecisions` instellen op `true`. Hierdoor wordt de SDK gedwongen om alle gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering, automatisch te renderen.

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

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, kunt u een callback functie verstrekken, die zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. Uw callback wordt verstrekt een `result` voorwerp, dat een `propositions` bezit kan bevatten die om het even welke teruggekeerde verpersoonlijkingsinhoud bevatten. Hieronder ziet u hoe u een callback-functie kunt gebruiken bij het verzenden van een gebeurtenis.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In dit voorbeeld is `result.propositions`, als dit bestaat, een array met verpersoonlijkingsvoorstellingen die betrekking hebben op de gebeurtenis. Standaard worden alleen voorstellingen opgenomen die in aanmerking komen voor automatische rendering.

De `propositions`-array kan er ongeveer als volgt uitzien:

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
    "renderAttempted": false
  }
]
```

In het voorbeeld was de optie `renderDecisions` niet ingesteld op `true` toen de opdracht `sendEvent` werd uitgevoerd, zodat de SDK niet probeerde automatisch inhoud te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering. U hebt deze opgehaald om de inhoud handmatig te renderen als u dat wilt. Merk op dat elk propositievoorwerp zijn `renderAttempted` bezit heeft die aan `false` wordt geplaatst.

Als u in plaats daarvan de optie `renderDecisions` zou hebben ingesteld op `true` bij het verzenden van de gebeurtenis, zou de SDK hebben geprobeerd om eventuele profielen te renderen die in aanmerking komen voor automatische rendering (zoals eerder beschreven). Dientengevolge, zou elk van de propositievoorwerpen zijn `renderAttempted` bezit hebben die aan `true` wordt geplaatst. In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot dusver, hebben wij slechts verpersoonlijkingsinhoud besproken die voor automatische teruggeven (namelijk om het even welke inhoud die in Adobe Target Visual Experience Composer wordt gecreeerd) verkiest. Als u _geen_ wilt ophalen die geschikt zijn voor automatische rendering, moet u de inhoud opvragen door de optie `decisionScopes` te vullen wanneer u de gebeurtenis verzendt. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

Hier volgt een voorbeeld:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Als in dit voorbeeld proposities worden gevonden op de server die overeenkomt met het bereik `salutation` of `discount`, worden deze geretourneerd en opgenomen in de array `result.propositions`. Houd er rekening mee dat proposities die in aanmerking komen voor automatische rendering, ook in de toekomst in de `propositions`-array worden opgenomen, ongeacht hoe u de opties `renderDecisions` of `decisionScopes` configureert. De `propositions`-array zou er in dit geval ongeveer als volgt uitzien:

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
    "renderAttempted": false
  }
]
```

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld is het voorstel dat overeenkomt met het bereik `discount` een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Ervan uitgaande dat u een element op uw pagina hebt met de id `daily-special` en de inhoud van het `discount`-voorstel wilt weergeven in het `daily-special`-element, gaat u als volgt te werk:

1. Extraheer voorstellingen uit het object `result`.
1. Lijn door elk voorstel, zoekend het voorstel met een werkingsgebied van `discount`.
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat HTML-inhoud is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u het element `daily-special` op de pagina en vervangt u de HTML van het item door de gepersonaliseerde inhoud.

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
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Als u Adobe Target gebruikt, komen bereiken overeen met de boxes op de server, behalve dat ze allemaal tegelijk worden aangevraagd in plaats van afzonderlijk. De algemene mbox wordt altijd geretourneerd.

### flikkering beheren

De SDK biedt voorzieningen om flikkering](../personalization/manage-flicker.md) tijdens het verpersoonlijkingsproces te beheren.[
