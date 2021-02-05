---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;circle;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-cirkel
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Circle XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 2%

---


# [!UICONTROL Het type Geo ] CircleData

[!UICONTROL Geo ] Circle is een standaard XDM gegevenstype dat cirkelvormig geografisch gebied beschrijft, gegeven een bepaalde straal die op een specifieke reeks coördinaten wordt gecentreerd. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](http://schema.org/GeoCircle) wordt gedocumenteerd.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van het centrum van de cirkel. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de cirkel bevat. |
| `_schema.radius` | Dubbel | De lengte van de straal van de cirkel. Deze waarde komt overeen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-gegeven en wordt gemeten in meters. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de cirkel. |
