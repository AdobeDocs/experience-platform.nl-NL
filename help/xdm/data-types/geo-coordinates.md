---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;coördinaten;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-coördinaten
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo Coordinates XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 2%

---


# [!UICONTROL Geo ] Coordinators, gegevenstype

[!UICONTROL Geo ] Coordinators is een standaard XDM gegevenstype dat de geografische coördinaten van een plaats beschrijft. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](https://schema.org/GeoCoordinates) wordt gedocumenteerd.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de coördinaten identificeren. |
| `_schema.elevation` | Dubbel | De specifieke hoogte van de gedefinieerde coördinaat. De waarde moet voldoen aan de [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-datum en wordt gemeten in meters. |
| `_schema.latitude` | Dubbel | De ondertekende verticale coördinaat van het geografische punt. |
| `_schema.longitude` | Dubbel | De ondertekende horizontale coördinaat van het geografische punt. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
