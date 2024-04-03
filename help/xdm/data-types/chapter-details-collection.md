---
title: Het gegevenstype van de verzameling van hoofddetails
description: Leer over het de gegevenstype van de Gegevens van de Inzameling van het Hoofdstuk van het Gegevensmodel van de Gegevens (XDM).
source-git-commit: c6108bb692c80c79e115ac7b1488d95a7039ffcf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 2%

---

# [!UICONTROL Chapter Details] Gegevenstype verzameling

[!UICONTROL Chapter Details] De inzameling is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat diverse attributen met betrekking tot hoofdstukken of segmenten binnen media inhoud beschrijft. Gebruik de [!UICONTROL Chapter Details] Het gegevenstype van de inzameling om details zoals hoofdstuknaam, compensatie, duur, en de hoofdstukindex te vangen. In velden voor het verzamelen van media worden gegevens vastgelegd en naar andere Adobe-services verzonden voor verdere verwerking.

![Een diagram van het gegevenstype van de Verzameling van de Details van het Hoofdstuk.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | integer | Ja | De lengte van het hoofdstuk, in seconden. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | Nee | De naam van het hoofdstuk en/of segment. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | integer | Ja | De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | integer | Ja | De positie (index, geheel getal) van het hoofdstuk binnen de inhoud. |

{style="table-layout:auto"}
