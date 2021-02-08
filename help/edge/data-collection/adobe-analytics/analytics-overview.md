---
title: Gegevens verzenden naar Adobe Analytics
seo-title: Gegevens verzenden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Meer informatie over het verzenden van gegevens naar Adobe Analytics met Web SDK van Experience Platform
seo-description: Meer informatie over het verzenden van gegevens naar Adobe Analytics met Web SDK van Experience Platform
keywords: adobe analytics;analytics;mapped data;mapped vars;
translation-type: tm+mt
source-git-commit: 723711ee0c2b7b5ca4aea617a81241dbebbc839c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

De Adobe Experience Platform [!DNL Web SDK] kan gegevens naar Adobe Analytics verzenden. Dit werkt door `xdm` in een formaat te vertalen de Adobe Analytics kan gebruiken.

## Instellen

Adobe Analytics haalt de gegevens die u verzendt automatisch op als u een rapportsuite hebt toegewezen in de gebruikersinterface van Customer Config. Hier kunt u één of meerdere rapporten aan een bepaalde config in kaart brengen. Nadat een rapportsuite is toegewezen, beginnen de gegevens automatisch te stromen.

## Automatisch toegewezen gegevens

De Adobe Experience Platform [!DNL Edge Network] wijst automatisch veel XDM-variabelen toe. De volledige lijst van deze variabelen wordt [hier](automatically-mapped-vars.md) vermeld.

## Handmatig toegewezen gegevens

Alle gegevens die door het randnetwerk worden verzameld, zijn toegankelijk via verwerkingsregels. De gegevens worden afgevlakt met behulp van puntnotatie en zijn beschikbaar als contextData.

Als je een schema had dat er zo uitzag.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Dan zouden dit de sleutels van contextgegevens beschikbaar aan u zijn.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

Hier volgt een voorbeeld van een verwerkingsregel waarin deze gegevens worden gebruikt.

![Interface voor verwerkingsregels](../../../assets/edge_analytics_processing_rules.png)
