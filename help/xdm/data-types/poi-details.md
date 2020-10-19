---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;poi details;point of interest;point of interest details;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype van aandachtspunt
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Point of Interest Details.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---


# [!UICONTROL Gegevenstype van interessdetails]

[!UICONTROL Details] over punten van belang zijn een standaard XDM-gegevenstype dat de geografische gegevens beschrijft waar een gebeurtenis werd waargenomen.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beschrijft de bakkendetails actief voor de interactie POI. |
| `geoInteractionDetails` | [[!UICONTROL Gegevens over geointeractie]](./geo-interaction-details.md) | Beschrijft de geo details actief voor de interactie POI. |
| `category` | Tekenreeks | Een algemene categorie die door de beheerder van POI-definities is toegewezen voor het organiseren van de POI&#39;s. |
| `distanceToPOICenter` | Dubbel | De geschatte afstand van het POI-middelpunt in meters. |
| `locatingType` | Tekenreeks | Het mechanisme dat wordt gebruikt om locatie te bepalen. Tot de geaccepteerde waarden behoren: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Tekenreeks | Een naam die aan de POI is gegeven. |
| `poiID` | Tekenreeks | Een unieke id van de POI. |
| `type` | Tekenreeks | Het algemene type van POI die een typend die schema gebruikt door de beheerder van de POI definities wordt geselecteerd. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)