---
title: applyProposities
description: Rendervoorstellingen die al met sendEvent zijn gerenderd.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# `applyPropositions`

Met de opdracht `applyPropositions` kunt u opnieuw voorstellingen renderen die al zijn gerenderd met de opdracht [`sendEvent`](sendevent/overview.md) . Deze opdracht is handig wanneer u werkt met toepassingen van één pagina waarin delen van de pagina opnieuw worden weergegeven en waarmee u eventuele al op de pagina toegepaste aanpassingen kunt overschrijven.

Deze opdracht ondersteunt de volgende velden:

* **Voorstellen**: Een serie van propositievoorwerpen die u wilt re-teruggeven.
* **naam van de Mening**: De naam van de mening om terug te geven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen via de optie `sendEvent` in een volgende opdracht van `personalization.includeRenderedPropositions` worden opgenomen.
* **gegevens van Meta**: Een voorwerp dat bepaalt hoe de aanbiedingen van HTML kunnen worden toegepast. Het bevat de volgende eigenschappen:
   * Bereik
   * Kiezer
   * Type handeling

>[!NOTE]
>
>De opdracht `applyPropositions` verzendt niet automatisch weergavegebeurtenissen. Als de opnamevertoningen gewenst zijn, gebruik het `sendEvent` bevel zoals die in [&#x200B; wordt beschreven leidt vertoningsgebeurtenissen &#x200B;](/help/collection/use-cases/personalization/display-events.md).

Voer het `applyPropositions` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`propositions`**: Een array van propositieobjecten die u opnieuw wilt renderen. Dit object wordt meestal niet gebruikt, omdat het veld `propositionScopes` meestal bepaalt welk bereik of welke oppervlakken u opnieuw wilt renderen.
* **`metadata`** - Hiermee bepaalt u hoe HTML-aanbiedingen worden toegepast. Het is een kaart waar de sleutel een bereik of een oppervlak is en de waarde een object is dat de toetsen `selector` en `actionType` bevat.
   * `selector`: Een tekenreeks die een CSS-kiezer bevat waaruit de HTML moet worden toegepast.
   * `actionType`: De handeling die met de HTML moet worden uitgevoerd. Geldige waarden zijn `setHtml` , `replaceHtml` en `appendHtml` .
* **`viewName`**: De naam van de weergave die in een toepassing van één pagina moet worden weergegeven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen met `sendEvent` worden opgenomen in een volgende `personalization.includeRenderedPropositions` -opdracht.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Proposities toepassen met de Web SDK-tagextensie

De Web SDK-tagextensie die equivalent is aan deze opdracht, is de [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) -handeling.
