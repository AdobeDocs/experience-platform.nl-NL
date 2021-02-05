---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;geo vorm;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Geo-vorm
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Shape XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---


# [!UICONTROL Het type Geo ] Shapedata

[!UICONTROL Geo ] Shapis een standaard XDM gegevenstype dat de vorm van een geografisch gebied beschrijft. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](https://schema.org/GeoShape) wordt gedocumenteerd.

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.box` | Array van [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft een geografisch gebied dat wordt omsloten door een rechthoek die wordt gevormd door twee coördinaten. De eerste coördinaat is de onderhoek van de rechthoek en de tweede coördinaat is de bovenhoek. |
| `_schema.circle` | Array van [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft een cirkelvormig gebied met een specifieke straal gecentreerd op een geografische coördinaat. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Een reeks van vier of meer coördinaten waarbij de eerste en laatste coördinaten identiek zijn. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de vorm definieert. |
| `_schema.elevation` | Dubbel | De specifieke of minimale hoogte van de vorm. Deze waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-gegeven en wordt gemeten in meters. In combinatie met `ceiling` kan deze eigenschap worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de vorm. |
| `ceiling` | Dubbel | De maximale hoogte van de vorm. Deze eigenschap is alleen geldig in combinatie met `elevation`. De waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-gegeven en wordt gemeten in meters. In combinatie met `elevation` kan deze eigenschap worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
