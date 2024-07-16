---
title: renderDecisions
description: Render gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 1%

---

# `renderDecisions`

Met de eigenschap `renderDecisions` kunt u de SDK van het web dwingen gepersonaliseerde inhoud te renderen die geschikt is voor automatische rendering.

## Aangepaste inhoud renderen met de Web SDK-tagextensie

Selecteer het selectievakje **[!UICONTROL Render visual personalization decisions]** binnen de handelingen van een labelregel.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Blader omlaag naar de sectie [!UICONTROL Personalization] en schakel vervolgens het selectievakje **[!UICONTROL Render visual personalization decisions]** in.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Aangepaste inhoud renderen met de Web SDK JavaScript-bibliotheek

Stel de Booleaanse waarde `renderDecisions` in wanneer u de opdracht `sendEvent` uitvoert. Als deze eigenschap wordt weggelaten, wordt deze standaard ingesteld op `false` . Stel deze eigenschap in op `true` als u gepersonaliseerde inhoud automatisch wilt renderen.

>[!IMPORTANT]
>
>De eigenschap `renderDecisions` is niet compatibel met de eigenschap [`documentUnloading`](documentunloading.md) . Stel beide eigenschappen niet tegelijkertijd in op `true` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
