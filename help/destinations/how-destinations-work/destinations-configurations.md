---
title: Configureerbare en algemene exportinstellingen in doelen
description: Leer welke de uitvoermontages in bestemmingen configureerbaar op een bestemmingsniveau zijn en die vast zijn en niet kunnen worden uitgegeven.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---


# Configureerbare en algemene exportinstellingen in doelen

Wanneer het denken over het de uitvoergedrag aan de bestemmingen van het Experience Platform, moet u drie afzonderlijke niveaus overwegen waarop de configuraties handelen.

* Op een eerste niveau, zijn sommige montages met betrekking tot het gedrag van de profieluitvoer en configuratiemontages gemeenschappelijk over alle bestemmingen die tot een bestemmingstype behoren. Deze montages verwijzen naar wat een bestemmingsuitvoer teweegbrengt en wat in de uitvoer inbegrepen is en niet door bestemmingsontwikkelaars of gebruikers in real time CDP kan worden uitgegeven.
* Op een tweede niveau, kunnen sommige montages op een bestemmingsniveau door de bestemmingsontwikkelaar worden aangepast wanneer het ontwerpen van bestemmingen die Destination SDK gebruiken.
* Op een derde niveau, zijn er configuratiemontages die de gebruikers in real time CDP in de activeringswerkschema&#39;s kunnen plaatsen.

![Diagram die interplay tussen gemeenschappelijke en configureerbare uitvoermontages voor bestemmingen tonen](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Deze pagina beschrijft of verbindt uit aan alle gemeenschappelijke en configureerbare uitvoermontages voor bestemmingen, op de drie niveaus hierboven geschetst.

## Algemene exportinstellingen voor verschillende doeltypen {#common-settings-across-destination-types}

Het uitvoergedrag van de bestemming is consistent voor alle bestemmingen die tot een type bestemming behoren met betrekking tot *wat een doelexport activeert* en *wat is inbegrepen bij de uitvoer van bestemming*. De uitvoer van de bestemming wordt teweeggebracht door berichten die de bestemmingsdienst van ontvangt [upstream klantenprofielservice in realtime](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Wat in de bestemmingsuitvoer inbegrepen is varieert lichtjes tussen bestemmingstypes. Meer informatie over de [algemene exportgedragspatronen per doeltype](/help/destinations/how-destinations-work/profile-export-behavior.md). Deze montages kunnen niet door bestemmingsontwikkelaars of gebruikers in real time CDP worden uitgegeven.

## Aanpasbare exportinstellingen per doelontwikkelaar {#customizable-settings-by-destination-developers}

Doelontwikkelaars kunnen [Destination SDK](/help/destinations/destination-sdk/overview.md) om aangepaste of productieve (particuliere of openbare) bestemmingen te maken. Destination SDK biedt ontwikkelaars grote flexibiliteit om doelen te configureren op basis van de downstreammogelijkheden van hun API-eindpunten en systemen voor het ontvangen van bestanden. Gebaseerd op de stroomafwaartse mogelijkheden, hebben de bestemmingsontwikkelaars de volgende configuratieopties beschikbaar wanneer het vormen van een bestemming gebruikend Destination SDK:

* Bepaal welke kenmerken en identiteiten uit het Experience Platform naar het doel kunnen worden geëxporteerd. Bepaal ook welke identiteiten door hun bestemmingen voor een succesvolle gegevensuitvoer worden vereist.
* Stel een samenvoegingsbeleid in dat bepaalt hoe lang Experience Platform moet wachten wanneer HTTP-berichten worden samengevoegd die naar API-integratie moeten worden verzonden. Doelontwikkelaars kunnen verschillende aggregatietypen configureren om te bepalen hoeveel profielen moeten worden opgenomen in uitgaande HTTP-berichten en hoe lang het Experience Platform moet wachten tot het HTTP-bericht wordt verzonden. Meer informatie over de [configuratieopties voor samenvoegingsbeleid](/help/destinations/destination-sdk/destination-configuration.md#aggregation) beschikbaar aan bestemmingsontwikkelaars in de documentatie van de Destination SDK.
* Bepaal als de het berichtuitvoer van HTTP profielen zou moeten omvatten die voor segmenten kwalificeren, die uit segmenten, of allebei worden verwijderd.
* Bepaal welke bestandsnaam en opmaakconfiguraties bij het exporteren van bestanden beschikbaar moeten zijn voor gebruikers.

## Instellingen op een gegevensstroomniveau dat door gebruikers kan worden aangepast {#settings-on-dataflow-level}

Naast de niet-bewerkbare instellingen die afhankelijk zijn van het doeltype en de instellingen die door de doelontwikkelaar zijn geconfigureerd, zijn er bepaalde exportinstellingen die gebruikers kunnen configureren in de activeringsworkflow. Deze instellingen hebben betrekking op het exportschema voor een bepaalde gegevensstroom naar een bestemming, de kenmerken en identiteitsvelden die in een gegevensstroom moeten worden geëxporteerd of de opmaakopties voor geëxporteerde bestanden.

De montages die aan gebruikers wanneer het verbinden met een bestemming beschikbaar zijn hangen van af hoe de bestemming door de bestemmingsontwikkelaar werd gevormd en welke montages zij ter beschikking stelden aan gebruikers.

Bijvoorbeeld: [streaming doelen](/help/destinations/destination-types.md#streaming-destinations), kan een bestemmingsontwikkelaar vormen welke identiteiten hun bestemming goedkeurt en slechts die identiteiten zullen aan de gebruiker binnen worden getoond [toewijzingsstap van de activeringsworkflow](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), zoals hieronder weergegeven:

![Schermopname van de identiteitsselectie voor doelveld in de toewijzingsstap van de activeringsworkflow. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Evenzo geldt voor [bestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based)kan de doelontwikkelaar bepalen welke [bestandsnaam toevoegen, opties](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) zij ter beschikking willen stellen voor hun bestemming, of [opties voor bestandsindeling](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) ze willen het bestand beschikbaar maken en de gebruiker kan alleen uit de volgende opties kiezen, zoals hieronder wordt getoond:

![Schermopname van de optie voor bestandsindeling wanneer verbinding wordt gemaakt met een op een bestand gebaseerd doel.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![De opname van het scherm van filename voegt optie in de het plannen stap van het activeringswerkschema toe. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Lees meer over de verschillende opties en stappen in de activeringsworkflow:

* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activeer publieksgegevens aan ondernemingsbestemmingen](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Bestanden op aanvraag exporteren naar batchbestemmingen](/help/destinations/ui/export-file-now.md)
* [(bèta) Gegevenssets exporteren naar cloudopslagbestemmingen](/help/destinations/ui/export-datasets.md)

## Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu welke de uitvoermontages voor bestemmingen over bestemmingstypes gemeenschappelijk zijn, die op een individueel bestemmingsniveau door ontwikkelaars kunnen worden gevormd, en welke montages door gebruikers in het activeringswerkschema kunnen worden uitgegeven.

Vervolgens kunt u meer gedetailleerde informatie lezen over de [algemene exportgedragspatronen per doeltype](/help/destinations/how-destinations-work/profile-export-behavior.md).

Voor doelontwikkelaars kunt u [Aan de slag](/help/destinations/destination-sdk/getting-started.md) met Destination SDK. Voor gebruikers die gegevens willen activeren, kunt u alle beschikbare doelen uitchecken in het dialoogvenster [catalogus](/help/destinations/catalog/overview.md).