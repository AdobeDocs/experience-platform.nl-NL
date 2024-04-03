---
title: Lijst met statussen Gegevenstype verzameling starten
description: Leer over de Lijst van het gegevenstype van het Begin van het Gegevensmodel van de Ervaring (XDM) gegevenstype.
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# [!UICONTROL List of States Start] gegevenstype

De [!UICONTROL List of States Start] Het gegevenstype is een XDM-gegevenstype (Experience Data Model) dat is ontworpen voor het weergeven van informatie die betrekking heeft op de begintoestand van verschillende spelerkenmerken. Het omvat de [!UICONTROL Player State Name] eigenschappen die de specifieke kenmerkstatus aangeven (bijvoorbeeld &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dit gegevenstype wordt gebruikt om de beginvoorwaarden van de verschillende spelerstatussen vast te leggen en te beschrijven.

![Een schema van [!UICONTROL List of States Start] gegevenstype.](../images/data-types/list-of-states-start-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nee | De naam van de spelerstatus. Opsommend: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; met respectieve betekenissen. |

{style="table-layout:auto"}
