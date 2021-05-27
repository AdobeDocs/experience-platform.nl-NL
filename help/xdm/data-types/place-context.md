---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;place context;placeContext;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Contextgegevenstype plaatsen
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Context plaatsen.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# [!UICONTROL Place context] gegevenstype

[!UICONTROL Place context] is een standaard XDM gegevenstype dat de plaats van een waargenomen gebeurtenis, met inbegrip van punt-van-belang informatie en geografische coördinaten beschrijft.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Beschrijft details over de punt-van-belang (POI) interactie. |
| `activePOIs` | Array van [[!UICONTROL Point of interest details]](./poi-details.md) | Beschrijft POIs die de gebeurtenis veroorzaakte. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschrijft de geografische plaats waar de ervaring werd geleverd. |
| `localTime` | DateTime | Een tijdstempel in de notatie [RFC 3339](https://tools.ietf.org/html/rfc3339) die de lokale tijd aangeeft die wordt gebruikt met een opgegeven verschuiving van de tijdzone. Het opmaakpatroon is `yyyy-MM-dd'T'HH:mm:ssXXX` (bijvoorbeeld `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Geheel | De huidige lokale tijdzoneverschuiving in minuten vanaf UTC voor de waarde `localTime`. Dit moet, indien van toepassing, de huidige DST-verschuiving omvatten. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
