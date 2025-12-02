---
title: Aangepaste inhoud renderen met Adobe Experience Platform Web SDK
description: Leer hoe u persoonlijke inhoud kunt renderen met de Adobe Experience Platform Web SDK.
keywords: personalisatie;renderDecisions;sendEvent;DecisionScopes;proposities;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Aangepaste inhoud renderen

Adobe Experience Platform Web SDK steunt het terugwinnen van gepersonaliseerde inhoud van de verpersoonlijkingsoplossingen van Adobe, met inbegrip van [&#x200B; Adobe Target &#x200B;](https://business.adobe.com/nl/products/target/adobe-target.html), [&#x200B; Offer Decisioning &#x200B;](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=nl) en [&#x200B; Adobe Journey Optimizer &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=nl).

Bovendien, de bevoegdheden van SDK van het Web op dezelfde pagina en volgende-pagina verpersoonlijkingsmogelijkheden door de verpersoonlijkingsbestemmingen van Adobe Experience Platform, zoals [&#x200B; Adobe Target &#x200B;](/help/destinations/catalog/personalization/adobe-target-connection.md) en de [&#x200B; verbinding van de douaneverpersoonlijking &#x200B;](/help/destinations/catalog/personalization/custom-personalization.md). Leren hoe te om Experience Platform voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen, zie de [&#x200B; specifieke gids &#x200B;](/help/destinations/ui/activate-edge-personalization-destinations.md).

De inhoud die binnen Adobe Target [&#x200B; wordt gecreeerd Visuele Composer van de Ervaring &#x200B;](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=nl-NL) en de Campagne UI van het Web van Adobe Journey Optimizer [&#x200B; &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=nl-NL) kan automatisch worden teruggewonnen en door SDK worden teruggegeven. De inhoud die binnen Adobe Target [&#x200B; op vorm-gebaseerde Composer van de Ervaring &#x200B;](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=nl-NL) wordt gecreeerd, Adobe Journey Optimizer [&#x200B; op code-gebaseerd Kanaal van de Ervaring &#x200B;](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/code-based-experience/get-started-code-based) of Offer Decisioning kan niet automatisch door SDK worden teruggegeven. In plaats daarvan moet u deze inhoud aanvragen via de SDK en de inhoud vervolgens zelf handmatig renderen.

## Inhoud automatisch renderen {#automatic}

Wanneer u gebeurtenissen naar de server verzendt, kunt u de optie `renderDecisions` instellen op `true` . Hierdoor wordt de SDK gedwongen om automatisch gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering.

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

## Inhoud handmatig renderen {#manual}

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, kunt u een callback functie verstrekken, die zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. De callback is voorzien van een `result` -object dat een `propositions` -eigenschap kan bevatten met geretourneerde personalisatie-inhoud. Hieronder ziet u hoe u een callback-functie kunt gebruiken bij het verzenden van een gebeurtenis.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In dit voorbeeld is `result.propositions` , indien aanwezig, een array met verpersoonlijkingsvoorstellingen die betrekking hebben op de gebeurtenis. Standaard worden alleen voorstellingen opgenomen die in aanmerking komen voor automatische rendering.

De array `propositions` kan er ongeveer als volgt uitzien:

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

In het voorbeeld is de optie `renderDecisions` niet ingesteld op `true` wanneer de opdracht `sendEvent` werd uitgevoerd. De SDK heeft dus niet geprobeerd om inhoud automatisch te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering. U hebt deze inhoud als u dat wilt handmatig renderen. Voor elk propositieobject is de eigenschap `renderAttempted` ingesteld op `false` .

Als u in plaats daarvan de optie `renderDecisions` op `true` zou hebben ingesteld tijdens het verzenden van de gebeurtenis, zou de SDK hebben geprobeerd om alle profielen te renderen die in aanmerking komen voor automatische rendering (zoals eerder beschreven). Als gevolg hiervan zou de eigenschap `renderAttempted` van elk propositieobject zijn ingesteld op `true` . In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot dusver, hebben wij slechts verpersoonlijkingsinhoud besproken die voor automatische teruggeven (namelijk om het even welke inhoud die in de Composer van de Visual Experience van Adobe Target of de Campagne UI van het Web van Adobe Journey Optimizer wordt gecreeerd) verkiesbaar is. Om om het even welke verpersoonlijkingsinhoud _terug te winnen niet_ geschikt voor automatische teruggeven, moet u de inhoud verzoeken door de `decisionScopes` optie te bevolken wanneer het verzenden van de gebeurtenis. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

Hier volgt een voorbeeld:

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Als in dit voorbeeld proposities worden gevonden op de server die overeenkomt met het bereik `salutation` of `discount` , worden deze geretourneerd en opgenomen in de array `result.propositions` . Houd er rekening mee dat proposities die in aanmerking komen voor automatische rendering, ook in de toekomst in de array `propositions` worden opgenomen, ongeacht hoe u opties voor `renderDecisions` of `decisionScopes` configureert. De array `propositions` ziet er in dit geval ongeveer als volgt uit:

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

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld is het voorstel dat overeenkomt met het bereik van `discount` een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Ervan uitgaande dat u een element op uw pagina hebt met de id `daily-special` en dat u de inhoud van het `discount` proposition in het `daily-special` -element wilt renderen, gaat u als volgt te werk:

1. Extraheer voorstellen uit het `result` -object.
1. Doorloop elk voorstel en zoek het voorstel met een bereik van `discount` .
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat HTML-inhoud is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u het `daily-special` -element op de pagina en vervangt u de HTML door de gepersonaliseerde inhoud.
1. Nadat de inhoud is gerenderd, verzendt u een `display` -gebeurtenis.

Uw code ziet er als volgt uit:

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "display" event 
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Als u Adobe Target gebruikt, komen bereiken overeen met de boxes op de server, behalve dat ze allemaal tegelijk worden aangevraagd in plaats van afzonderlijk. De algemene mbox wordt altijd geretourneerd.

### flikkering beheren

SDK verstrekt faciliteiten om [&#x200B; flikkering &#x200B;](../personalization/manage-flicker.md) tijdens het verpersoonlijkingsproces te beheren.

## Profielen renderen in toepassingen van één pagina zonder metrische gegevens te verhogen {#applypropositions}

Met de opdracht `applyPropositions` kunt u een array met voorstellingen van [!DNL Target] of Adobe Journey Optimizer renderen of uitvoeren in toepassingen van één pagina, zonder de metriek [!DNL Analytics] en [!DNL Target] te verhogen. Dit verhoogt de nauwkeurigheid van de rapportage.

>[!IMPORTANT]
>
>Als proposities voor `__view__` scope (of een Web-oppervlakte) op paginading werden teruggegeven, zal hun `renderAttempted` vlag aan `true` worden geplaatst. Met de opdracht `applyPropositions` worden de `__view__` scope (of web surface)-voorstellingen die de `renderAttempted: true` -markering hebben, niet opnieuw gerenderd.

### Hoofdlettergebruik 1: toepassingenweergavevoorstellen van één pagina opnieuw renderen

Het gebruiksgeval dat in het onderstaande voorbeeld wordt beschreven, rendert de eerder opgehaalde en weergegeven voorstellingen van de kartonweergave opnieuw zonder weergavemeldingen te verzenden.

In het onderstaande voorbeeld wordt de opdracht `sendEvent` geactiveerd na een wijziging in de weergave en wordt het resulterende object in een constante opgeslagen.

Wanneer vervolgens de weergave of een component wordt bijgewerkt, wordt de opdracht `applyPropositions` aangeroepen, met de voorstellen van de vorige opdracht `sendEvent` , om de weergavevoorstellingen opnieuw te renderen.

```js
var cartPropositions = alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "web": {
      "webPageDetails": {
        "viewName": "cart"
      }
    }
  }
}).then(function(result) {
  var propositions = result.propositions;

  // Collect response tokens, etc.
  return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
  "propositions": cartPropositions
});
```

### Hoofdlettergebruik 2: voorvertoningen renderen die geen kiezer hebben

Dit gebruiksgeval is op ervaringen van toepassing die gebruikend [!DNL Target Form-based Experience Composer] of Adobe Journey Optimizer [&#x200B; op code-Gebaseerd Kanaal van de Ervaring &#x200B;](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/code-based-experience/get-started-code-based) worden geschreven.

U moet de kiezer, de handeling en het bereik opgeven in de aanroep van `applyPropositions` .

Ondersteunde `actionTypes` zijn:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
  "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
  // Render propositions on the page by providing additional metadata

  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      "salutation": {
        "selector": "#first-form-based-offer",
        "actionType": "setHtml"
      },
      "discount": {
        "selector": "#second-form-based-offer",
        "actionType": "replaceHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    function sendDisplayEvent(proposition) {
      const {
        id,
        scope,
        scopeDetails = {}
      } = proposition;

      alloy("sendEvent", {
        "xdm": {
          "eventType": "decisioning.propositionDisplay",
          "_experience": {
            "decisioning": {
              "propositions": [{
                "id": id,
                "scope": scope,
                "scopeDetails": scopeDetails
              }],
              "propositionEventType": {
                "display": 1
              }
            }
          }
        }
      });
    }
  });
});
```

Als u geen meta-gegevens voor een beslissingswerkingsgebied verstrekt, zullen de bijbehorende voorstellen niet worden teruggegeven.
