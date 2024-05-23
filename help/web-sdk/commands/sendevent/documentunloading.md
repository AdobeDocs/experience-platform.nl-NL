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

De `documentUnloading` kunt u JavaScript gebruiken [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) methode om gegevens naar Adobe te verzenden. Als een typisch verzoek te lang duurt, kan browser het verzoek annuleren. U kunt de SDK van het Web aan gebruik vertellen `sendBeacon` zodat de aanvraag op de achtergrond wordt uitgevoerd nadat u bij de pagina vandaan navigeert. Schakel deze eigenschap in om te voorkomen dat gegevensaanvragen door de browser worden geannuleerd wanneer ze worden verwijderd.

Verschillende browsers stellen een limiet van 64 kB in voor de hoeveelheid gegevens die kan worden verzonden met `sendBeacon` in één keer. Als browser de gebeurtenis verwerpt omdat de lading te groot is, valt SDK van het Web terug naar het gebruiken van zijn normale vervoermethode.

## Document verwijderen configureren met de webSDK-tagextensie

De optie **[!UICONTROL Document will unload]** Schakel het selectievakje in binnen de handelingen van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Navigeren naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. De optie **[!UICONTROL Document will unload]** Selectievakje in het dialoogvenster [!UICONTROL Data] sectie.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Document verwijderen configureren met de Web SDK JavaScript-bibliotheek

Stel de `documentUnloading` boolean wanneer de `sendEvent` gebruiken. De standaardwaarde is `false`. Deze eigenschap instellen op `true` als u de opdracht `sendBeacon` methode om gegevens naar Adobe te verzenden.

>[!IMPORTANT]
>
>De `documentUnloading` eigenschap is onverenigbaar met de [`renderDecisions`](renderdecisions.md) eigenschap. U moet beide eigenschappen niet instellen op `true` tegelijkertijd.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
