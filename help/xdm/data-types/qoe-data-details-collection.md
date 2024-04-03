---
title: QoE (Quality of Experience) Gegevenstype Gegevens verzameling
description: Leer over het QoE (Kwaliteit van Ervaring) gegevenstype van de Gegevens van de Inzameling van Gegevens van het Model van de Ervaring van de Gegevens (XDM) gegevenstype.
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# QoE (Kwaliteit van Ervaring) Gegevensinzameling gegevenstype

[!UICONTROL QoE Data Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) dat gedetailleerde meetgegevens biedt met betrekking tot de kwaliteit van de ervaring (QoE) tijdens het afspelen van media. Gebruik de [!UICONTROL QoE Data Details] Het gegevenstype van de inzameling om details zoals bitsnelheidsinformatie, kadertarieven, het als buffer optreden voor gebeurtenissen, gelaten vallen kaders, etc. te vangen. In velden voor het verzamelen van media worden gegevens vastgelegd en naar andere Adobe-services verzonden voor verdere verwerking. Met dit gegevenstype kunt u de afspeelkwaliteit analyseren, zodat u inzicht hebt in de streamingprestaties, gebruikerservaring en potentiële problemen die tijdens afspeelsessies zijn opgetreden.

+++Selecteren om het gegevenstype QoE-gegevensdetails weer te geven.
![Een diagram van het gegevenstype Gegevensverzameling QoE (Quality of Experience).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | integer | Nee | De bitsnelheidwaarde (in kbps). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | integer | Nee | Het totale aantal frames dat tijdens het afspelen is gedropt. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | integer | Nee | De huidige framesnelheid van de stream (in frames per seconde). |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | integer | Nee | Duur (in seconden) tussen het laden van de video en het starten. |

{style="table-layout:auto"}
