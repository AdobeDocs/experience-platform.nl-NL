---
title: Proposities handmatig renderen
description: Render propositieinhoud met behulp van uw eigen UI-logica (HTML, JSON of aangepaste schema's) en neem vervolgens weergavegebeurtenissen op.
keywords: personalisatie;voorstellingen;handmatige rendering;sendEvent;decisions;display-gebeurtenissen;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Proposities handmatig renderen

Gebruik dit patroon wanneer u volledige controle nodig hebt over de manier waarop de proposition-items worden toegepast. U maakt bijvoorbeeld een complexe gebruikersinterface op basis van JSON-inhoud of u wilt aangepaste bedrijfsregels toepassen voordat u gaat renderen.

## &#x200B;1. Verzoek om voorstellen

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Zie het object [`personalization`](/help/collection/js/commands/sendevent/personalization.md) in de opdracht [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) voor meer informatie.

## &#x200B;2. Projectitems renderen (voorbeeld)

Wanneer u handmatig voorstellingen rendert, kunnen ze vele verschillende vormen of vormen aannemen. Het volgende is een minimaal voorbeeld dat een voorstel door werkingsgebied vindt, dan past het eerste HTML inhoudspunt toe dat het vindt.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Als u HTML rendert, moet u ervoor zorgen dat deze veilig is voor uw omgeving. Inhoud renderen behandelen als een beveiligingsgrens (ontsmetten, vertrouwde bronnen en CSP-overwegingen).

## &#x200B;3. Neem weergavegebeurtenissen op voor wat u hebt gerenderd

Voor handmatig gerenderde voorstellingen worden weergavegebeurtenissen vastgelegd via `sendEvent` -aanroepen die verwijzen naar de gerenderde voorstellingen.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Zie [ vertoningsgebeurtenissen ](display-events.md) voor meer informatie beheren.

## &#x200B;4. Herrendering

Wanneer wijzigingen in de gebruikersinterface opnieuw moeten worden gerenderd, voert u de handmatige renderinglogica opnieuw uit tegen de propositiegegevens die u in de cache hebt opgeslagen (of haalt u indien nodig nogmaals op). Als u een vertoning voor re-rendert scenario&#39;s moet registreren, zie [ vertoningsgebeurtenissen ](display-events.md) leiden.
