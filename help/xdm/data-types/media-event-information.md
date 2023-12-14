---
title: Gegevenstype voor Media-gebeurtenis
description: Meer informatie over het gegevenstype Data Model (XDM) van het Media Event Information Experience.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 1%

---

# [!UICONTROL Media event information] gegevenstype

[!UICONTROL Media Event Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat media detailinformatie met betrekking tot de ervaringsgebeurtenis beschrijft.

![Een diagram van het gegevenstype Media Event Information.](../images/data-types/media-event-information.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Informatie over mediagegevens met betrekking tot de ervaringsgebeurtenis. |
| `mediaEventTimestamp` | [!UICONTROL String] | Het tijdstip waarop een mediagebeurtenis heeft plaatsgevonden. |
| `mediaEventType` | [!UICONTROL String] | Het type media-gebeurtenis. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
