---
title: sendEvent
description: Gegevens verzenden naar het Adobe Experience Platform Edge Network.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# `sendEvent`

De `sendEvent` bevel is de primaire manier om gegevens naar Adobe te verzenden, om gepersonaliseerde inhoud, identiteiten, en publieksbestemmingen terug te winnen. Gebruik de [`xdm`](xdm.md) -object om gegevens te verzenden die zijn toegewezen aan uw Adobe Experience Platform-schema. Gebruik de [`data`](data.md) -object om niet-XDM-gegevens te verzenden. Met de datastroommapper kunt u gegevens binnen dit object uitlijnen op schemavelden.

## Gebeurtenisgegevens verzenden met de webSDK-tagextensie

Het verzenden van gebeurtenisgegevens wordt uitgevoerd als een handeling binnen een regel in de interface met Adobe Experience Platform-tags voor gegevensverzameling.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Stel de gewenste velden in en klik op **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Gebeurtenisgegevens verzenden met de Web SDK JavaScript-bibliotheek

Voer de `sendEvent` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. Zorg ervoor dat u de [`configure`](../configure/overview.md) bevel alvorens te roepen `sendEvent` gebruiken.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": true,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Object Response

Als u besluit [reacties verwerken](../command-responses.md) met deze opdracht zijn de volgende eigenschappen beschikbaar in het reactieobject:

* **`propositions`**: Een array met voorstellingen die door het Edge-netwerk worden geretourneerd. Voorstellen die automatisch worden gerenderd, omvatten de markering `renderAttempted` instellen op `true`.
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: Een array met doelobjecten die door het Edge-netwerk worden geretourneerd.
