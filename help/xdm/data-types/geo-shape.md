---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype GeoShape
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Shape XDM.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---


# [!UICONTROL Gegevenstype Geo] Shape

[!UICONTROL Geo Shape] is een standaard XDM-gegevenstype dat de vorm van een geografisch gebied beschrijft. Dit gegevenstype is gebaseerd op de openbare die specificatie op [schema.org](https://schema.org/GeoShape)wordt gedocumenteerd.

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.box` | Array van [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft een geografisch gebied dat wordt omsloten door een rechthoek die wordt gevormd door twee coördinaten. De eerste coördinaat is de onderhoek van de rechthoek en de tweede coördinaat is de bovenhoek. |
| `_schema.circle` | Array van [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft een cirkelvormig gebied met een specifieke straal gecentreerd op een geografische coördinaat. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Een reeks van vier of meer coördinaten waarbij de eerste en laatste coördinaten identiek zijn. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de vorm definieert. |
| `_schema.elevation` | Dubbel | De specifieke of minimale hoogte van de vorm. Deze waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) -gegeven en wordt gemeten in meters. In combinatie met `ceiling`, kan dit bezit worden gebruikt om een driedimensionaal bounding doos voor een plaats uit te drukken. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de vorm. |
| `ceiling` | Dubbel | De maximale hoogte van de vorm. Deze eigenschap is alleen geldig in combinatie met `elevation`. De waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) -gegeven en wordt gemeten in meters. In combinatie met `elevation`, kan dit bezit worden gebruikt om een driedimensionaal bounding doos voor een plaats uit te drukken. |
