---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schemas;baken;interactiedetails;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Geo-interactie
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor Geo Interaction Details.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# [!UICONTROL Geo interactie ] detailsgegevenstype

[!UICONTROL De interactie van geo ] detailleert een standaard XDM gegevenstype dat de huidige staat van opneming in een geografisch bepaald gebied beschrijft.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-vorm]](./geo-shape.md) | Beschrijft de geo-vorm van het gebied waarmee wordt gewerkt. In dit veld kunt u een vak, cirkel of veelhoek beschrijven. |
| `deviceGeoAccuracy` | Dubbel | De nauwkeurigheid van de geo-meetinrichting of -mechanisme, gemeten in meters. |
| `distanceToCenter` | Dubbel | De afstand tot het middelpunt van de geo in het geval van een geocirkel, gemeten in meters. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
