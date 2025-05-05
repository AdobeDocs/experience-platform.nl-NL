---
title: Het gegevenstype van de verzameling van hoofddetails
description: Leer over het de gegevenstype van de Gegevens van de Inzameling van het Hoofdstuk van het Gegevensmodel van de Gegevens (XDM).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# [!UICONTROL Chapter Details] Gegevenstype verzameling

[!UICONTROL Chapter Details] Verzameling is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat diverse attributen met betrekking tot hoofdstukken of segmenten binnen media inhoud beschrijft. Met het gegevenstype [!UICONTROL Chapter Details] Verzameling kunt u gegevens vastleggen, zoals de hoofdstuknaam, verschuiving, duur en hoofdstukindex. In velden voor het verzamelen van media worden gegevens vastgelegd en naar andere Adobe-services verzonden voor verdere verwerking.

![ A diagram van het gegevenstype van de Inzameling van de Details van het Hoofdstuk.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=nl-NL#chapter-length) | `length` | integer | Ja | De lengte van het hoofdstuk, in seconden. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=nl-NL#chapter-name) | `friendlyName` | string | Nee | De naam van het hoofdstuk en/of segment. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=nl-NL#chapter-offset) | `offset` | integer | Ja | De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=nl-NL#chapter-position) | `index` | integer | Ja | De positie (index, geheel getal) van het hoofdstuk binnen de inhoud. |

{style="table-layout:auto"}
