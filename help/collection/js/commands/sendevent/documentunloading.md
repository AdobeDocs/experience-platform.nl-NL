---
title: documentUnloading
description: Gebruik de JavaScript sendBeacon-API om gegevens naar Adobe te verzenden.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

Met de eigenschap `documentUnloading` kunt u de JavaScript-methode [`sendBeacon` ](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) gebruiken om gegevens naar Adobe te verzenden. Als een typisch verzoek te lang duurt, kan browser het verzoek annuleren. U kunt de SDK van het Web vertellen om `sendBeacon` te gebruiken zodat het verzoek op de achtergrond loopt nadat u vanaf de pagina navigeert. Schakel deze eigenschap in om te voorkomen dat gegevensaanvragen door de browser worden geannuleerd wanneer ze worden verwijderd.

In verschillende browsers geldt een limiet van 64 kB voor de hoeveelheid gegevens die tegelijk met `sendBeacon` kan worden verzonden. Als browser de gebeurtenis verwerpt omdat de lading te groot is, het Web SDK terug naar het gebruiken van zijn normale vervoermethode valt. Zelfs als een bepaalde browser grotere ladingen toestaat, beperken de servers van de gegevensinzameling van Adobe nuttige ladingen tot 64 KB.

Stel de Booleaanse waarde `documentUnloading` in wanneer u de opdracht `sendEvent` uitvoert. De standaardwaarde is `false` . Stel deze eigenschap in op `true` als u de methode `sendBeacon` wilt gebruiken om gegevens naar Adobe te verzenden.

>[!IMPORTANT]
>
>De eigenschap `documentUnloading` is niet compatibel met de eigenschap [`renderDecisions`](renderdecisions.md) . Stel beide eigenschappen niet tegelijkertijd in op `true` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Document wordt verwijderd met de webtagextensie SDK

Het selectievakje **[!UICONTROL Document will unload]** is beschikbaar wanneer u een handeling [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) configureert wanneer u de extensie van de SDK-tag Web gebruikt.
