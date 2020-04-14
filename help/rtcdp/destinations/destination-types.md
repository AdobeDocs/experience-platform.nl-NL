---
title: Typen bestemmingen en categorieën
seo-title: Typen bestemmingen en categorieën
description: 'In het Platform van de Gegevens van de Klant van Adobe In real time, leggen de Profiel/de bestemmingen van de Uitvoer van het Segment gebeurtenisgegevens vast, combineren het met andere gegevensbronnen, passen segmentatie toe, en voeren segmenten en gekwalificeerde profielen naar bestemmingen uit. Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen. '
seo-description: In het Platform van de Gegevens van de Klant van Adobe In real time, leggen de Profiel/de bestemmingen van de Uitvoer van het Segment gebeurtenisgegevens vast, combineren het met andere gegevensbronnen, passen segmentatie toe, en voeren segmenten en gekwalificeerde profielen naar bestemmingen uit. Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen.
translation-type: tm+mt
source-git-commit: bc3f57d636c363c94555b2a779f5bb98a9eca13f

---


# Doeltypen en -categorieën

Lees deze pagina om inzicht te krijgen in de verschillende typen en categorieën bestemmingen van het Adobe Real-time klantgegevensplatform.

## Doeltypen

In Adobe Real-time Customer Data Platform maken we onderscheid tussen twee doeltypen - verbindingen en extensies. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Verbindingen

**De bestemmingen van de Uitvoer** en van het **Segment van het profiel van de Uitvoer** in het Platform van de Gegevens van de Klant van Adobe Real-time vangen gebeurtenisgegevens, combineren het met andere gegevensbronnen om het [real-time klantenprofiel](/help/profile/home.md)te vormen, segmentatie toe te passen, en segmenten en gekwalificeerde profielen naar bestemmingen uit te voeren.

<br> 

#### Profielexportdoelen

Profielexportdoelen genereren een bestand met profielen en/of kenmerken. Deze bestemmingen gebruiken ruwe gegevens, vaak met e-mailadres als primaire sleutel. De [Amazon S3-bestemming voor cloudopslag](/help/rtcdp/destinations/amazon-s3-destination.md) is een voorbeeld van een bestemming waar u bestanden met profielexport kunt neerzetten.

#### Exportbestemmingen segment

De de uitvoerbestemmingen van het segment verzenden de profielen en de segmenten die zij voor aan bestemmingsplatforms kwalificeerden. Deze bestemmingen gebruiken segment ID of gebruiker IDs. Advertentiebestemmingen zoals [Google Display &amp; Video 360](/help/rtcdp/destinations/google-dv360-destination.md) of [Google Ads](/help/rtcdp/destinations/google-ads-destination.md) zijn voorbeelden van deze soorten doelen.

#### Exportdoelen profiel en segment - video-overzicht

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensies

Adobe Real-time CDP maakt gebruik van de kracht en flexibiliteit van Experience Platform Launch om Launch-extensies op te nemen in de Adobe Real-time CDP-interface.

Start extensies om onbewerkte gebeurtenisgegevens door te sturen naar verschillende typen doelen. Beschouw extensies als een **type bestemming voor doorsturen** van gebeurtenissen. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Gegineerde personalisatieuitbreiding](/help/rtcdp/destinations/gainsight-extension.md) of de [Bevestiging Stem van de uitbreiding](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)van de Klant.

Voor gedetailleerde informatie over de uitbreidingen van de Lancering van het Platform van de Ervaring, zie het overzicht [van de Uitbreidingen van de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Lancering.


![De uitbreidingen van de Lancering van het Platform van de ervaring vergeleken met andere bestemmingen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Wanneer gebruikt u verbindingen en extensies

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn handig wanneer u een volledig gecentraliseerd klantprofiel of een klantensegment voor activering wilt gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald segment te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker worden aangesloten.

<br> 

## Doelcategorieën

De verbindingen en extensies in de [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Advertising**, **Cloud storage**, **Survey-platforms**, **Email marketing**, enz.), afhankelijk van het marketinggeval dat deze u helpen te maken. Raadpleeg de documentatie bij de [catalogus](/help/rtcdp/destinations/destinations-catalog.md)Doelen voor meer informatie over elk van de categorieën en over de bestemmingen die in elke categorie zijn opgenomen.

![Doelcategorieën](/help/rtcdp/destinations/assets/destination-categories-menu.png)

