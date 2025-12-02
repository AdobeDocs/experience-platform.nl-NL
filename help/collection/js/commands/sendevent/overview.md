---
title: sendEvent
description: Gegevens verzenden naar de Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

De opdracht `sendEvent` is de primaire manier om gegevens naar Adobe te verzenden. Zijn reactievoorwerp is de primaire manier om gepersonaliseerde inhoud, identiteiten, en publieksbestemmingen terug te winnen. Met het [`xdm`](xdm.md) -object kunt u gegevens verzenden die zijn toegewezen aan uw Adobe Experience Platform-schema. Gebruik het [`data`](data.md) -object om niet-XDM-gegevens te verzenden. De lading wanneer het verzenden van gegevens naar Adobe heeft een maximumgrens van 64 KB.

Voer het `sendEvent` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Roep de opdracht [`configure`](../configure/overview.md) aan voordat u de opdracht `sendEvent` aanroept.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Object Response

Als u besluit om [ reacties ](../command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`propositions`**: Een array met voorstellingen die door de Edge Network worden geretourneerd. Voorwaarden die automatisch worden gerenderd, zijn onder andere de markering `renderAttempted` ingesteld op `true` .
* **`inferences`**: Een array van gebeurtenisobjecten die informatie over deze gebruiker bevatten.
* **`destinations`**: een array van doelobjecten die door de Edge Network worden geretourneerd.

## Gebeurtenis verzenden met de Web SDK-tagextensie

Het equivalent van deze opdracht voor de SDK-tag Web is de [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) -handeling.
