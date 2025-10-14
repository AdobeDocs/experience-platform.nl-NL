---
title: sendEvent
description: Gegevens verzenden naar de Adobe Experience Platform-Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# `sendEvent`

De opdracht `sendEvent` is de primaire manier om gegevens naar Adobe te verzenden, om gepersonaliseerde inhoud, identiteiten en publieksdoelen op te halen. Met het [`xdm`](xdm.md) -object kunt u gegevens verzenden die zijn toegewezen aan uw Adobe Experience Platform-schema. Gebruik het [`data`](data.md) -object om niet-XDM-gegevens te verzenden. Met de datastroommapper kunt u gegevens binnen dit object uitlijnen op schemavelden.

## Gebeurtenisgegevens verzenden met de webSDK-tagextensie

Het verzenden van gebeurtenisgegevens wordt uitgevoerd als een handeling binnen een regel in de interface met Adobe Experience Platform-tags voor gegevensverzameling.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Stel de gewenste velden in, klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Gebeurtenisgegevens verzenden met de Web SDK JavaScript-bibliotheek

Voer het `sendEvent` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Roep de opdracht [`configure`](../configure/overview.md) aan voordat u de opdracht `sendEvent` aanroept.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Object Response

Als u besluit om [&#x200B; reacties &#x200B;](../command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`propositions`**: Een array met voorstellingen die door de Edge Network worden geretourneerd. Voorwaarden die automatisch worden gerenderd, zijn onder andere de markering `renderAttempted` ingesteld op `true` .
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: een array met doelobjecten die door de Edge Network worden geretourneerd.
