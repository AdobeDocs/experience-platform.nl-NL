---
keywords: destinations;destination;destination types
title: Typen bestemmingen en categorieën
seo-title: Typen bestemmingen en categorieën
description: 'In het Platform van de Gegevens van de Klant van Adobe in real time, vangen de de bestemmingen van de Uitvoer van het Profiel/van het Segment gebeurtenisgegevens, combineren het met andere gegevensbronnen, passen segmentatie, en de de uitvoersegmenten en gekwalificeerde profielen op bestemmingen toe. Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen. '
seo-description: In het Platform van de Gegevens van de Klant van Adobe in real time, vangen de de bestemmingen van de Uitvoer van het Profiel/van het Segment gebeurtenisgegevens, combineren het met andere gegevensbronnen, passen segmentatie, en de de uitvoersegmenten en gekwalificeerde profielen op bestemmingen toe. Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen.
translation-type: tm+mt
source-git-commit: b510f715133cc3fed98861f977b3ce9a857a5ced
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Doeltypen en -categorieën

Lees deze pagina om de verschillende types en de categorieën van de bestemmingen van het Platform van de Gegevens van de Klant in real time van Adobe te begrijpen.

## Doeltypen

In het Platform van de Gegevens van de Klant van Adobe in real time, maken wij onderscheid tussen twee bestemmingstypes - verbindingen en uitbreidingen. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Verbindingen {#connections}

**[!UICONTROL De bestemmingen van de Uitvoer]** en van het **[!UICONTROL Segment van het profiel van de Uitvoer]** in het Platform van de Gegevens van de Klant van Adobe Real-time vangen gebeurtenisgegevens, combineren het met andere gegevensbronnen om het [real-time klantenprofiel](/help/profile/home.md)te vormen, segmentatie, en de uitvoersegmenten en gekwalificeerde profielen op bestemmingen toe te passen.

<br> 

#### Profielexportdoelen

Profielexportdoelen genereren een bestand met profielen en/of kenmerken. Deze bestemmingen gebruiken ruwe gegevens, vaak met e-mailadres als primaire sleutel. De [Amazon S3-bestemming voor cloudopslag](/help/rtcdp/destinations/amazon-s3-destination.md) is een voorbeeld van een bestemming waar u bestanden met profielexport kunt neerzetten.

#### Exportbestemmingen segment

De de uitvoerbestemmingen van het segment verzenden de profielen en de segmenten die zij voor aan bestemmingsplatforms kwalificeerden. Deze bestemmingen gebruiken segment ID of gebruiker IDs. Reclamebestemmingen zoals [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) of [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) zijn voorbeelden van dit soort bestemmingen.

#### Exportdoelen profiel en segment - video-overzicht

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensies {#extensions}

Adobe In real time CDP hefboomwerkingen de macht en de flexibiliteit van Experience Platform Launch om de uitbreidingen van de Lancering in de Adobe in real time CDP interface te omvatten.

>[!TIP]
>
>Zie het overzicht [Extensies](/help/rtcdp/destinations/experience-platform-launch-extensions.md)starten voor meer informatie over extensies van Experience Platforms Launch, waaronder gebruiksgevallen en het zoeken van deze extensies in de interface.

Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen. Beschouw extensies als een **type bestemming voor doorsturen** van gebeurtenissen. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Gegineerde personalisatieuitbreiding](/help/rtcdp/destinations/gainsight-extension.md) of de [Bevestiging Stem van de uitbreiding](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)van de Klant.

![Extensies van Experience Platforms Launch vergeleken met andere bestemmingen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Wanneer gebruikt u verbindingen en extensies

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn handig wanneer u een volledig gecentraliseerd klantprofiel of een klantensegment voor activering wilt gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald segment te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker worden aangesloten.

<br> 

## Doelcategorieën

De verbindingen en extensies in de [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Advertising**, **Cloud storage**, **Survey-platforms**, **Email marketing**, enz.), afhankelijk van het marketinggeval dat deze u helpen te maken. Raadpleeg de documentatie bij de [catalogus](/help/rtcdp/destinations/destinations-catalog.md)Doelen voor meer informatie over elk van de categorieën en over de bestemmingen die in elke categorie zijn opgenomen.

![Doelcategorieën](/help/rtcdp/destinations/assets/destination-categories-menu.png)

