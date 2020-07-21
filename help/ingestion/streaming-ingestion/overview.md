---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van streaming Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Overzicht van het opnemen van streaming

Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten naar [!DNL Experience Platform] realtime te verzenden.

## Wat kan je doen met streaming opname?

Adobe Experience Platform laat u toe om gecoördineerde, verenigbare, en relevante ervaringen te drijven door een [!DNL Real-time Customer Profile] voor elk van uw individuele klanten te produceren. Streaming opname speelt een belangrijke rol bij het samenstellen van deze profielen door u in staat te stellen [!DNL Profile] gegevens met zo weinig mogelijk latentie in de [!DNL Data Lake] omgeving te leveren.

De volgende video is ontworpen om u te helpen bij het begrijpen van streaming opname en geeft een overzicht van de bovenstaande concepten.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stroomprofielrecords en [!DNL ExperienceEvents]

Met het stromen opname, kunnen de gebruikers profielverslagen en [!DNL ExperienceEvents] aan [!DNL Platform] in seconden stromen helpen verpersoonlijking in real time drijven. Alle gegevens die naar gestreamde opname-API&#39;s worden verzonden, blijven automatisch in de [!DNL Data Lake]sjabloon behouden.

Lees de handleiding voor het [maken van streaming verbindingen](../tutorials/create-streaming-connection.md) voor meer informatie.

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets voor [!DNL Real-time Customer Profile] en [!DNL Identity Service].

Voor meer informatie bij het toelaten van een dataset voor [!DNL Profile] en [!DNL Identity Service], te lezen gelieve een [datasetgids](../../profile/tutorials/dataset-configuration.md)vormen.

## Wat is de verwachte latentie voor het stromen van opname op [!DNL Platform]?

| Bestemming | Verwachte vertraging |
| --------- | ---------------- |
| Klantprofiel in realtime | &lt; 1 minuut |
| Data Lake | &lt; 60 minuten |

## Adobe Experience Platform extensie

Met de extensie Adobe Experience Platform kunt u een nieuwe streamingverbinding maken. De [!DNL Experience Platform] extensie biedt acties voor het verzenden van bakens die zijn opgemaakt in [!DNL Experience Data Model] (XDM) voor realtime invoer naar [!DNL Experience Platform]. Raadpleeg de documentatie bij Extensie [Experience Platform](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) voor meer informatie.