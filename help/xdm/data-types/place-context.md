---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: Contextgegevenstype plaatsen
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Context plaatsen.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---


# [!UICONTROL Context] -gegevenstype plaatsen

[!UICONTROL De context] van de plaats is een standaard XDM gegevenstype dat de plaats van een waargenomen gebeurtenis, met inbegrip van punt-van-belang informatie en geografische coördinaten beschrijft.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interactie van aandachtspunten]](./poi-interaction.md) | Beschrijft details over de punt-van-belang (POI) interactie. |
| `activePOIs` | Array van [[!UICONTROL aandachtspunten]](./poi-details.md) | Beschrijft POIs die de gebeurtenis veroorzaakte. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschrijft de geografische plaats waar de ervaring werd geleverd. |
| `localTime` | DateTime | Een tijdstempel in [RFC 3339](https://tools.ietf.org/html/rfc3339) -indeling die de lokale tijd aangeeft die wordt gebruikt met een opgegeven tijdzoneverschuiving. Het opmaakpatroon is `yyyy-MM-dd'T'HH:mm:ssXXX` (bijvoorbeeld `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Geheel | De huidige lokale tijdzoneverschuiving in minuten vanaf UTC voor de `localTime` waarde. Dit moet, indien van toepassing, de huidige DST-verschuiving omvatten. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)