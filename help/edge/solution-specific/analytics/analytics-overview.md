---
title: Gegevens verzenden naar Adobe Analytics
seo-title: Gegevens verzenden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Meer informatie over het verzenden van gegevens naar Adobe Analytics met Experience Platform Web SDK
seo-description: Meer informatie over het verzenden van gegevens naar Adobe Analytics met Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

De Adobe Experience Platform Web SDK kan gegevens verzenden naar Adobe Analytics. Dit werkt door te vertalen `xdm` in een indeling die Adobe Analytics kan gebruiken.

## Instellen

Adobe Analytics haalt automatisch de gegevens op die u verzendt als u een rapportsuite hebt toegewezen in de gebruikersinterface van Customer Config. Hier kunt u één of meerdere rapporten aan een bepaalde config in kaart brengen. Nadat een rapportsuite is toegewezen, beginnen de gegevens automatisch te stromen.

## Automatisch toegewezen gegevens

Het Adobe Experience Platform Edge Network wijst automatisch veel XDM-variabelen toe. De volledige lijst met automatisch toegewezen variabelen wordt [hier](../analytics/automatically-mapped-vars.md)weergegeven.

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
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

Dan zouden dit de sleutels van contextgegevens beschikbaar aan u zijn.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Hier volgt een voorbeeld van een verwerkingsregel waarin deze gegevens worden gebruikt.

![Interface voor verwerkingsregels](../../../assets/edge_analytics_processing_rules.png)
