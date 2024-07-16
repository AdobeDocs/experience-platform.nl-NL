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

Met de opdracht `applyResponse` kunt u verschillende handelingen uitvoeren op basis van een reactie van de Edge Network. Het wordt typisch gebruikt in hybride plaatsingen waar de server een aanvankelijke vraag aan de Edge Network doet. Dit bevel neemt de reactie van die vraag en initialiseert het Web SDK in browser.

## Reactie toepassen met de web SDK-tagextensie

Het toepassen van reacties wordt uitgevoerd als een actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Apply response]** .
1. Stel de gewenste velden rechts in.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Reactie toepassen met de Web SDK JavaScript-bibliotheek

Voer het `applyResponse` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`renderDecisions`**: Een Booleaanse waarde die de SDK van het web dwingt om gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering. Identiek aan [`renderDecisions`](sendevent/renderdecisions.md) in het [`sendEvent`](sendevent/overview.md) bevel.
* **`responseHeaders`**: Een kaart met namen van tekenreeksheaders naar waarden van tekenreeksheaders.
* **`responseBody`**: vereist. Een JSON-antwoordinstantie van de serveraanroep naar de Edge Network.
* **`personalization.sendDisplayEvent`**: Een Booleaanse waarde die op dezelfde manier werkt als [`personalization.sendDisplayEvent`](sendevent/personalization.md) in de opdracht `sendEvent` .

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

Als u besluit om [ reacties ](command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`propositions`**: Een array met voorstellingen die door de Edge Network worden geretourneerd. Voorwaarden die automatisch worden gerenderd, zijn onder andere de markering `renderAttempted` ingesteld op `true` .
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: een array met doelobjecten die door de Edge Network worden geretourneerd.
