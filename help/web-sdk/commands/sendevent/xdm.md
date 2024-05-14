---
title: xdm
description: Leer hoe u gegevens naar Adobe verzendt via het XDM-schema-uitgelijnde object.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# `xdm`

De `xdm` -object bevat de gegevenslading die naar de Adobe is verzonden. Velden die in dit object zijn ingesteld, worden rechtstreeks toegewezen aan elementen die in het schema van de gegevensset zijn gedefinieerd.

Adobe Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens.

Dit object heeft een maximumlimiet van 32 kB.

## Vorm het voorwerp XDM gebruikend de uitbreiding van SDK van het Web

Stel de **[!UICONTROL XDM]** -object binnen de handelingen van een labelregel. De [XDM-object](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) biedt een intuïtieve interface voor het toewijzen van andere gegevenselementen aan hun respectievelijke XDM-velden.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Geef het gegevenselement op dat het gewenste object bevat in het dialoogvenster **[!UICONTROL XDM]** veld.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Het XDM-object configureren met de Web SDK JavaScript-bibliotheek

Stel de `xdm` object wanneer het `sendEvent` gebruiken. Zorg ervoor dat de hiërarchie in dit voorwerp het schema voor de gevormde dataset aanpast. U kunt beide opties opnemen `xdm` en de [`data`](data.md) object in hetzelfde `sendEvent` gebruiken.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

In het volgende voorbeeld wordt het [Commerce-detailschema, veldgroep](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```
