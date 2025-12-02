---
title: applyResponse
description: Gebruik een reactie van Edge Network om het Web SDK te initialiseren.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

Met de opdracht `applyResponse` kunt u verschillende handelingen uitvoeren op basis van een reactie van de Edge Network. Het wordt typisch gebruikt in hybride plaatsingen waar de server een eerste vraag aan de Edge Network doet. Dit bevel neemt de reactie van die vraag en initialiseert het Web SDK in browser.

Voer het `applyResponse` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Het object met configuratieopties ondersteunt de volgende velden:

* **`renderDecisions`**: Een Booleaanse waarde die de Web SDK dwingt om gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering. Identiek aan [`renderDecisions`](sendevent/renderdecisions.md) in het [`sendEvent`](sendevent/overview.md) bevel.
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

Als u besluit om [&#x200B; reacties &#x200B;](command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`propositions`**: Een array met voorstellingen die door de Edge Network worden geretourneerd. Voorwaarden die automatisch worden gerenderd, zijn onder andere de markering `renderAttempted` ingesteld op `true` .
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: een array van doelobjecten die door de Edge Network worden geretourneerd.

## Reactie toepassen met de Web SDK-tagextensie

De Web SDK-tagextensie die equivalent is aan deze opdracht, is de [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) -handeling.
