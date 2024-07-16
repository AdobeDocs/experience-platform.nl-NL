---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;poi;poi details;punt van belang;punt details;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype interessdetails
description: Meer informatie over het XDM-gegevenstype Point of Interest Details.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# [!UICONTROL Point of interest details] gegevenstype

[!UICONTROL Point of interest details] is een standaard XDM-gegevenstype dat de geografische gegevens beschrijft waar een gebeurtenis werd waargenomen.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beschrijft de bakkendetails actief voor de interactie POI. |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | Beschrijft de geo details actief voor de interactie POI. |
| `category` | String | Een algemene categorie die door de beheerder van POI-definities is toegewezen voor het organiseren van de POI&#39;s. |
| `distanceToPOICenter` | Dubbel | De geschatte afstand van het POI-middelpunt in meters. |
| `locatingType` | String | Het mechanisme dat wordt gebruikt om locatie te bepalen. Tot de geaccepteerde waarden behoren: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Een naam die aan de POI is gegeven. |
| `poiID` | String | Een unieke id van de POI. |
| `type` | String | Het algemene type van POI die een typend die schema gebruikt door de beheerder van de POI definities wordt geselecteerd. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
