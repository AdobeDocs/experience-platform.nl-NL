---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;ingesloten gegevens;streaming;overzicht;streaming opname;latentie;streaming latentie;
solution: Experience Platform
title: Overzicht van streaming inscriptie
topic: overview
description: Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten in real-time naar het Experience Platform te verzenden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Overzicht van het opnemen van streaming

Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten in real-time naar [!DNL Experience Platform] te verzenden.

## Wat kan je doen met streaming opname?

Met Adobe Experience Platform kunt u gecoördineerde, consistente en relevante ervaringen aansturen door een [!DNL Real-time Customer Profile] voor elk van uw individuele klanten te genereren. Streaming opname speelt een belangrijke rol bij het samenstellen van deze profielen door u in staat te stellen [!DNL Profile] gegevens in [!DNL Data Lake] te leveren met zo weinig mogelijk vertraging.

De volgende video is ontworpen om u te helpen bij het begrijpen van streaming opname en geeft een overzicht van de bovenstaande concepten.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stroomprofielrecords en [!DNL ExperienceEvents]

Met streaming opname kunnen gebruikers profielrecords streamen en [!DNL ExperienceEvents] naar [!DNL Platform] in seconden om realtime personalisatie te bevorderen. Alle gegevens die naar streaming opname-API&#39;s worden verzonden, blijven automatisch behouden in [!DNL Data Lake].

Lees de [Create a streaming connection guide](../tutorials/create-streaming-connection.md) voor meer informatie.

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets voor [!DNL Real-time Customer Profile] en [!DNL Identity Service] toelaten.

Voor meer informatie over het toelaten van een dataset voor [!DNL Profile] en [!DNL Identity Service], te lezen [vorm een datasetgids](../../profile/tutorials/dataset-configuration.md).

## Wat is de verwachte latentie voor het stromen van opname op [!DNL Platform]?

| Bestemming | Verwachte vertraging |
| --------- | ---------------- |
| Klantprofiel in realtime | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60=&quot;&quot; minutes=&quot;&quot;> |

## Adobe Experience Platform-extensie

Met de Adobe Experience Platform-extensie kunt u een nieuwe streamingverbinding maken. De extensie [!DNL Experience Platform] biedt acties om bakens te verzenden die zijn opgemaakt in [!DNL Experience Data Model] (XDM) voor realtime invoer naar [!DNL Experience Platform]. Raadpleeg de documentatie [Extensie Experience Platform](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) voor meer informatie.