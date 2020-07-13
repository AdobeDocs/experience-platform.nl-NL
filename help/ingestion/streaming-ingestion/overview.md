---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van streaming Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Overzicht van het opnemen van streaming

Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en server-side apparaten in real-time naar het Experience Platform te verzenden.

## Wat kan je doen met streaming opname?

Met Adobe Experience Platform kunt u gecoördineerde, consistente en relevante ervaringen aansturen door een realtime klantprofiel voor elk van uw individuele klanten te genereren. Streaming opname speelt een belangrijke rol bij het samenstellen van deze profielen door u in staat te stellen de gegevens van het Profiel met zo weinig mogelijk latentie in het Datameer te leveren.

De volgende video is ontworpen om u te helpen bij het begrijpen van streaming opname en geeft een overzicht van de bovenstaande concepten.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stream-profielrecords en ExperienceEvents

Met streaming opname kunnen gebruikers profielrecords en ExperienceEvents binnen enkele seconden streamen naar een Platform om de realtime personalisatie te bevorderen. Alle gegevens die naar streaming opname-API&#39;s worden verzonden, blijven automatisch behouden in het Data Lake.

Lees de handleiding voor het [maken van streaming verbindingen](../tutorials/create-streaming-connection.md) voor meer informatie.

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets voor het Profiel en de Dienst van de Identiteit van de Klant in real time toelaten.

Voor meer informatie bij het toelaten van een dataset voor de Dienst van het Profiel en van de Identiteit, te lezen gelieve een datasetgids [](../../profile/tutorials/dataset-configuration.md)vormen.

## Wat is de verwachte latentie voor het stromen van opname op Platform?

| Bestemming | Verwachte vertraging |
| --------- | ---------------- |
| Klantprofiel in realtime | &lt; 1 minuut |
| Data Lake | &lt; 60 minuten |

## Adobe Experience Platform extensie

Met de extensie Adobe Experience Platform kunt u een nieuwe streamingverbinding maken. De uitbreiding van het Experience Platform verstrekt acties om bakens te verzenden die in het Model van de Gegevens van de Ervaring (XDM) voor opname in real time aan Experience Platform worden geformatteerd. Raadpleeg de documentatie bij Extensie [Experience Platform](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) voor meer informatie.