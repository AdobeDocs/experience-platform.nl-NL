---
title: applyProposities
description: Rendervoorstellingen die al met sendEvent zijn gerenderd.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# `applyPropositions`

Met de opdracht `applyPropositions` kunt u opnieuw voorstellingen renderen die al zijn gerenderd met de opdracht [`sendEvent`](sendevent/overview.md) . Deze opdracht is handig wanneer u werkt met toepassingen van één pagina waarin delen van de pagina opnieuw worden weergegeven en waarmee u eventuele al op de pagina toegepaste aanpassingen kunt overschrijven.

Deze opdracht ondersteunt de volgende velden:

* **Voorstellen**: Een serie van propositievoorwerpen die u wilt re-teruggeven.
* **naam van de Mening**: De naam van de mening om terug te geven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen via de optie `personalization.includeRenderedPropositions` in een volgende opdracht van `sendEvent` worden opgenomen.
* **gegevens van Meta**: Een voorwerp dat bepaalt hoe de aanbiedingen van HTML kunnen worden toegepast. Het bevat de volgende eigenschappen:
   * Bereik
   * Kiezer
   * Type handeling

## Proposities toepassen met de webSDK-tagextensie

Het toepassen van voorstellingen wordt uitgevoerd als een actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Apply propositions]** .
1. Stel de gewenste velden rechts in.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Proposities toepassen met de Web SDK JavaScript-bibliotheek

Voer het `applyPropositions` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`propositions`**: Een array van propositieobjecten die u opnieuw wilt renderen. Dit object wordt meestal niet gebruikt, omdat het veld `propositionScopes` meestal bepaalt welk bereik of welke oppervlakken u opnieuw wilt renderen.
* **`metadata`** - Hiermee bepaalt u hoe HTML-aanbiedingen worden toegepast. Het is een kaart waar de sleutel een bereik of een oppervlak is en de waarde een object is dat de toetsen `selector` en `actionType` bevat.
   * `selector`: Een tekenreeks die een CSS-kiezer bevat waaruit de HTML moet worden toegepast.
   * `actionType`: De handeling die met de HTML moet worden uitgevoerd. Geldige waarden zijn `setHtml` , `replaceHtml` en `appendHtml` .
* **`viewName`**: De naam van de weergave die in een toepassing van één pagina moet worden weergegeven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen met `personalization.includeRenderedPropositions` worden opgenomen in een volgende `sendEvent` -opdracht.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
