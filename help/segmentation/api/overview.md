---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van Adobe Experience Platform Segmentation Service
topic: guide
translation-type: tm+mt
source-git-commit: 995fadef9abacf22d0561e0590dfbe172adf0a43
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van Adobe Experience Platform-API [!DNL Segmentation Service]

[!DNL Adobe Experience Platform Segmentation Service] kunt u segmenten maken en publiek genereren [!DNL Adobe Experience Platform] op basis van uw [!DNL Real-time Customer Profile] gegevens.

De [!DNL Segmentation Service] API verstrekt veelvoudige eindpunten die u toestaan om uw segmenteringsverrichtingen in programmatically te beheren [!DNL Experience Platform]. Dit overzichtsdocument verstrekt inleiding op hoog niveau aan elk van deze eindpunten, en verbindingen aan hun bijbehorende eindpuntgidsen voor details. Alvorens de individuele eindpuntgidsen te lezen, gelieve te verwijzen naar de [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, raadpleegt u de API-naslaggids voor [segmentatieservice](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exporttaken

De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. Met het `/export/jobs` eindpunt kunt u alle exporttaken ophalen, een nieuwe exporttaak maken, details van een specifieke exporttaak ophalen of een specifieke exporttaak annuleren.

Voor meer informatie bij het gebruiken van dit eindpunt, gelieve te lezen de gids [van het de eindpunt van](./export-jobs.md)uitvoerbanen.

## Voorvertoningen en ramingen

De voorproeven verstrekken een gepagineerde lijst van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht. U kunt het `/preview` eindpunt gebruiken om een nieuwe voorproefbaan tot stand te brengen of resultaten van een specifieke voorproefbaan op te zoeken.

Schattingen bieden statistische informatie voor segmentdefinities, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval en de standaardafwijking voor fouten. U kunt het `/estimate` eindpunt gebruiken om een schatting van een segmentdefinitie te bekijken.

Lees voor meer informatie over het gebruik van deze eindpunten de handleiding voor [voorvertoningen en schattingen van eindpunten](./previews-and-estimates.md).

## Planningen

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt het `/config/schedules` eindpunt gebruiken om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de gids [van het](./schedules.md)planneneindpunt.

## Segmentdefinities

Segmentdefinities definiëren welke profielen deel uitmaken van welke doelsegmenten. U kunt het `/segment/definitions` eindpunt gebruiken om segmentdefinities te beheren.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de gids [van het](./segment-definitions.md)segmentdefinitieeindpunt.

## Segmenttaken

De banen van het segment verwerken eerder vastgestelde segmentdefinities om een publiekssegment te produceren. U kunt het `/segment/jobs` eindpunt gebruiken om segmentbanen te beheren.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de gids [van het](./segment-jobs.md)segmentbaaneindpunt.

## Segmentzoekopdracht

Het onderzoek van het segment wordt gebruikt om gebieden te zoeken die zich over diverse gegevensbronnen bevinden en hen in bijna real time terug te keren. Beginnen met segmentonderzoek, zie de gids van het [onderzoekseindpunt](segment-search.md)

## Volgende stappen

Om met API te beginnen, herzie de verschillende eindpuntgidsen voor gedetailleerde stappen op hoe te om vraag aan de diverse eindpunten van de dienst te maken. [!DNL Segmentation Service] Meer over het werken met segmenten gebruikend [!DNL Platform] UI leren, zie de de gebruikersgids [van de](../ui/overview.md)Segmentatie.