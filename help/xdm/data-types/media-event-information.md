---
title: Gegevenstype voor Media-gebeurtenis
description: Meer informatie over het gegevenstype Data Model (XDM) van het Media Event Information Experience.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# [!UICONTROL Media Event Information] gegevenstype

[!UICONTROL Media Event Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat media detailinformatie met betrekking tot de ervaringsgebeurtenis beschrijft.

![Een diagram van het gegevenstype Media Event Information.](../images/data-types/media-event-information.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informatie over mediagegevens met betrekking tot de ervaringsgebeurtenis. Dit gegevenstype wordt gebruikt voor beide [gegevensverzameling media](./media-collection-details.md) en [Mediagegevensrapportage](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL String] | Het tijdstip waarop een mediagebeurtenis heeft plaatsgevonden. |
| `mediaEventType` | [!UICONTROL String] | Het type media-gebeurtenis. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
