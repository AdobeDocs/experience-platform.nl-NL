---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;circle;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-cirkel
topic-legacy: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Circle XDM.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

---

# [!UICONTROL Geo Circle] gegevenstype

[!UICONTROL Geo Circle] is een standaard XDM gegevenstype dat cirkelvormig geografisch gebied beschrijft, gegeven een bepaalde straal gecentreerd op een specifieke reeks coördinaten. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van het centrum van de cirkel. |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de cirkel bevat. |
| `_schema.radius` | Dubbel | De lengte van de straal van de cirkel. Deze waarde is in overeenstemming met de [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum en wordt gemeten in meters. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de cirkel. |
