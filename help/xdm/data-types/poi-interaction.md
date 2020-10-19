---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype van interactie van het punt van belang
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Point of Interest Interaction.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype voor interactie] van het aandachtspunt

[!UICONTROL Interactie] van het punt van belang is een standaard XDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `poiDetail` | [!UICONTROL Details van het belangenpunt](./poi-details.md) | Beschrijft de details van POI die de gebeurtenis veroorzaakte. |
| `poiEntries` | Object | Beschrijft het aantal tijden een persoon POI is ingegaan. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |
| `poiExits` | Object | Beschrijft het aantal tijden een persoon POI heeft verlaten. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
