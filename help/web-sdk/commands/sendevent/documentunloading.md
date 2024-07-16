---
title: documentUnloading
description: Gebruik de JavaScript sendBeacon-API om gegevens naar de Adobe te verzenden.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# `documentUnloading`

Met de eigenschap `documentUnloading` kunt u de JavaScript-methode [`sendBeacon` ](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) gebruiken om gegevens naar de Adobe te verzenden. Als een typisch verzoek te lang duurt, kan browser het verzoek annuleren. U kunt de SDK van het Web vertellen om `sendBeacon` te gebruiken zodat het verzoek op de achtergrond loopt nadat u vanaf de pagina navigeert. Schakel deze eigenschap in om te voorkomen dat gegevensaanvragen door de browser worden geannuleerd wanneer ze worden verwijderd.

In verschillende browsers geldt een limiet van 64 kB voor de hoeveelheid gegevens die tegelijk met `sendBeacon` kan worden verzonden. Als browser de gebeurtenis verwerpt omdat de lading te groot is, valt SDK van het Web terug naar het gebruiken van zijn normale vervoermethode.

## Document verwijderen configureren met de webSDK-tagextensie

Schakel het selectievakje **[!UICONTROL Document will unload]** in binnen de handelingen van een labelregel.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Schakel het selectievakje **[!UICONTROL Document will unload]** in de sectie [!UICONTROL Data] in.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Document verwijderen configureren met de Web SDK JavaScript-bibliotheek

Stel de Booleaanse waarde `documentUnloading` in wanneer u de opdracht `sendEvent` uitvoert. De standaardwaarde is `false` . Stel deze eigenschap in op `true` als u de methode `sendBeacon` wilt gebruiken om gegevens naar de Adobe te verzenden.

>[!IMPORTANT]
>
>De eigenschap `documentUnloading` is niet compatibel met de eigenschap [`renderDecisions`](renderdecisions.md) . Stel beide eigenschappen niet tegelijkertijd in op `true` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
