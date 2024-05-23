---
title: applyResponse
description: Gebruik een reactie van de Edge Network om het Web SDK te initialiseren.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# `applyResponse`

De `applyResponse` staat u toe om diverse acties uit te voeren die op een reactie van de Edge Network worden gebaseerd. Het wordt typisch gebruikt in hybride plaatsingen waar de server een aanvankelijke vraag aan de Edge Network doet. Dit bevel neemt de reactie van die vraag en initialiseert het Web SDK in browser.

## Reactie toepassen met de web SDK-tagextensie

Het toepassen van reacties wordt uitgevoerd als een actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Navigeren naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Apply response]**.
1. Stel de gewenste velden rechts in.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Reactie toepassen met de Web SDK JavaScript-bibliotheek

Voer de `applyResponse` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`renderDecisions`**: Een Booleaanse waarde die de Web SDK dwingt om gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering. Identiek aan [`renderDecisions`](sendevent/renderdecisions.md) in de [`sendEvent`](sendevent/overview.md) gebruiken.
* **`responseHeaders`**: Een kaart met tekenreeksheader aan tekenreeksheader.
* **`responseBody`**: Vereist. Een JSON-antwoordinstantie van de serveraanroep naar de Edge Network.
* **`personalization.sendDisplayEvent`**: Een Booleaanse waarde die identiek is aan [`personalization.sendDisplayEvent`](sendevent/personalization.md) in de `sendEvent` gebruiken.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Object Response

Als u besluit [reacties verwerken](command-responses.md) met deze opdracht zijn de volgende eigenschappen beschikbaar in het reactieobject:

* **`propositions`**: Een array met voorstellingen die door de Edge Network worden geretourneerd. Voorstellen die automatisch worden gerenderd, omvatten de markering `renderAttempted` instellen op `true`.
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: Een array van doelobjecten die door de Edge Network worden geretourneerd.
