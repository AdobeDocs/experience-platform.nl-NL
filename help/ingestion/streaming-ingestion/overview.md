---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van Streaming-inname Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# Overzicht van het opnemen van streaming

Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten naar Experience Platform in real-time te verzenden.

## Wat kan je doen met streaming opname?

Met het Adobe Experience Platform kunt u een gecoördineerde, consistente en relevante ervaring opdoen door een Real-time klantprofiel te genereren voor elk van uw individuele klanten. Streaming opname speelt een belangrijke rol bij het samenstellen van deze profielen door u in staat te stellen de gegevens van het Profiel met zo weinig mogelijk latentie in het Datameer te leveren.

### Stream-profielrecords en ExperienceEvents

Met streaming opname kunnen gebruikers profielrecords en ExperienceEvents binnen enkele seconden streamen naar Platform om realtime personalisatie te bevorderen. Alle gegevens die naar streaming opname-API&#39;s worden verzonden, blijven automatisch behouden in het Data Lake.

Lees de handleiding voor het [maken van streaming verbindingen](../tutorials/create-streaming-connection.md) voor meer informatie.

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets voor het Profiel en de Dienst van de Identiteit van de Klant in real time toelaten.

Voor meer informatie bij het toelaten van een dataset voor de Dienst van het Profiel en van de Identiteit, te lezen gelieve een datasetgids [](../../profile/tutorials/dataset-configuration.md)vormen.

## Wat is de verwachte latentie voor het stromen opname op Platform?

| Doel | Verwachte vertraging |
| --------- | ---------------- |
| Klantprofiel in realtime | &lt; 1 minuut |
| Data Lake | &lt; 60 minuten |

## Adobe Experience Platform-extensie

Met de extensie Adobe Experience Platform kunt u een nieuwe streamingverbinding maken. De uitbreiding van het Platform van de Ervaring verstrekt acties om bakens te verzenden die in het Model van de Gegevens van de Ervaring (XDM) voor opname in real time aan het Platform van de Ervaring worden geformatteerd. Raadpleeg de documentatie bij Extensie [](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) Experience Platform voor meer informatie.