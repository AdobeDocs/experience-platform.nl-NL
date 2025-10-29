---
title: Configureerbare en algemene exportinstellingen in doelen
description: Leer welke de uitvoermontages in bestemmingen configureerbaar op een bestemmingsniveau zijn en die vast zijn en niet kunnen worden uitgegeven.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Configureerbare en algemene exportinstellingen in doelen

Wanneer het denken over het uitvoergedrag aan de bestemmingen van Experience Platform, moet u drie afzonderlijke niveaus overwegen waarop de configuraties handelen.

* Op een eerste niveau, zijn sommige montages met betrekking tot het gedrag van de profieluitvoer en configuratiemontages gemeenschappelijk over alle bestemmingen die tot een bestemmingstype behoren. Deze instellingen verwijzen naar wat een doelexport activeert en naar wat in een exportbewerking is opgenomen en niet kan worden bewerkt door bestemmingsontwikkelaars of Real-Time CDP-gebruikers.
* Op een tweede niveau, kunnen sommige montages op een bestemmingsniveau door de bestemmingsontwikkelaar worden aangepast wanneer het ontwerpen van bestemmingen die Destination SDK gebruiken.
* Op een derde niveau zijn er configuratie-instellingen die Real-Time CDP-gebruikers kunnen instellen in de activeringsworkflows.

