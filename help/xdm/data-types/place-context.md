---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;place context;placeContext;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Contextgegevenstype plaatsen
description: Meer informatie over het XDM-gegevenstype Context plaatsen.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# [!UICONTROL Place context] gegevenstype

[!UICONTROL Place context] is een standaard XDM-gegevenstype dat de locatie van een waargenomen gebeurtenis beschrijft, inclusief informatie over punten en geografische coördinaten.

![](../images/data-types/place-context.png){width=500}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Beschrijft details over de punt-van-belang (POI) interactie. |
| `activePOIs` | Array van [[!UICONTROL Point of interest details]](./poi-details.md) | Beschrijft POIs die de gebeurtenis veroorzaakte. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschrijft de geografische plaats waar de ervaring werd geleverd. |
| `localTime` | DateTime | Een timestamp in [ RFC 3339 ](https://tools.ietf.org/html/rfc3339) formaat, die op de lokale tijd wijzen die met een verklaarde compensatie van de tijdzone gebruikt. Het opmaakpatroon is `yyyy-MM-dd'T'HH:mm:ssXXX` (bijvoorbeeld `2001-07-04T12:08:56-07:00` ). |
| `localTimezoneOffset` | Geheel | De huidige lokale tijdzoneverschuiving in minuten vanaf UTC voor de waarde `localTime` . Dit moet, indien van toepassing, de huidige DST-verschuiving omvatten. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
