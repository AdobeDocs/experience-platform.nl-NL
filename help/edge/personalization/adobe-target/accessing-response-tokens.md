---
title: Toegang krijgen tot respontokens met de Adobe Experience Platform Web SDK
description: Leer hoe te om tot reactietokens met het Web SDK van Adobe Experience Platform toegang te hebben.
keywords: personalisatie;target;adobe target;renderDecisions;sendEvent;decisionsScopes;result.decisions,response tokens;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Toegang krijgen tot reactietokens

Tot de personalisatie-inhoud die door Adobe Target wordt geretourneerd, behoren [reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het gebruikersinterface van Adobe Target worden gevormd.

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, verstrek een callback functie wanneer het verzenden van een gebeurtenis. Deze callback zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. Uw callback wordt verstrekt a `result` object, dat een `propositions` eigenschap met geretourneerde personalisatie-inhoud. Hieronder ziet u een voorbeeld van een callback-functie.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In dit voorbeeld: `result.propositions`, als deze bestaat, is een array met personalisatievoorstellen die betrekking hebben op de gebeurtenis. Zie [Renderen van personalisatie-inhoud](../rendering-personalization-content.md) voor meer informatie over de inhoud van `result.propositions`.

Veronderstel u alle activiteitennamen van alle voorstellen wilt verzamelen die automatisch door het Web SDK werden teruggegeven en hen duwen in één enkele serie. Vervolgens kunt u de ene array naar een derde verzenden. In dit geval:

1. Proposities verwijderen uit de `result` object.
1. Doorloop elk voorstel.
1. Bepaal of de SDK het voorstel heeft weergegeven.
1. Als zo, lijn door elk punt in het voorstel.
1. De naam van de activiteit ophalen uit het dialoogvenster `meta` eigenschap, dat een object is dat responstokens bevat.
1. Zet de naam van de activiteit in een array.
1. Verzend de namen van de activiteiten naar een derde.

Uw code ziet er als volgt uit:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
