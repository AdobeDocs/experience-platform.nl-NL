---
title: Weergavegebeurtenissen beheren in de Web SDK
description: Verklaart welke vertoningsgebeurtenissen zijn en hoe u hen in het Web SDK kunt gebruiken.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personalisatie;display gebeurtenissen;sendEvent;renderDecisions;applyProposities;proposities;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Weergavegebeurtenissen beheren in de Web SDK

De gebeurtenissen van de vertoning vertellen verpersoonlijking of analysediensten dat een specifiek stuk van gepersonaliseerde inhoud aan de gebruiker werd getoond. Het verzenden van vertoningsgebeurtenissen verbetert rapporteringsnauwkeurigheid door stroomafwaartse systemen te helpen tussen inhoud onderscheiden die **&#x200B; en inhoud werd gevraagd die &#x200B;** eigenlijk werd getoond.

## Weergavegebeurtenissen automatisch verzenden

Automatische weergavegebeurtenissen zijn doorgaans de eenvoudigste optie. Ze worden direct verzonden nadat Web SDK klaar is met het renderen van in aanmerking komende inhoud uit het `sendEvent` -antwoord, waardoor de rapportnauwkeurigheid kan worden verbeterd.

Als u weergavegebeurtenissen automatisch wilt verzenden, gebruikt u een `sendEvent` -aanroep die `renderDecisions` op `true` instelt en `personalization.sendDisplayEvent` op `true` instelt (of weglaat, aangezien `true` de standaardwaarde is):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Automatische weergavegebeurtenissen zijn afhankelijk van door SDK beheerde rendering. Als u inhoud handmatig rendert (inclusief door `applyPropositions` te gebruiken), moet u weergavegebeurtenissen expliciet verzenden met `sendEvent` .

## Weergavegebeurtenissen verzenden in volgende `sendEvent` oproepen

Het opnemen van weergavegebeurtenissen in een latere aanroep van `sendEvent` is handig als u extra laadgegevens voor de pagina wilt toevoegen die niet beschikbaar zijn wanneer u om personalisatie vraagt. Het wordt algemeen gebruikt wanneer het uitvoeren van [&#x200B; Hoogste en bodempaginagebeurtenissen &#x200B;](/help/collection/use-cases/personalization/top-bottom-page-events.md). Correct het uitvoeren van vertoningsgebeurtenissen op deze manier helpt kwesties met [&#x200B; Stuiteren tarief &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/bounce-rate) in Adobe Analytics vermijden.

1. Vraag bij de eerste `sendEvent` -aanroep (vaak boven aan de pagina) inhoud aan en geef deze weer, maar onderdruk automatische weergavegebeurtenissen door `renderDecisions` in te stellen op `true` en `personalization.sendDisplayEvent` op `false` :

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Later (vaak onder aan de pagina) roept u `sendEvent` aan met een XDM-lading die weergavegebeurtenissen bevat voor voorstellingen die sinds de vorige aanvraag zijn gerenderd door [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) in te stellen op `true` :

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Alleen automatisch gerenderde voorstellingen waarvoor de weergave was onderdrukt, worden opgenomen wanneer u `includeRenderedPropositions` gebruikt.

## Weergavegebeurtenissen verzenden voor handmatig gerenderde profielen

Als u inhoud zelf rendert (volledig handmatig renderen of met `applyPropositions` ), moet u weergavegebeurtenissen expliciet verzenden met de opdracht `sendEvent` . Roep `sendEvent` aan met een XDM-lading die de volgende eigenschappen bevat:

* `_experience.decisioning.propositions` met de gerenderde voorstellingen&#39; `id` , `scope` en `scopeDetails`
* `_experience.decisioning.propositionEventType.display` ingesteld op `1`

In de volgende twee voorbeelden wordt deze hulpfunctie gebruikt om de weergavegebeurtenis XDM payload te bouwen:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

In het volgende voorbeeld wordt handmatig renderen met weergavegebeurtenissen gebruikt:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

In het volgende voorbeeld wordt de opdracht `applyPropositions` gebruikt met weergavegebeurtenissen. `sendEvent`, `applyPropositions` en een ander `sendEvent` worden samen geketend:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Gemeenschappelijke fouten om te vermijden

* **verzend vertoningsgebeurtenissen alvorens terug te geven** eindigt: verzend vertoningsgebeurtenissen nadat auto-teruggeeft voltooit, nadat `applyPropositions`, of nadat uw hand het teruggeven logica voltooit.
* **verzendt vertoningsgebeurtenissen voor voorstellen die u** niet teruggaf: Slechts omvat voorstellen die eigenlijk aan de gebruiker werden getoond.
* **Vervallen`scopeDetails`**: neem `scopeDetails` op van het propositieobject wanneer u weergavegebeurtenissen verzendt.
