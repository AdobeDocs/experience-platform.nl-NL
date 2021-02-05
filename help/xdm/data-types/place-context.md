---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;place context;placeContext;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Contextgegevenstype plaatsen
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Context plaatsen.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---


# [!UICONTROL Het ] gegevenstype ContextData plaatsen

[!UICONTROL Plaatst ] context een standaard XDM gegevenstype dat de plaats van een waargenomen gebeurtenis, met inbegrip van punt-van-belangeninformatie en geografische coördinaten beschrijft.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interactie van aandachtspunten]](./poi-interaction.md) | Beschrijft details over de punt-van-belang (POI) interactie. |
| `activePOIs` | Array van [[!UICONTROL Gegevens betreffende het punt]](./poi-details.md) | Beschrijft POIs die de gebeurtenis veroorzaakte. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschrijft de geografische plaats waar de ervaring werd geleverd. |
| `localTime` | DateTime | Een tijdstempel in de notatie [RFC 3339](https://tools.ietf.org/html/rfc3339) die de lokale tijd aangeeft die wordt gebruikt met een opgegeven verschuiving van de tijdzone. Het opmaakpatroon is `yyyy-MM-dd'T'HH:mm:ssXXX` (bijvoorbeeld `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Geheel | De huidige lokale tijdzoneverschuiving in minuten vanaf UTC voor de waarde `localTime`. Dit moet, indien van toepassing, de huidige DST-verschuiving omvatten. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)