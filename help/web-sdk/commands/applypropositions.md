---
title: applyProposities
description: Rendervoorstellingen die al met sendEvent zijn gerenderd.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# `applyPropositions`

De `applyPropositions` staat u toe om voorstellingen opnieuw terug te geven die reeds gebruikend werden teruggegeven [`sendEvent`](sendevent/overview.md) gebruiken. Deze opdracht is handig wanneer u werkt met toepassingen van één pagina waarin delen van de pagina opnieuw worden weergegeven en waarmee u eventuele al op de pagina toegepaste aanpassingen kunt overschrijven.

Deze opdracht ondersteunt de volgende velden:

* **Voorstellen**: Een array van propositieobjecten die u opnieuw wilt renderen.
* **Naam weergeven**: De naam van de weergave die moet worden weergegeven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen in een volgende `sendEvent` gebruiken `personalization.includePendingDisplayNotifications` -optie.
* **Metagegevens**: Een object dat bepaalt hoe HTML-aanbiedingen kunnen worden toegepast. Het bevat de volgende eigenschappen:
   * Bereik
   * Kiezer
   * Type handeling

## Proposities toepassen met de webSDK-tagextensie

Het toepassen van voorstellingen wordt uitgevoerd als een actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Apply propositions]**.
1. Stel de gewenste velden rechts in.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Proposities toepassen met de Web SDK JavaScript-bibliotheek

Voer de `applyPropositions` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`propositions`**: Een array van propositieobjecten die u opnieuw wilt renderen. Dit object wordt doorgaans niet gebruikt als de `propositionScopes` bepaalt meestal welk bereik of welke oppervlakken u opnieuw wilt renderen.
* **`metadata`**: Hiermee bepaalt u hoe HTML-aanbiedingen worden toegepast. Het is een kaart waar de sleutel een bereik of een oppervlak is en de waarde een object is dat de toetsen bevat `selector` en `actionType`.
   * `selector`: Een tekenreeks met een CSS-kiezer waaruit de HTML moet worden toegepast.
   * `actionType`: De actie die met de HTML moet worden ondernomen. Geldige waarden zijn `setHtml`, `replaceHtml`, en `appendHtml`.
* **`viewName`**: De naam van de weergave die in een toepassing van één pagina moet worden weergegeven. De weergavemeldingen voor deze beslissingen worden in het cachegeheugen opgeslagen en kunnen in een volgende `sendEvent` gebruiken `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
