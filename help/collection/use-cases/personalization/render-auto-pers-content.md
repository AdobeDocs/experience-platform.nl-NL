---
title: DOM-actievoorstellen automatisch renderen
description: Het Web SDK van het gebruik om erkende DOM actievoorstellen automatisch terug te geven en gemeenschappelijke SPA te behandelen herstelt scenario's.
keywords: personalisatie;renderDecisions;dom-action;sendEvent;applyProposities;single page application;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# DOM-actievoorstellen automatisch renderen

Gebruik dit patroon wanneer uw verpersoonlijkingsreactie propositie-items met het schema omvat:

**`https://ns.adobe.com/personalization/dom-action`**

Deze items bevatten doorgaans een kiezer en een handelingstype (bijvoorbeeld `setHtml` ) dat de Web SDK automatisch kan toepassen wanneer `renderDecisions` is ingeschakeld.

## &#x200B;1. flikkering beheren (optioneel)

Als u flikkering moet voorkomen terwijl gepersonaliseerde inhoud wordt toegepast, gebruikt u de aanbevolen aanpak voor flikkerbeheer voor uw implementatie. Zie [ flikkering ](manage-flicker.md) voor beschikbare opties beheren.

## &#x200B;2. Beslissingen aanvragen en weergeven voor automatische rendering

Stel `renderDecisions` in op `true` wanneer u de opdracht `sendEvent` aanroept. De eigenschap `renderDecisions` wordt standaard ingesteld op false wanneer deze wordt weggelaten.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Als u specifieke plaatsingen wilt aanvragen, neemt u desgewenst `personalization.decisionScopes` op:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Zie het object [`personalization`](/help/collection/js/commands/sendevent/personalization.md) in de opdracht [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) voor meer informatie.

## &#x200B;3. Weergavegebeurtenissen

Als u `renderDecisions` op `true` instelt en `personalization.sendDisplayEvent` op `true` instelt of weglaat, verzendt de Web SDK onmiddellijk weergavegebeurtenissen nadat de personalisatie is gerenderd.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Zie [ vertoningsgebeurtenissen ](display-events.md) voor afwisselende opties beheren die aan de behoeften van uw implementatie voldoen, zoals wanneer het gebruiken van [ Hoogste en onderste paginagebeurtenissen ](top-bottom-page-events.md).

## &#x200B;4. Wijzigingen in de SPA-weergave en renderen

Neem voor toepassingen van één pagina een `viewName` op voor gebeurtenissen die worden weergegeven en gewijzigd.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Als uw KUUROORD UI voor de zelfde mening zonder een nieuw besluit teruggeeft haalt, kunt u eerder teruggekeerde voorstellingen opnieuw toepassen:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Zie [`applyPropositions`](/help/collection/js/commands/applypropositions.md) voor meer informatie.

>[!NOTE]
>
>De opdracht `applyPropositions` verzendt niet automatisch weergavegebeurtenissen. Als u &quot;vertoning&quot;voor re-geef scenario&#39;s moet registreren, zie [ weergavegebeurtenissen ](display-events.md) beheren.
