---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: Geo Coordinates, gegevenstype
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Coordinates XDM.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 2%

---


# [!UICONTROL Geo Coordinates] , gegevenstype

[!UICONTROL Geo Coordinates] is een standaard XDM gegevenstype dat de geografische coördinaten van een plaats beschrijft. Dit gegevenstype is gebaseerd op de openbare die specificatie op [schema.org](https://schema.org/GeoCoordinates)wordt gedocumenteerd.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de coördinaten identificeren. |
| `_schema.elevation` | Dubbel | De specifieke hoogte van de gedefinieerde coördinaat. De waarde moet overeenkomen met het [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) -gegeven en wordt gemeten in meters. |
| `_schema.latitude` | Dubbel | De ondertekende verticale coördinaat van het geografische punt. |
| `_schema.longitude` | Dubbel | De ondertekende horizontale coördinaat van het geografische punt. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
