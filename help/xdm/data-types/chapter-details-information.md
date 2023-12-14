---
title: Hoofdstuk Details Gegevenstype
description: Leer over het de gegevenstype van de Gegevens van het Hoofdstuk van de Ervaring van Gegevens Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# [!UICONTROL Chapter Details Information] gegevenstype

[!UICONTROL Chapter Details Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat diverse attributen met betrekking tot hoofdstukken of segmenten binnen media inhoud beschrijft. Gebruik de [!UICONTROL Chapter Details Information] het gegevenstype om details zoals hoofdstuknaam, duur, positie, identiteitskaart, playbackstatus (begonnen/voltooid), en de tijd te vangen besteed aan elk hoofdstuk.

![Een diagram van het gegevenstype Informatie van hoofdstukdetails.](../images/data-types/chapter-details-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Chapter Name] | `friendlyName` | string | De naam van het hoofdstuk en/of segment. |
| [!UICONTROL Chapter Length Or Duration] | `length` | integer | **Vereist** De lengte van het hoofdstuk, in seconden. |
| [!UICONTROL Chapter Offset] | `offset` | integer | **Vereist** De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin. |
| [!UICONTROL Chapter Position] | `index` | integer | **Vereist** De positie (index, geheel getal) van het hoofdstuk binnen de inhoud. |
| [!UICONTROL Chapter ID] | `ID` | string | De automatisch gegenereerde id van het hoofdstuk. |
| [!UICONTROL Chapter Started] | `isStarted` | boolean | Of het hoofdstuk is begonnen. |
| [!UICONTROL Chapter Completed] | `isCompleted` | boolean | Of het hoofdstuk is voltooid. |
| [!UICONTROL Chapter Time Played] | `timePlayed` | integer | De tijd die aan het hoofdstuk wordt doorgebracht, in seconden. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
