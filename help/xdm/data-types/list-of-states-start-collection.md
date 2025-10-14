---
title: Lijst met statussen Gegevenstype verzameling starten
description: Leer over de Lijst van het gegevenstype van het Begin van het Gegevensmodel van de Ervaring (XDM) gegevenstype.
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# [!UICONTROL List of States Start] gegevenstype

Het gegevenstype [!UICONTROL List of States Start] is een XDM-gegevenstype (Experience Data Model) dat is ontworpen voor het weergeven van informatie die betrekking heeft op de begintoestand van verschillende spelerkenmerken. Deze bevat de eigenschappen [!UICONTROL Player State Name] die de specifieke kenmerkstatus aangeven (bijvoorbeeld &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dit gegevenstype wordt gebruikt om de beginvoorwaarden van de verschillende spelerstatussen vast te leggen en te beschrijven.

![&#x200B; een diagram van [!UICONTROL List of States Start] gegevenstype.](../images/data-types/list-of-states-start-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nee | De naam van de spelerstatus. Opsommend: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; met respectieve betekenissen. |

{style="table-layout:auto"}
