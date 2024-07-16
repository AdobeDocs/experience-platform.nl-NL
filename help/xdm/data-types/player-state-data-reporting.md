---
title: Gegevenstype van afspeelstatus
description: Leer over het gegevenstype van de Gegevens van de Staat van de Speler die het Model van Gegevens van de Ervaring (XDM) melden.
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# [!UICONTROL Player State Data Reporting] gegevenstype

[!UICONTROL Player State Data Reporting] is een standaard XDM-gegevenstype (Experience Data Model) dat de verschillende statussen en hun voorvallen in een mediaspeler beschrijft. Gebruik het gegevenstype [!UICONTROL Player State Data Reporting] om verschillende spelerstatussen vast te leggen, zoals volledig scherm, dempen, ondertiteling, beeld-in-beeld en status in focus. Voor elke status wordt vastgelegd of de status is ingesteld, hoeveel exemplaren zijn geteld en hoe lang de status actief blijft tijdens het afspelen van media.

![ een diagram van de Gegevens die van de Staat van de Speler gegevenstype melden.](../images/data-types/player-state-data-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | De naam van de spelerstatus. Opsommend: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; met respectieve betekenissen. |
| [!UICONTROL Player State Set] | `isSet` | boolean | Of de spelerstatus op die status is ingesteld. |
| [!UICONTROL Player State Count] | `count` | integer | Het aantal keren dat de spelerstatus op de stream is ingesteld. |
| [!UICONTROL Player State Time] | `time` | integer | De totale duur van die spelerstatus. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
