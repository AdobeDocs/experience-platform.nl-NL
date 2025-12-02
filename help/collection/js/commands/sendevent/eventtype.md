---
title: eventType
description: Plaats het type van gebeurtenis voor een sendEvent vraag.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

Met de eigenschap `eventType` kunt u het type gebeurtenis definiëren dat u verzendt via de Web SDK. In dit veld wordt het veld `xdm.eventType` uiteindelijk gevuld. Het is nuttig wanneer u de gebeurtenistypen wilt onderscheiden die u naar Adobe verzendt.

Adobe bevat enkele vooraf gedefinieerde gebeurtenistypen die u kunt gebruiken. Zie [ Beschikbare waarden voor `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) in de XDM gebruikersgids voor een volledige lijst van vooraf bepaalde waarden. U kunt desgewenst ook uw eigen waarden gebruiken.

Wanneer u zowel `type` hier als `xdm.eventType` in het [`xdm`](xdm.md) -object instelt, krijgt de waarde in dit veld prioriteit.

Stel de eigenschap `eventType` string in wanneer u de opdracht `sendEvent` uitvoert.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Gebeurtenistype met de Web SDK-tagextensie

Het equivalent van de de marktextensie van SDK van het Web van dit bezit is het [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) drop-down menu wanneer het vormen van een &quot;[!UICONTROL Send event]&quot;actie.
