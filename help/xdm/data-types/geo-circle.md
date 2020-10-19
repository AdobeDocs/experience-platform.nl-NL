---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype Geo Circle
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Circle XDM.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 2%

---


# [!UICONTROL Gegevenstype Geo Circle]

[!UICONTROL Geo Circle] is een standaard XDM-gegevenstype dat cirkelvormige geografische regio beschrijft, op basis van een bepaalde straal die op een bepaalde set coördinaten is gecentreerd. Dit gegevenstype is gebaseerd op de openbare die specificatie op [schema.org](http://schema.org/GeoCircle)wordt gedocumenteerd.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van het centrum van de cirkel. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de cirkel bevat. |
| `_schema.radius` | Dubbel | De lengte van de straal van de cirkel. Deze waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) -gegeven en wordt gemeten in meters. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de cirkel. |
