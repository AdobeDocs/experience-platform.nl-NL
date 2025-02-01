---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;geo;coördinaten;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Geo-coördinaten
description: Meer informatie over het gegevenstype Geo Coordinates XDM.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# [!UICONTROL Geo Coordinates] gegevenstype

[!UICONTROL Geo Coordinates] is een standaard XDM gegevenstype dat de geografische coördinaten van een plaats beschrijft. Dit gegevenstype is gebaseerd op de openbare die specificatie op [ wordt gedocumenteerd schema.org ](https://schema.org/GeoCoordinates).

![](../images/data-types/geo-coordinates.png){width=400}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema.description` | String | Een beschrijving van wat de coördinaten identificeren. |
| `_schema.elevation` | Dubbel | De specifieke hoogte van de gedefinieerde coördinaat. De waarde moet met het [ WGS84 ](https://gisgeography.com/wgs84-world-geodetic-system/) gegeven in overeenstemming zijn en in meters gemeten. |
| `_schema.latitude` | Dubbel | De ondertekende verticale coördinaat van het geografische punt. |
| `_schema.longitude` | Dubbel | De ondertekende horizontale coördinaat van het geografische punt. |
| `_id` | String | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
