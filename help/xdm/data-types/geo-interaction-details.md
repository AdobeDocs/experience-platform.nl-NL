---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schemas;baken;interactiedetails;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Geo-interactie
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor Geo Interaction Details.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!UICONTROL Geo interaction details] gegevenstype

[!UICONTROL Geo interaction details] is een standaard XDM gegevenstype dat de huidige staat van opneming in een geografisch bepaald gebied beschrijft.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | Beschrijft de geo-vorm van het gebied waarmee wordt gewerkt. In dit veld kunt u een vak, cirkel of veelhoek beschrijven. |
| `deviceGeoAccuracy` | Dubbel | De nauwkeurigheid van de geo-meetinrichting of -mechanisme, gemeten in meters. |
| `distanceToCenter` | Dubbel | De afstand tot het middelpunt van de geo in het geval van een geocirkel, gemeten in meters. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
