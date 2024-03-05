---
title: applyResponse
description: Gebruik een reactie van het Netwerk van de Rand om het Web SDK te initialiseren.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# `applyResponse`

De `applyResponse` staat u toe om diverse acties uit te voeren die op een reactie van het Netwerk van de Rand worden gebaseerd. Het wordt typisch gebruikt in hybride plaatsingen waar de server een eerste vraag aan het Netwerk van de Rand doet. Dit bevel neemt de reactie van die vraag en initialiseert het Web SDK in browser.

## Reactie toepassen met de web SDK-tagextensie

Het toepassen van reacties wordt uitgevoerd als een actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
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
* **`responseBody`**: Vereist. Een JSON-antwoordinstantie van de serveraanroep naar het Edge-netwerk.
* **`personalization.sendDisplayEvent`**: Een Booleaanse waarde die identiek is aan [`personalization.sendDisplayEvent`](sendevent/personalization.md) in de `sendEvent` gebruiken.

```js
allow("applyResponse",{
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

* **`propositions`**: Een array met voorstellingen die door het Edge-netwerk worden geretourneerd. Voorstellen die automatisch worden gerenderd, omvatten de markering `renderAttempted` instellen op `true`.
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: Een array met doelobjecten die door het Edge-netwerk worden geretourneerd.
