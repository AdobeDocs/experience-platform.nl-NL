---
title: xdm
description: Leer hoe u gegevens naar Adobe verzendt via het XDM-schema-uitgelijnde object.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

Het `xdm` -object bevat de gegevenslading die naar Adobe is verzonden. Velden die in dit object zijn ingesteld, worden rechtstreeks toegewezen aan elementen die in het schema van de gegevensset zijn gedefinieerd.

Adobe Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens.

Stel het object `xdm` in wanneer u de opdracht `sendEvent` uitvoert. Zorg ervoor dat de hiërarchie in dit voorwerp het schema voor de gevormde dataset aanpast. U kunt zowel het object `xdm` als het object [`data`](data.md) in dezelfde opdracht `sendEvent` opnemen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Het volgende voorbeeld gebruikt de [ het schemagroep van Details van Commerce ](/help/xdm/field-groups/event/commerce-details.md):

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

## Het `xdm` -object gebruiken met de extensie van de Web SDK-tag

Het `xdm` voorwerp is beschikbaar als of a [ Variabel gegevenselement ](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) of [ XDM objecten gegevenselement ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) wanneer het gebruiken van de de markeringsuitbreiding van SDK van het Web. Adobe raadt in de meeste gevallen aan een gegevenselement met variabele gegevens te gebruiken.