![&#x200B; Diagram die interplay tussen gemeenschappelijke en configureerbare de uitvoermontages voor bestemmingen &#x200B;](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png) tonen

Deze pagina beschrijft of verbindt uit aan alle gemeenschappelijke en configureerbare uitvoermontages voor bestemmingen, op de drie niveaus hierboven geschetst.

## Algemene exportinstellingen voor verschillende doeltypen {#common-settings-across-destination-types}

Het de uitvoergedrag van de bestemming is verenigbaar over bestemmingen die tot een bestemmingstype met betrekking tot *behoren wat een bestemmingsuitvoer* teweegbrengt en *wat in de bestemmingsuitvoer* inbegrepen is. De uitvoer van de bestemming wordt teweeggebracht door berichten die de bestemmingsdienst van de [&#x200B; stroomopwaartse dienst van het Profiel van de Klant in real time &#x200B;](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram) ontvangt.

Wat in de bestemmingsuitvoer inbegrepen is varieert lichtjes tussen bestemmingstypes. Lees meer over de [&#x200B; gemeenschappelijke patronen van het uitvoergedrag per bestemmingstype &#x200B;](/help/destinations/how-destinations-work/profile-export-behavior.md). Deze instellingen kunnen niet worden bewerkt door bestemmingsontwikkelaars of Real-Time CDP-gebruikers.

## Aanpasbare exportinstellingen per doelontwikkelaar {#customizable-settings-by-destination-developers}

De ontwikkelaars van de bestemming kunnen [&#x200B; Destination SDK &#x200B;](/help/destinations/destination-sdk/overview.md) gebruiken om douane of geproduceerde (privé of openbare) bestemmingen tot stand te brengen. Destination SDK biedt ontwikkelaars grote flexibiliteit om doelen te configureren op basis van de downstreammogelijkheden van hun API-eindpunten en systemen voor het ontvangen van bestanden. Gebaseerd op de stroomafwaartse mogelijkheden, hebben de bestemmingsontwikkelaars de volgende configuratieopties beschikbaar wanneer het vormen van een bestemming gebruikend Destination SDK:

* Bepaal welke kenmerken en identiteiten uit Experience Platform naar de bestemming kunnen worden geëxporteerd. Bepaal ook welke identiteiten door hun bestemmingen voor een succesvolle gegevensuitvoer worden vereist.
* Stel een samenvoegingsbeleid in dat bepaalt hoe lang Experience Platform moet wachten wanneer HTTP-berichten worden samengevoegd die naar API-integratie moeten worden verzonden. Doelontwikkelaars kunnen verschillende aggregatietypen configureren om te bepalen hoeveel profielen moeten worden opgenomen in uitgaande HTTP-berichten en hoe lang Experience Platform moet wachten tot het HTTP-bericht wordt verzonden. Vind uitgebreide informatie over de [&#x200B; configuratieopties van het samenvoegingsbeleid &#x200B;](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) beschikbaar aan bestemmingsontwikkelaars in de documentatie van Destination SDK.
* Bepaal als de het berichtuitvoer van HTTP profielen zou moeten omvatten die voor segmenten kwalificeren, die uit segmenten, of allebei worden verwijderd.
* Bepaal welke bestandsnaam en opmaakconfiguraties bij het exporteren van bestanden beschikbaar moeten zijn voor gebruikers.

## Instellingen op een gegevensstroomniveau dat door gebruikers kan worden aangepast {#settings-on-dataflow-level}

Naast de niet-bewerkbare instellingen die afhankelijk zijn van het doeltype en de instellingen die door de doelontwikkelaar zijn geconfigureerd, zijn er bepaalde exportinstellingen die gebruikers kunnen configureren in de activeringsworkflow. Deze instellingen hebben betrekking op het exportschema voor een bepaalde gegevensstroom naar een bestemming, de kenmerken en identiteitsvelden die in een gegevensstroom moeten worden geëxporteerd of de opmaakopties voor geëxporteerde bestanden.

De montages die aan gebruikers wanneer het verbinden met een bestemming beschikbaar zijn hangen van af hoe de bestemming door de bestemmingsontwikkelaar werd gevormd en welke montages zij ter beschikking stelden aan gebruikers.

Bijvoorbeeld, voor [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations), kan een bestemmingsontwikkelaar vormen welke identiteiten hun bestemming goedkeurt en slechts die identiteiten zullen aan de gebruiker in [&#x200B; kaartstap van het activeringswerkschema &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), zoals hieronder getoond worden getoond:

![&#x200B; opname van het Scherm van de identiteitsselectie voor doelgebied in de afbeeldingsstap van het activeringswerkschema.](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Op dezelfde manier voor [&#x200B; op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based), kan de bestemmingsontwikkelaar bepalen welke [&#x200B; filename opties &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) toevoegt zij voor hun bestemming beschikbaar willen maken, of welke [&#x200B; dossier het formatteren opties &#x200B;](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) zij beschikbaar willen maken, en de gebruiker van deze opties slechts, zoals hieronder getoond zal kunnen selecteren:

![&#x200B; opname van het Scherm van de dossier het formatteren optie wanneer het verbinden met een op dossier-gebaseerde bestemming.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![&#x200B; de opname van het Scherm van filename voegt optie in de het plannen stap van het activeringswerkschema toe.](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Meer informatie over de verschillende opties en stappen in de activeringsworkflow vindt u:

* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activeer publieksgegevens aan ondernemingsbestemmingen](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Bestanden op aanvraag exporteren naar batchbestemmingen](/help/destinations/ui/export-file-now.md)
* [Gegevenssets exporteren naar cloudopslagbestemmingen](/help/destinations/ui/export-datasets.md)

## Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu welke de uitvoermontages voor bestemmingen over bestemmingstypes gemeenschappelijk zijn, die op een individueel bestemmingsniveau door ontwikkelaars kunnen worden gevormd, en welke montages door gebruikers in het activeringswerkschema kunnen worden uitgegeven.

Daarna, kunt u meer gedetailleerde informatie over [&#x200B; gemeenschappelijke de patronen van het uitvoergedrag per bestemmingstype &#x200B;](/help/destinations/how-destinations-work/profile-export-behavior.md) lezen.

Voor bestemmingsontwikkelaars, kunt u [&#x200B; begonnen worden &#x200B;](/help/destinations/destination-sdk/getting-started.md) met Destination SDK. Voor gebruikers die gegevens proberen te activeren, kunt u alle beschikbare bestemmingen in de [&#x200B; catalogus &#x200B;](/help/destinations/catalog/overview.md) uitchecken.
