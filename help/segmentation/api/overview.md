---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;API;api;
title: API-handleiding voor segmentatieservice
topic-legacy: guide
description: Met de segmentatieservice-API kunnen ontwikkelaars segmentatiebewerkingen in Adobe Experience Platform programmatisch beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 6133c3127aaf10243d5472540c29125155c99d7b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Handleiding voor Segmenteringsservice-API

[!DNL Adobe Experience Platform Segmentation Service] staat u toe om segmenten te bouwen en publiek te produceren in [!DNL Adobe Experience Platform] van uw [!DNL Real-time Customer Profile] gegevens.

De [!DNL Segmentation Service] API verstrekt veelvoudige eindpunten die u toestaan om uw segmenteringsverrichtingen programmatically te beheren in [!DNL Experience Platform]. Dit overzichtsdocument verstrekt inleiding op hoog niveau aan elk van deze eindpunten, en verbindingen aan hun bijbehorende eindpuntgidsen voor details. Voor het lezen van de individuele eindpuntgidsen, gelieve te verwijzen naar [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, raadpleegt u de [Verwijzing naar API voor segmentatieservice](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Exporttaken

De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt de `/export/jobs` eindpunt om alle uitvoerbanen terug te winnen, een nieuwe uitvoerbaan tot stand te brengen, details van een specifieke uitvoerbaan terug te winnen, of een specifieke uitvoerbaan te annuleren.

Voor meer informatie over het gebruik van dit eindpunt, gelieve te lezen [eindgebruikershandleiding exporttaken](./export-jobs.md).

## Voorvertoningen en ramingen

De voorproeven verstrekken een gepagineerde lijst van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht. U kunt de `/preview` eindpunt om een nieuwe voorproefbaan tot stand te brengen of resultaten van een specifieke voorproefbaan op te zoeken.

Schattingen bieden statistische informatie voor segmentdefinities, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval en de standaardafwijking voor fouten. U kunt de `/estimate` eindpunt om een schatting van een segmentdefinitie te bekijken.

Lees voor meer informatie over het gebruik van deze eindpunten de [handleiding voor voorvertoningen en schattingen van eindpunten](./previews-and-estimates.md).

## Planningen

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt de `/config/schedules` eindpunt om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

Voor meer informatie over het gebruik van dit eindpunt, gelieve te lezen [plannings eindgids](./schedules.md).

## Segmentdefinities

Segmentdefinities definiëren welke profielen deel uitmaken van welke doelsegmenten. U kunt de `/segment/definitions` eindpunt om segmentdefinities te beheren.

Voor meer informatie over het gebruik van dit eindpunt, gelieve te lezen [segmentdefinities, eindhulplijn](./segment-definitions.md).

## Segmenttaken

De banen van het segment verwerken eerder vastgestelde segmentdefinities om een publiekssegment te produceren. U kunt de `/segment/jobs` eindpunt om segmentbanen te beheren.

Voor meer informatie over het gebruik van dit eindpunt, gelieve te lezen [eindgids voor segmenttaken](./segment-jobs.md).

## Segmentzoekopdracht

Het onderzoek van het segment wordt gebruikt om gebieden te zoeken die zich over diverse gegevensbronnen bevinden en hen in bijna real time terug te keren. Als u met segmentzoekopdrachten wilt gaan werken, raadpleegt u de [zoekeindpuntgids](segment-search.md)

## Volgende stappen

Ga als volgt te werk: [!DNL Segmentation Service] API, herzie de verschillende eindpuntgidsen voor gedetailleerde stappen op hoe te om vraag aan de diverse eindpunten van de dienst te maken. Als u meer wilt weten over het werken met segmenten met de opdracht [!DNL Platform] UI, zie [Gebruikershandleiding voor segmentatie](../ui/overview.md).
