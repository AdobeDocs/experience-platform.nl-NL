---
title: QoE (Quality of Experience) Gegevenstype Gegevens
description: Meer informatie over het gegevenstype Data Type Experience Data Model (XDM) van het QoE-gegevenstype (Quality of Experience).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# QoE (Kwaliteit van Ervaring) Gegevendetails Gegevenstype

[!UICONTROL QoE Data Details Information] is een standaard XDM-gegevenstype (Experience Data Model) voor gedetailleerde meetgegevens met betrekking tot de kwaliteit van de ervaring (QoE) tijdens het afspelen van media. Gebruik de [!UICONTROL QoE Data Details Information] gegevenstype voor het vastleggen van gegevens zoals bitsnelheidgegevens, framesnelheden, buffergebeurtenissen, gedropte frames, enzovoort. Met dit gegevenstype kunt u de afspeelkwaliteit analyseren, zodat u inzicht hebt in de streamingprestaties, gebruikerservaring en potentiële problemen die tijdens afspeelsessies zijn opgetreden.

++ + selecteren om het gegevenstype Informatie van de Details van Gegevens QoE te tonen.
![Een diagram van het gegevenstype Informatie van QoE (Quality of Experience)-gegevens.](../images/data-types/qoe-data-details-information.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Average Bitrate Bucket] | `bitrateAverageBucket` | string | De gemiddelde bitsnelheid (in kbps) die in vooraf gedefinieerde emmers met intervallen van 100 kbps wordt gecategoriseerd. |
| [!UICONTROL Bitrate] | `bitrate` | integer | De bitsnelheidwaarde (in kbps). |
| [!UICONTROL Average Bitrate] | `bitrateAverage` | getal | De gemiddelde bitsnelheid (in kbps, geheel getal). Berekend als een gewogen gemiddelde van bitsnelheidwaarden. |
| [!UICONTROL Bitrate Change Impacted Streams] | `hasBitrateChangeImpactedStreams` | boolean | Geeft aan of streams tijdens het afspelen zijn beïnvloed door wijzigingen in bitsnelheid. |
| [!UICONTROL Bitrate Changes] | `bitrateChangeCount` | integer | Het totale aantal bitsnelheden verandert tijdens het afspelen. |
| [!UICONTROL Dropped Frame Impacted Streams] | `hasDroppedFrameImpactedStreams` | boolean | Geeft aan of streams tijdens het afspelen door gedropte frames zijn beïnvloed. |
| [!UICONTROL Dropped Frames] | `droppedFrames` | integer | Het totale aantal frames dat tijdens het afspelen is gedropt. |
| [!UICONTROL Drops Before Starts] | `isDroppedBeforeStart` | boolean | Hiermee geeft u aan of gebruikers de video vóór het starten moeten sluiten, ongeacht advertenties. |
| [!UICONTROL Frames Per Second] | `framesPerSecond` | integer | De huidige framesnelheid van de stream (in frames per seconde). |
| [!UICONTROL Time To Start] | `timeToStart` | integer | Duur (in seconden) tussen het laden van de video en het starten. |
| [!UICONTROL Buffer Impacted Streams] | `hasBufferImpactedStreams` | boolean | Geeft aan of streams zijn beïnvloed door bufferen tijdens het afspelen. |
| [!UICONTROL Buffer Events] | `bufferCount` | integer | Het aantal verschillende bufferstatussen tijdens het afspelen. |
| [!UICONTROL Total Buffer Duration] | `bufferTime` | integer | Totale tijd (in seconden) besteed aan bufferen tijdens het afspelen. |
| [!UICONTROL Error Impacted Streams] | `hasErrorImpactedStreams` | boolean | Geeft aan of er fouten zijn opgetreden tijdens het afspelen van streams. |
| [!UICONTROL Errors] | `errorCount` | integer | Het totale aantal fouten dat tijdens het afspelen is opgetreden. |
| [!UICONTROL Stalling Impacted Streams] | `hasStallImpactedStreams` | boolean | Geeft aan of streams tijdens het afspelen stalling hebben ervaren. |
| [!UICONTROL Stalling Events] | `stallCount` | integer | Het aantal stapelgebeurtenissen tijdens het afspelen. |
| [!UICONTROL Total Stalling Duration] | `stallTime` | integer | De totale tijd (in seconden) dat het afspelen tijdens het afspelen is gestopt. |
| [!UICONTROL Player SDK Error IDs] | `playerSdkErrors` | array van tekenreeksen | Unieke fout-id&#39;s die tijdens het afspelen door de speler-SDK worden gegenereerd. |
| [!UICONTROL External Error IDs] | `externalErrors` | array van tekenreeksen | Unieke fout-id&#39;s van externe bronnen, bijvoorbeeld CDN-fouten. |
| [!UICONTROL Media SDK Error IDs] | `mediaSdkErrors` | array van tekenreeksen | Unieke fout-id&#39;s die door Media SDK worden gegenereerd tijdens het afspelen. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

