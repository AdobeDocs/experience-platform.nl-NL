---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentatie van meerdere entiteiten
topic: overview
translation-type: tm+mt
source-git-commit: f44e42a4faa3b10f147dbaf929048054ce0bec42
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Segmentatie van meerdere entiteiten

De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.

Als u meer wilt weten over segmentatie tussen meerdere entiteiten, blijft u de documentatie lezen en kunt u deze leren aanvullen door de onderstaande video te bekijken of het [segmentatieoverzicht](./home.md)te verkennen.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende diensten van het Adobe Experience Platform die betrokken zijn bij het gebruik van segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Klantprofiel](../profile/home.md)in realtime: Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Segmenteringsservice](./home.md)Adobe Experience Platform: Staat u toe om segmenten van het Profiel van de Klant in real time te bouwen.
- [XDM (Experience Data Model)](../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

## XDM-relaties definiëren

Het bepalen van verhoudingen met de structuur van uw schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) is een belangrijk en integraal deel van segmentverwezenlijking.

Dit proces kan of gebruikend de Registratie API van het Schema of de Redacteur van het Schema worden gedaan. Voor een gedetailleerde gids over het gebruiken van API om een verhouding tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verhouding tussen twee schema&#39;s gebruikend API](../xdm/tutorials/relationship-api.md). Voor een gedetailleerde gids bij het gebruiken van de Redacteur van het Schema om een verband tussen twee schema&#39;s te bepalen, te lezen gelieve [het leerprogramma over het bepalen van een verband tussen twee schema&#39;s gebruikend de Redacteur](../xdm/tutorials/relationship-ui.md)van het Schema.

## Hoe te om segmenten tot stand te brengen die relaties gebruiken XDM

Zodra u uw verhoudingen XDM hebt bepaald, kunt u de Dienst API van de Segmentatie gebruiken om een segment te bouwen.

Dit proces kan of gebruikend de Segmentatie API of het gebruikersinterface van de Bouwer van het Segment worden gedaan. Voor een gedetailleerde gids over het gebruiken van API om een segment te bouwen, gelieve te lezen [het leerprogramma over het creëren van een segment gebruikend de Segmentatie API](./tutorials/create-a-segment.md). Voor een gedetailleerde gids bij het gebruiken van de Bouwer van het Segment om een segment te bouwen, te lezen gelieve [de gebruikersgids](./ui/overview.md)van de Bouwer van het Segment.

## Hoe te om tot segmenten voor multi-entiteitsegmenten te evalueren en toegang te hebben

Nadat u een segment hebt gemaakt, kunt u de resultaten van het segment evalueren en openen met de [!DNL Segmentation Service] API. Het evalueren van een segment met meerdere entiteiten lijkt sterk op het evalueren van een regulier segment.

Dit proces kan alleen worden uitgevoerd met de [!DNL Segmentation Service] API. Lees de zelfstudie over het [evalueren en benaderen van segmenten](./tutorials/evaluate-a-segment.md)voor een gedetailleerde handleiding over het gebruik van de API voor het evalueren van en het openen van segmenten.