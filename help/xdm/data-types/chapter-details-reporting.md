---
title: Hoofdstuk - Gegevens die Gegevenstype rapporteren
description: Leer over het het gegevenstype van de Gegevens van de Rapportering van de Ervaring van het Hoofdstuk Model (XDM).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL Chapter Details] Gegevenstype rapporteren

[!UICONTROL Chapter Details] De rapportering is een standaard het gegevenstype van de Gegevens van de Ervaring Model (XDM) dat diverse attributen met betrekking tot hoofdstukken of segmenten binnen media inhoud beschrijft. Gebruik de [!UICONTROL Chapter Details] Gegevenstype rapporteren om details vast te leggen, zoals hoofdstuknaam, duur, positie, id, afspeelstatus (gestart/voltooid) en de tijd die aan elk hoofdstuk is besteed. Media-rapportvelden worden door Adobe-services gebruikt voor het analyseren van de velden Media Collection die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd.

![Een diagram van het gegevenstype Rapportage van hoofdstukdetails.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | boolean | Of het hoofdstuk is voltooid of niet. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | string | De automatisch gegenereerde id van het hoofdstuk. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | integer | De lengte van het hoofdstuk, in seconden. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | De naam van het hoofdstuk en/of segment. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | integer | De verschuiving van het hoofdstuk binnen de inhoud (in seconden) vanaf het begin. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | integer | De positie (index, geheel getal) van het hoofdstuk binnen de inhoud. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | boolean | Of het hoofdstuk is begonnen of niet. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | integer | De tijd die aan het hoofdstuk wordt doorgebracht, in seconden. |
