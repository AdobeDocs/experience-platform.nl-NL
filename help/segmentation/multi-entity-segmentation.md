---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentatie van meerdere entiteiten
topic: overview
description: De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Segmentatie van meerdere entiteiten

De segmentatie van meerdere entiteiten is de capaciteit om [!DNL Profile] gegevens met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het [!DNL Profile] schema inheems waren.

Als u meer wilt weten over segmentatie tussen meerdere entiteiten, blijft u de documentatie lezen en kunt u deze leren door de onderstaande video te bekijken of het [segmentatieoverzicht](./home.md)te verkennen.

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het gebruik van segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time klantprofiel]](../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Adobe Experience Platform Segmentation Service](./home.md): Staat u toe om segmenten van het Profiel van de Klant in real time te bouwen.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

## XDM-relaties definiëren

Het bepalen van verhoudingen met de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s is een belangrijk en integraal deel van segmentverwezenlijking.

Dit proces kan worden uitgevoerd met de [!DNL Schema Registry] API of de [!DNL Schema Editor]. Voor een gedetailleerde gids over het gebruiken van API om een verhouding tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verhouding tussen twee schema&#39;s gebruikend API](../xdm/tutorials/relationship-api.md). Voor een gedetailleerde gids bij het gebruiken van het [!DNL Schema Editor] om een verband tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verband tussen twee schema&#39;s gebruikend de Redacteur](../xdm/tutorials/relationship-ui.md)van het Schema.

## Hoe te om segmenten tot stand te brengen die relaties gebruiken XDM

Nadat u de XDM-relaties hebt gedefinieerd, kunt u de [!DNL Segmentation Service] API gebruiken om een segment te maken.

Dit proces kan worden uitgevoerd met de [!DNL Segmentation] API of de [!DNL Segment Builder] gebruikersinterface. Voor een gedetailleerde gids over het gebruiken van API om een segment te bouwen, gelieve te lezen [het leerprogramma over het creëren van een segment gebruikend de Segmentatie API](./tutorials/create-a-segment.md). Voor een gedetailleerde gids bij het gebruiken van de Bouwer van het Segment om een segment te bouwen, te lezen gelieve [de gebruikersgids](./ui/overview.md)van de Bouwer van het Segment.

## Hoe te om tot segmenten voor multi-entiteitsegmenten te evalueren en toegang te hebben

Nadat u een segment hebt gemaakt, kunt u de resultaten van het segment evalueren en openen met de [!DNL Segmentation Service] API. Het evalueren van een segment met meerdere entiteiten lijkt sterk op het evalueren van een regulier segment.

Dit proces kan alleen worden uitgevoerd met de [!DNL Segmentation Service] API. Lees de zelfstudie over het [evalueren en benaderen van segmenten](./tutorials/evaluate-a-segment.md)voor een gedetailleerde handleiding over het gebruik van de API voor het evalueren van en het openen van segmenten.