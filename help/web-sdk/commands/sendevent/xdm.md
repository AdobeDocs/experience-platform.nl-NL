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

Het `xdm` -object bevat de gegevenslading die naar de Adobe is verzonden. Velden die in dit object zijn ingesteld, worden rechtstreeks toegewezen aan elementen die in het schema van de gegevensset zijn gedefinieerd.

Adobe Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens.

Dit object heeft een maximumlimiet van 32 kB.

## Vorm het voorwerp XDM gebruikend de uitbreiding van SDK van het Web

Stel het **[!UICONTROL XDM]** -object in binnen de handelingen van een labelregel. Het [&#x200B; voorwerp XDM &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) verstrekt een intuïtieve interface om andere gegevenselementen aan hun respectieve gebieden in kaart te brengen XDM.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Geef het gegevenselement met het gewenste object op in het veld **[!UICONTROL XDM]** .
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Het XDM-object configureren met de Web SDK JavaScript-bibliotheek

Stel het object `xdm` in wanneer u de opdracht `sendEvent` uitvoert. Zorg ervoor dat de hiërarchie in dit voorwerp het schema voor de gevormde dataset aanpast. U kunt zowel het object `xdm` als het object [`data`](data.md) in dezelfde opdracht `sendEvent` opnemen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Het volgende voorbeeld gebruikt de [&#x200B; het schemagroep van Details van Commerce &#x200B;](/help/xdm/field-groups/event/commerce-details.md):

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
