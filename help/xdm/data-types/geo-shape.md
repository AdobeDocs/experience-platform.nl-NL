---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;geo vorm;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Geo-vorm
description: Leer meer over het gegevenstype Geo Shape XDM.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL Geo Shape] gegevenstype

[!UICONTROL Geo Shape] is een standaard XDM gegevenstype dat de vorm van een geografisch gebied beschrijft. Dit gegevenstype is gebaseerd op de openbare die specificatie op [&#x200B; wordt gedocumenteerd schema.org &#x200B;](https://schema.org/GeoShape).

![](../images/data-types/geo-shape.png){width=500}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.box` | Array van [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft een geografisch gebied dat wordt omsloten door een rechthoek die wordt gevormd door twee coördinaten. De eerste coördinaat is de onderhoek van de rechthoek en de tweede coördinaat is de bovenhoek. |
| `_schema.circle` | Array van [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft een cirkelvormig gebied met een specifieke straal die op een geografische coördinaat wordt gecentreerd. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Een reeks van vier of meer coördinaten waarbij de eerste en laatste coördinaten identiek zijn. |
| `_schema.description` | String | Een beschrijving van wat de vorm definieert. |
| `_schema.elevation` | Dubbel | De specifieke of minimale hoogte van de vorm. Deze waarde is aan het [&#x200B; WGS84 &#x200B;](https://gisgeography.com/wgs84-world-geodetic-system/) gegeven en in meters gemeten. In combinatie met `ceiling` kan deze eigenschap worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
| `_id` | String | Een unieke, door het systeem gegenereerde id voor de vorm. |
| `ceiling` | Dubbel | De maximale hoogte van de vorm. Deze eigenschap is alleen geldig in combinatie met `elevation` . De waarde is met het [&#x200B; WGS84 &#x200B;](https://gisgeography.com/wgs84-world-geodetic-system/) gegeven in overeenstemming en in meters gemeten. In combinatie met `elevation` kan deze eigenschap worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
