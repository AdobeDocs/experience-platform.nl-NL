---
title: HTML-aanbiedingen renderen zonder kiezers
description: Render HTML-propositieitems zonder kiezers door metagegevens op te geven voor applyProposities en vervolgens weergavegebeurtenissen op te nemen.
keywords: personalisatie;applyProposities;metadata;actionType;DecisionScopes;display gebeurtenissen;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# HTML-aanbiedingen renderen zonder kiezers

Gebruik dit patroon wanneer uw voorstellingen HTML-inhoud bevatten, maar u moet opgeven waar u deze wilt toepassen (kiezer) en hoe u deze wilt toepassen (handelingstype). U kunt dit doen door [`applyPropositions`](/help/collection/js/commands/applypropositions.md) aan te roepen met een `metadata` -object dat via bereik is vergrendeld. Ondersteunde `actionType` -waarden zijn `setHtml` , `replaceHtml` en `appendHtml` .

## &#x200B;1. flikkering beheren (optioneel)

Als u inhoud verbergt tijdens het renderen, bent u er verantwoordelijk voor dat de inhoud wordt weergegeven nadat het renderen is voltooid. Zie [ flikkering ](manage-flicker.md) voor meer informatie beheren.

## &#x200B;2. Vraag voorstellen aan voor het bereik dat u wilt renderen

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Zie [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md) voor meer informatie.

## &#x200B;3. Aanbiedingen renderen met `applyPropositions` metagegevens

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Registreer weergavegebeurtenissen voor gerenderde voorstellingen

Weergavegebeurtenissen worden niet automatisch verzonden wanneer `applyPropositions` wordt aangeroepen. Nadat het renderen is voltooid, gebruikt u een `sendEvent` -aanroep die verwijst naar de gerenderde voorstellingen:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Zie [ vertoningsgebeurtenissen ](display-events.md) voor meer informatie beheren.

>[!TIP]
>
>Als u [ Hoogste en bodempaginagebeurtenissen ](top-bottom-page-events.md) gebruikt, wordt deze &quot;verslagvertoning&quot;vraag algemeen uitgevoerd in de bodem `sendEvent` vraag.

## &#x200B;5. Opnieuw renderen

Als de implementatie later opnieuw moet worden gerenderd (bijvoorbeeld in toepassingen met één pagina), roept u `applyPropositions` nogmaals aan met dezelfde voorstellingen en metagegevens:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Als u een vertoningsgebeurtenis voor dat moet registreren re-geef terug, zie [ vertoningsgebeurtenissen ](display-events.md) leiden.
