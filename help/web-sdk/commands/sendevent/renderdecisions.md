---
title: renderDecisions
description: Render gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# `renderDecisions`

De `renderDecisions` staat u toe om SDK van het Web te dwingen om het even welke gepersonaliseerde inhoud terug te geven die voor automatische het teruggeven verkiesbaar is.

## Aangepaste inhoud renderen met de Web SDK-tagextensie

Selecteer de **[!UICONTROL Render visual personalization decisions]** Schakel het selectievakje in binnen de handelingen van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Navigeren naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Omlaag schuiven naar de [!UICONTROL Personalization] en selecteert u vervolgens de **[!UICONTROL Render visual personalization decisions]** selectievakje.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Persoonlijke inhoud renderen met de Web SDK JavaScript-bibliotheek

Stel de `renderDecisions` boolean wanneer de `sendEvent` gebruiken. Indien weggelaten, wordt deze eigenschap standaard ingesteld op `false`. Deze eigenschap instellen op `true` als u gepersonaliseerde inhoud automatisch wilt renderen.

>[!IMPORTANT]
>
>De `renderDecisions` eigenschap is onverenigbaar met de [`documentUnloading`](documentunloading.md) eigenschap. U moet beide eigenschappen niet instellen op `true` tegelijkertijd.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
