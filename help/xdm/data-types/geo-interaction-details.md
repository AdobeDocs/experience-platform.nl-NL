---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype van geointeractie
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor Geo Interaction Details.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype van geo-interactie]

[!UICONTROL De interactiedetails] van geo is een standaard XDM gegevenstype dat de huidige staat van opneming in een geografisch bepaald gebied beschrijft.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-vorm]](./geo-shape.md) | Beschrijft de geo-vorm van het gebied waarmee wordt gewerkt. In dit veld kunt u een vak, cirkel of veelhoek beschrijven. |
| `deviceGeoAccuracy` | Dubbel | De nauwkeurigheid van de geo-meetinrichting of -mechanisme, gemeten in meters. |
| `distanceToCenter` | Dubbel | De afstand tot het middelpunt van de geo in het geval van een geocirkel, gemeten in meters. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
