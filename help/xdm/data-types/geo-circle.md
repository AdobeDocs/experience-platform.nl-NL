---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;circle;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-cirkel
description: Meer informatie over het gegevenstype Geo Circle XDM.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# [!UICONTROL Geo Circle] gegevenstype

[!UICONTROL Geo Circle] is een standaard XDM gegevenstype dat cirkelvormig geografisch gebied beschrijft, gegeven een bepaalde straal gecentreerd op een specifieke reeks coördinaten. Dit gegevenstype is gebaseerd op de openbare die specificatie op [ wordt gedocumenteerd schema.org ](https://schema.org/GeoCircle).

![](../images/data-types/geo-circle.png){width=400}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van het centrum van de cirkel. |
| `_schema.description` | String | Een beschrijving van wat de cirkel bevat. |
| `_schema.radius` | Dubbel | De lengte van de straal van de cirkel. Deze waarde is aan het [ WGS84 ](https://gisgeography.com/wgs84-world-geodetic-system/) gegeven en in meters gemeten. |
| `_id` | String | Een unieke, door het systeem gegenereerde id voor de cirkel. |
