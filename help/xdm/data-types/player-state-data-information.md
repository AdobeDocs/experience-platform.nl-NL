---
title: Gegevenstype van afspeelstatus
description: Leer over het gegevenstype van de de Ervaring van de Gegevens van de Staat van de Speler Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# [!UICONTROL Player State Data Information] gegevenstype

[!UICONTROL Player State Data Information] is een standaard XDM-gegevenstype (Experience Data Model) waarmee de verschillende statussen en hun voorvallen in een mediaspeler worden beschreven. Gebruik de [!UICONTROL Player State Data Information] gegevenstype voor het vastleggen van verschillende spelerstatussen, zoals volledig scherm, dempen, ondertiteling, beeld-in-beeld en status in focus. Voor elke status wordt vastgelegd of de status is ingesteld, hoeveel exemplaren zijn geteld en hoe lang de status actief blijft tijdens het afspelen van media.

![Een diagram van het gegevenstype Gegevens van de Staat van de Speler.](../images/data-types/player-state-data-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | De naam van de spelerstatus. Opsommend: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; met respectieve betekenissen. |
| [!UICONTROL Player State Set] | `isSet` | boolean | Of de spelerstatus op die status is ingesteld. |
| [!UICONTROL Player State Count] | `count` | integer | Het aantal keren dat de spelerstatus op de stream is ingesteld. |
| [!UICONTROL Player State Time] | `time` | integer | De totale duur van die spelerstatus. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
