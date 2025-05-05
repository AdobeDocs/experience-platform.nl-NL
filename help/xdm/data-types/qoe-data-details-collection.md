---
title: QoE (Quality of Experience) Gegevenstype Gegevens verzameling
description: Leer over het QoE (Kwaliteit van Ervaring) gegevenstype van de Gegevens van de Inzameling van Gegevens van het Model van de Ervaring van de Gegevens (XDM) gegevenstype.
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# QoE (Kwaliteit van Ervaring) Gegevensinzameling gegevenstype

[!UICONTROL QoE Data Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) dat gedetailleerde metriek biedt met betrekking tot de kwaliteit van de ervaring (QoE) tijdens het afspelen van media. Gebruik het gegevenstype [!UICONTROL QoE Data Details] Verzameling om details vast te leggen, zoals informatie over bitsnelheid, framesnelheden, buffergebeurtenissen, gedropte frames, enzovoort. In velden voor het verzamelen van media worden gegevens vastgelegd en naar andere Adobe-services verzonden voor verdere verwerking. Met dit gegevenstype kunt u de afspeelkwaliteit analyseren, zodat u inzicht hebt in de streamingprestaties, gebruikerservaring en potentiële problemen die tijdens afspeelsessies zijn opgetreden.

+++Selecteren om het gegevenstype QoE-gegevensdetails weer te geven.
![ een diagram van het QoE (Kwaliteit van Ervaring) gegevenstype van de Gegevens van de Inzameling.](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=nl-NL#average-bitrate) | `bitrate` | integer | Nee | De bitsnelheidwaarde (in kbps). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=nl-NL#dropped-frames) | `droppedFrames` | integer | Nee | Het totale aantal frames dat tijdens het afspelen is gedropt. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=nl-NL#frames-per-second) | `framesPerSecond` | integer | Nee | De huidige framesnelheid van de stream (in frames per seconde). |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=nl-NL#time-to-start-1) | `timeToStart` | integer | Nee | Duur (in seconden) tussen het laden van de video en het starten. |

{style="table-layout:auto"}
