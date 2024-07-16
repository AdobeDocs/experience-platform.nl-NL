---
title: eventType
description: Plaats het type van gebeurtenis voor een sendEvent vraag.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# `eventType`

Met de eigenschap `eventType` kunt u het type gebeurtenis definiëren dat u verzendt met de SDK van het web. In dit veld wordt het veld `xdm.eventType` uiteindelijk gevuld. Het is nuttig wanneer u de gebeurtenistypen wilt onderscheiden die u naar Adobe verzendt.

Adobe biedt enkele vooraf gedefinieerde gebeurtenistypen die u kunt gebruiken. Zie [ Beschikbare waarden voor `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) in de XDM gebruikersgids voor een volledige lijst van vooraf bepaalde waarden. U kunt desgewenst ook uw eigen waarden gebruiken.

Wanneer u zowel `type` hier als `xdm.eventType` in het [`xdm`](xdm.md) -object instelt, krijgt de waarde in dit veld prioriteit.

## Gebeurtenistype configureren met de web SDK-tagextensie

Stel het vervolgkeuzeveld **[!UICONTROL Type]** in binnen de handelingen van een labelregel.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Gebruik de vervolgkeuzelijst onder het veld **[!UICONTROL Type]** of voer uw eigen waarde in.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Gebeurtenistype configureren met de Web SDK JavaScript-bibliotheek

Stel de eigenschap `eventType` string in wanneer u de opdracht `sendEvent` uitvoert.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
