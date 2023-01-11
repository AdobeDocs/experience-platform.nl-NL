---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;coördinaten;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-coördinaten
description: Dit document biedt een overzicht van het gegevenstype Geo Coordinates XDM.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

---

# [!UICONTROL Geo Coordinates] gegevenstype

[!UICONTROL Geo Coordinates] is een standaard XDM gegevenstype dat de geografische coördinaten van een plaats beschrijft. Dit gegevenstype is gebaseerd op de openbare specificatie die op [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.description` | Tekenreeks | Een beschrijving van wat de coördinaten identificeren. |
| `_schema.elevation` | Dubbel | De specifieke hoogte van de gedefinieerde coördinaat. De waarde moet overeenkomen met de [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum en wordt gemeten in meters. |
| `_schema.latitude` | Dubbel | De ondertekende verticale coördinaat van het geografische punt. |
| `_schema.longitude` | Dubbel | De ondertekende horizontale coördinaat van het geografische punt. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
