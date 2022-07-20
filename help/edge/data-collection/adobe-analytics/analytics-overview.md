---
title: Adobe Analytics gebruiken met Platform Web SDK
description: Leer hoe u gegevens naar Adobe Analytics verzendt met de Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f627c1f6c917e74e0a366ce0611a1fa6bd0e3c3d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Analytics gebruiken met Platform Web SDK

De Adobe Experience Platform [!DNL Web SDK] kan gegevens naar Adobe Analytics verzenden. Dit werkt door te vertalen `xdm` in een indeling die de Adobe Analytics kan gebruiken.

## Instellen

Adobe Analytics haalt de gegevens die u verzendt automatisch op als u een rapportsuite hebt toegewezen in de gebruikersinterface van Customer Config. Hier kunt u één of meerdere rapporten aan een bepaalde config in kaart brengen. Nadat een rapportsuite is toegewezen, beginnen de gegevens automatisch te stromen.

## XDM-veldgroep

Om het gemakkelijker te maken om de gemeenschappelijkste metriek van Adobe Analytics te vangen, verstrekken wij een het gebiedsgroep van Analytics die u kunt gebruiken. Raadpleeg de documentatie bij het dialoogvenster [Adobe Analytics ExperienceEvent Volledige extensieschema, veldgroep](../../../xdm/field-groups/event/analytics-full-extension.md)

## Automatisch toegewezen gegevens

De Adobe Experience Platform [!DNL Edge Network] Hiermee worden veel XDM-variabelen automatisch toegewezen. De volledige lijst met deze variabelen wordt weergegeven [hier](automatically-mapped-vars.md).

## Handmatig toegewezen gegevens

Gegevens die niet automatisch door het Edge-netwerk worden toegewezen, zijn toegankelijk via verwerkingsregels. De gegevens worden afgevlakt met behulp van puntnotatie en zijn beschikbaar als contextData.

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

![Interface voor verwerkingsregels](./assets/edge_analytics_processing_rules.png)
