---
title: API-handleiding voor segmentatieservice
description: Met de segmentatieservice-API kunnen ontwikkelaars segmentatiebewerkingen in Adobe Experience Platform programmatisch beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: af79493c831c401c0bf14e391eb36a8175b4a2dd
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 2%

---

# Handleiding voor Segmenteringsservice-API

Met Adobe Experience Platform [!DNL Segmentation Service] kunt u een publiek maken aan de hand van segmentdefinities of andere bronnen in Adobe Experience Platform op basis van uw [!DNL Real-Time Customer Profile] -gegevens.

De API [!DNL Segmentation Service] biedt meerdere eindpunten waarmee u segmentatiebewerkingen in [!DNL Experience Platform] programmatisch kunt beheren. Dit overzichtsdocument verstrekt inleiding op hoog niveau aan elk van deze eindpunten, en verbindingen aan hun bijbehorende eindpuntgidsen voor details. Alvorens de individuele eindpuntgidsen te lezen, gelieve te verwijzen naar [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Om alle beschikbare eindpunten en verrichtingen te bekijken CRUD, gelieve te verwijzen naar de [&#x200B; Verschuiving van de Dienst API van de Segmentatie &#x200B;](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Doelgroepen

Soorten publiek is een verzameling mensen met een vergelijkbaar gedrag en/of vergelijkbare kenmerken. Deze kunnen worden gegenereerd met behulp van Experience Platform of van externe bronnen. U kunt het `/audiences` eindpunt gebruiken om alle publiek terug te winnen, een nieuw publiek tot stand te brengen, details van een specifiek publiek terug te winnen, een specifiek publiek bij te werken, of een specifiek publiek te schrappen.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; gids van het publiek eindpunt &#x200B;](./audiences.md).

## Exporttaken

De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt het eindpunt `/export/jobs` gebruiken om alle uitvoerbanen terug te winnen, een nieuwe uitvoerbaan tot stand te brengen, details van een specifieke uitvoerbaan terug te winnen, of een specifieke uitvoerbaan te annuleren.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; gids van het de baaneindpunt van de uitvoer &#x200B;](./export-jobs.md).

## Extern publiek

U kunt externe doelgroepen importeren in Experience Platform, de aanmaakstatus van een publiek opvragen, een extern publiek bijwerken, een uitvoering voor het opnemen van het publiek starten, een externe status voor het opnemen van het publiek opvragen, de uitvoering van het opnemen van het publiek in de lijst weergeven en een extern publiek verwijderen door het `/core/ais/external-audiences` -eindpunt te gebruiken.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; externe gids van het doelpubliek &#x200B;](./external-audiences.md).

## Voorvertoningen en ramingen

De voorproeven verstrekken een gepagineerde lijst van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht. U kunt het eindpunt `/preview` gebruiken om een nieuwe voorproefbaan tot stand te brengen of resultaten van een specifieke voorproefbaan op te zoeken.

Schattingen bieden statistische informatie voor segmentdefinities, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval en de standaardafwijking voor fouten. U kunt het `/estimate` eindpunt gebruiken om een schatting van een segmentdefinitie te bekijken.

Voor meer informatie bij het gebruiken van deze eindpunten, te lezen gelieve de [&#x200B; voorproeven en de gids van ramingen eindpunten &#x200B;](./previews-and-estimates.md).

## Planningen

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt het `/config/schedules` eindpunt gebruiken om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; gids van het planningeindpunt &#x200B;](./schedules.md).

## Segmentdefinities

Segmentdefinities definiëren welke profielen deel uitmaken van welk publiek. U kunt het `/segment/definitions` eindpunt gebruiken om segmentdefinities te beheren.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; gids van het segmentdefinitieeindpunt &#x200B;](./segment-definitions.md).

## Segmenttaken

Segmenttaken verwerken eerder gedefinieerde segmentdefinities om een publiek te genereren. U kunt het `/segment/jobs` eindpunt gebruiken om segmentbanen te beheren.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de [&#x200B; gids van het de baaneindpunt van segmenten &#x200B;](./segment-jobs.md).

## Segmentzoekopdracht

Het onderzoek van het segment wordt gebruikt om gebieden te zoeken die zich over diverse gegevensbronnen bevinden en hen in bijna real time terug te keren. Beginnen met segmentonderzoek, zie de [&#x200B; gids van het onderzoekseindpunt &#x200B;](segment-search.md)

## Volgende stappen

Om met [!DNL Segmentation Service] API te beginnen, herzie de verschillende eindpuntgidsen voor gedetailleerde stappen op hoe te om vraag aan de diverse eindpunten van de dienst te maken. Meer leren over het werken met segmenten gebruikend [!DNL Experience Platform] UI, zie de [&#x200B; gebruikersgids van de Segmentatie &#x200B;](../ui/overview.md).
