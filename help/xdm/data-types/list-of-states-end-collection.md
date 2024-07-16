---
title: Lijst met gegevenstypen voor eindverzameling frames
description: Leer over de Lijst van het gegevenstype van de Ervaring van het Type van Gegevens van de Inzameling van het Eind van Staten Gegevenstype (XDM) gegevenstype.
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# [!UICONTROL List of States End] gegevenstype

Het gegevenstype van het gegevenstype Verzameling van het Eind van de Lijst van Staten is een gegevenstype van de Gegevens van de Ervaring Model (XDM) dat voor het vertegenwoordigen van informatie met betrekking tot de beëindigende staat van diverse spelerattributen wordt ontworpen. Deze bevat de eigenschappen [!UICONTROL Player State Name] die de specifieke kenmerkstatus aangeven (bijvoorbeeld &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dit gegevenstype wordt gebruikt om de beginvoorwaarden van de verschillende spelerstatussen vast te leggen en te beschrijven.

![ een diagram van Lijst van het gegevenstype van de Inzameling van het Eind van Staten.](../images/data-types/list-of-states-end-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nee | De naam van de spelerstatus. Opsommend: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; met respectieve betekenissen. |

{style="table-layout:auto"}
