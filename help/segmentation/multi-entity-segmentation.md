---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentatie van meerdere entiteiten
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Segmentatie van meerdere entiteiten

De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.

Lees het [segmentatieoverzicht](./home.md)voor meer informatie over de segmentatie van meerdere entiteiten.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het gebruik van segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Klantprofiel](../profile/home.md)in realtime: Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Adobe Experience Platform Segmentation Service](./home.md): Staat u toe om segmenten van het Profiel van de Klant in real time te bouwen.
- [XDM (Experience Data Model)](../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

## XDM-relaties definiëren

Het bepalen van verhoudingen met de structuur van uw schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) is een belangrijk en integraal deel van segmentverwezenlijking.

Dit proces kan of gebruikend de Registratie API van het Schema of de Redacteur van het Schema worden gedaan. Voor een gedetailleerde gids over het gebruiken van API om een verhouding tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verhouding tussen twee schema&#39;s gebruikend API](../xdm/tutorials/relationship-api.md). Voor een gedetailleerde gids bij het gebruiken van de Redacteur van het Schema om een verband tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verband tussen twee schema&#39;s gebruikend de Redacteur](../xdm/tutorials/relationship-ui.md)van het Schema.

## Hoe te gebruiken creeer segmenten die relaties XDM gebruiken

Nadat u uw XDM-relaties hebt gedefinieerd, kunt u de Real-Time Customer Profile API&#39;s gebruiken om een segment te maken.

Dit proces kan of gebruikend Real-time het Profiel van de Klant of de Bouwer van het Segment worden gedaan. Voor een gedetailleerde gids over het gebruiken van API om een segment te bouwen, te lezen gelieve [de zelfstudie over het creëren van een segment gebruikend Real-time het Profiel van de Klant API](./tutorials/create-a-segment.md). Voor een gedetailleerde gids bij het gebruiken van de Bouwer van het Segment om een segment te bouwen, te lezen gelieve [de gebruikersgids](./ui/overview.md)van de Bouwer van het Segment.

## Hoe te om tot segmenten voor multi-entiteitsegmenten te evalueren en toegang te hebben

Na het creëren van een segment, kunt u de segmentresultaten evalueren en tot stand brengen gebruikend Real-time het Profiel van de Klant APIs. Het evalueren van een segment met meerdere entiteiten lijkt sterk op het evalueren van een regulier segment.

Dit proces kan alleen worden uitgevoerd met de Real-Time Customer Profile API. Voor een gedetailleerde gids over het gebruiken van API om segmenten te evalueren en toegang te hebben tot, gelieve [de zelfstudie over het evalueren van en de toegang tot segmenten](./tutorials/evaluate-a-segment.md)te lezen.