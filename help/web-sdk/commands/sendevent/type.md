---
title: eventType
description: Plaats het type van gebeurtenis voor een sendEvent vraag.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# `eventType`

De `eventType` het bezit staat u toe om het type van gebeurtenis te bepalen u gebruikend het Web SDK verzendt. In dit veld wordt uiteindelijk de waarde `xdm.eventType` veld. Het is nuttig wanneer u de gebeurtenistypen wilt onderscheiden die u naar Adobe verzendt.

Adobe biedt enkele vooraf gedefinieerde gebeurtenistypen die u kunt gebruiken. Zie [Beschikbare waarden voor `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) in de XDM-gebruikershandleiding voor een volledige lijst met vooraf gedefinieerde waarden. U kunt desgewenst ook uw eigen waarden gebruiken.

Als u beide instelt `type` hier en `xdm.eventType` in de [`xdm`](xdm.md) -object heeft de waarde in dit veld prioriteit.

## Gebeurtenistype configureren met de web SDK-tagextensie

Stel de **[!UICONTROL Type]** vervolgkeuzelijst binnen de handelingen van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Het vervolgkeuzemenu onder de **[!UICONTROL Type]** of voer uw eigen waarde in.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Gebeurtenistype configureren met de Web SDK JavaScript-bibliotheek

Stel de `eventType` tekenreekseigenschap wanneer de `sendEvent` gebruiken.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
