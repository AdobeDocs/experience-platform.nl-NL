---
title: getMediaAnalyticsTracker
description: Leer hoe u een Media Analytics Tracker-object maakt en dit gebruikt om mediagebeurtenissen bij te houden.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# `getMediaAnalyticsTracker`

Met deze Web SDK-opdracht haalt u een Media Analytics Tracker op. U kunt dit bevel gebruiken om een objecten instantie tot stand te brengen en dan, gebruikend zelfde APIs zoals die door de [&#x200B; bibliotheek JS van Media &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) worden verstrekt, de gebeurtenissen van de spoormedia.

De opdracht `getMediaAnalyticsTracker` retourneert de API voor oude media-analyse.

| Naam van methode | Beschrijving | Syntaxis |
|---|---|---|
| `getInstance` | Maakt een instantie van media om de afspeelsessie bij te houden. | `Media.getInstance()` |
| `createMediaObject` | Maakt een object met mediagegevens. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Maakt een object dat pagina-informatie bevat. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Maakt een object dat advertentiegegevens bevat. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Maakt een object met hoofdstukinformatie. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Maakt een object dat statusinformatie bevat. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createStateObject(name)` |
| `createQoEObject` | Maakt een object dat QoE-informatie bevat. Retourneert een leeg object als er ongeldige parameters worden doorgegeven. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Instantiemethoden

| Naam van methode | Beschrijving | Syntaxis |
|---|---|---|
| `trackSessionStart` | Houd de intentie bij om het afspelen te starten. Hiermee wordt een volgende sessie gestart op de instantie van de mediatracker. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Media bijhouden of hervatten na een vorige pauze. | `trackerInstance.trackPlay()` |
| `trackPause` | Media bijhouden gepauzeerd. | `trackerInstance.trackPause()` |
| `trackComplete` | Media bijhouden voltooid. Roep deze methode alleen aan wanneer de media volledig zijn weergegeven. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Het einde van een weergavesessie bijhouden. Roep deze methode aan, zelfs als de gebruiker de media niet aan voltooiing bekijkt. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Een fout bijhouden die is opgetreden tijdens het afspelen van media. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Een aangepaste gebeurtenis volgen. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | De positie van de afspeelkop bijwerken. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Werk de kwaliteit van de ervaring bij. | `trackerInstance.updateQoEObject(qoe)` |

## Constanten

| Naam van constante | Beschrijving | Waarde |
|---|---|---|
| `MediaType` | Mediatype | `Video`, `Audio` |
| `StreamType` | Het type Stream | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Hiermee worden de standaardmetagegevenssleutels voor videostreams gedefinieerd | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Hiermee worden de standaardmetagegevenssleutels voor audiostreams gedefinieerd. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Hiermee definieert u de standaard metagegevenstoetsen voor advertenties. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Hiermee wordt het type van een gebeurtenis tracking gedefinieerd. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Hiermee definieert u standaardwaarden voor het bijhouden van de spelerstatus. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |

## Media Analytics-tracering ophalen met de webtagextensie SDK

Het equivalent van deze opdracht voor de SDK-tag Web is de [**[!UICONTROL Get Media Analytics tracker]**](/help/tags/extensions/client/web-sdk/actions/get-media-analytics-tracker.md) -handeling.
