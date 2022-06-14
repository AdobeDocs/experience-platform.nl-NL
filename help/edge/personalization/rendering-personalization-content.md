---
title: Persoonlijke inhoud renderen met de SDK van het Adobe Experience Platform-web
description: Leer hoe u persoonlijke inhoud kunt renderen met de SDK van Adobe Experience Platform Web.
keywords: personalisatie;renderDecisions;sendEvent;DecisionScopes;proposities;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 0d8e19d8428191cc0c6c56e629e8c5528a96115c
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Aangepaste inhoud renderen

Adobe Experience Platform Web SDK steunt het terugwinnen van gepersonaliseerde inhoud van de oplossingen van de verpersoonlijking van Adobe, met inbegrip van [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) en [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=nl).

Bovendien, de bevoegdheden van SDK van het Web zelfde-pagina en volgende-pagina verpersoonlijkingsmogelijkheden door de verpersoonlijkingsbestemmingen van Adobe Experience Platform, zoals [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) en de [aangepaste verpersoonlijkingsverbinding](../../destinations/catalog/personalization/custom-personalization.md). Om te leren hoe te om Experience Platform voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen, zie [speciale gids](../../destinations/ui/configure-personalization-destinations.md).

Inhoud die is gemaakt in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kan automatisch worden opgehaald en gerenderd door de SDK. Inhoud die is gemaakt in Adobe Target [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) of Offer decisioning kan niet automatisch worden gerenderd door de SDK. In plaats daarvan moet u deze inhoud aanvragen met de SDK en de inhoud vervolgens zelf handmatig renderen.

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

## Profielen renderen in toepassingen van één pagina zonder metrische gegevens te verhogen {#applypropositions}

De `applyPropositions` met de opdracht kunt u een array met voorstellingen renderen of uitvoeren vanuit [!DNL Target] in toepassingen van één pagina, zonder het verhogen van [!DNL Analytics] en [!DNL Target] metriek. Hierdoor wordt de rapportnauwkeurigheid vergroot.

>[!IMPORTANT]
>
>Indien voorstellen voor de `__view__` bereik is weergegeven bij laden van pagina, hun `renderAttempted` markering wordt ingesteld op `true`. De `applyPropositions` de opdracht wordt niet opnieuw gerenderd `__view__` bereikvoorstellingen die de `renderAttempted: true` markering.

### Hoofdlettergebruik 1: Weergavevoorstellingen van één pagina opnieuw renderen

Het gebruiksgeval dat in het onderstaande voorbeeld wordt beschreven, rendert de eerder opgehaalde en weergegeven voorstellingen van de kartonweergave opnieuw zonder weergavemeldingen te verzenden.

In het onderstaande voorbeeld wordt `sendEvent` wordt getriggerd op een wijziging in de weergave en wordt het resulterende object in een constante opgeslagen.

Wanneer vervolgens de weergave of een component wordt bijgewerkt, wordt de `applyPropositions` wordt aangeroepen, met de voorstellen van het vorige `sendEvent` om de weergavevoorstellingen opnieuw te renderen.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
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
    propositions: cartPropositions
});
```

### Hoofdlettergebruik 2: Proposities renderen die geen kiezer hebben

Dit gebruiksgeval is van toepassing op activiteitenaanbiedingen die zijn gemaakt met de [!DNL Target Form-based Experience Composer].

U moet de kiezer, de handeling en het bereik opgeven in het dialoogvenster `applyPropositions` vraag.

Ondersteund `actionTypes` zijn:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

Als u geen meta-gegevens voor een beslissingswerkingsgebied verstrekt, zullen de bijbehorende voorstellen niet worden teruggegeven.