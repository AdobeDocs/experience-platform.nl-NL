---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;geo vorm;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Geo-vorm
topic-legacy: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Shape XDM.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 1%

---

# [!UICONTROL Geo Shape] gegevenstype

[!UICONTROL Geo Shape] is een standaard XDM gegevenstype dat de vorm van een geografisch gebied beschrijft. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.box` | Array van [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft een geografisch gebied dat wordt omsloten door een rechthoek die wordt gevormd door twee coördinaten. De eerste coördinaat is de onderhoek van de rechthoek en de tweede coördinaat is de bovenhoek. |
| `_schema.circle` | Array van [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft een cirkelvormig gebied met een specifieke straal die op een geografische coördinaat wordt gecentreerd. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Een reeks van vier of meer coördinaten waarbij de eerste en laatste coördinaten identiek zijn. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de vorm definieert. |
| `_schema.elevation` | Dubbel | De specifieke of minimale hoogte van de vorm. Deze waarde is in overeenstemming met de [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum en wordt gemeten in meters. In combinatie met `ceiling`Deze eigenschap kan worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de vorm. |
| `ceiling` | Dubbel | De maximale hoogte van de vorm. Deze eigenschap is alleen geldig in combinatie met `elevation`. De waarde is in overeenstemming met de [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum en wordt gemeten in meters. In combinatie met `elevation`Deze eigenschap kan worden gebruikt om een driedimensionaal selectiekader voor een locatie uit te drukken. |
