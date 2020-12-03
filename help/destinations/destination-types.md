---
keywords: destinations;destination;destination types
title: Typen bestemmingen en categorieën
seo-title: Typen bestemmingen en categorieën
description: 'In het Platform van Gegevens van de Klant in real time, vangen de de bestemmingen van de Uitvoer van het Profiel/van het Segment gebeurtenisgegevens, combineren het met andere gegevensbronnen, passen segmentatie toe, en voeren segmenten en gekwalificeerde profielen op bestemmingen uit. Experience Platform Launch-extensies sturen onbewerkte gebeurtenisgegevens door naar verschillende typen doelen. '
seo-description: In het Platform van Gegevens van de Klant in real time, vangen de de bestemmingen van de Uitvoer van het Profiel/van het Segment gebeurtenisgegevens, combineren het met andere gegevensbronnen, passen segmentatie toe, en voeren segmenten en gekwalificeerde profielen op bestemmingen uit. Experience Platform Launch-extensies sturen onbewerkte gebeurtenisgegevens door naar verschillende typen doelen.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Doeltypen en -categorieën

Lees deze pagina om de verschillende types en de categorieën bestemmingen van het Platform van de Gegevens van de Klant in real time te begrijpen.

## Doeltypen

In het Platform van Gegevens van de Klant in real time, maken wij onderscheid tussen twee bestemmingstypes - verbindingen en uitbreidingen. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](./assets/destination-types/types-of-destinations.png)

### Verbindingen {#connections}

**[!UICONTROL De bestemmingen van de Uitvoer]** en van het **[!UICONTROL Segment van het profiel van de Uitvoer]** in het Platform van de Gegevens van de Klant in real time vangen gebeurtenisgegevens, combineren het met andere gegevensbronnen om het [Real-time Profiel](../profile/home.md)van de Klant te vormen, segmentatie toe te passen, en segmenten en gekwalificeerde profielen naar bestemmingen uit te voeren.

#### Profielexportdoelen

Profielexportdoelen genereren een bestand met profielen en/of kenmerken. Deze bestemmingen gebruiken ruwe gegevens, vaak met e-mailadres als primaire sleutel. De [Amazon S3-bestemming voor cloudopslag](./catalog/cloud-storage/amazon-s3.md) is een voorbeeld van een bestemming waar u bestanden met profielexport kunt neerzetten.

#### Exportbestemmingen segment

De de uitvoerbestemmingen van het segment verzenden de profielen en de segmenten die zij voor aan bestemmingsplatforms kwalificeerden. Deze bestemmingen gebruiken segment ID of gebruiker IDs. Reclamebestemmingen zoals [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) of [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) zijn voorbeelden van dit soort bestemmingen.

#### Exportdoelen profiel en segment - video-overzicht

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Extensies {#extensions}

In real time gebruikt CDP de macht en de flexibiliteit van Adobe Experience Platform Launch om de uitbreidingen van de Lancering van het Platform in de interface in real time CDP te omvatten.

>[!TIP]
>
>Zie het overzicht [](./catalog/launch-extensions/overview.md)van Adobe Experience Platform Launch-extensies voor meer informatie over Adobe Experience Platform Launch-extensies, zoals use cases en hoe u deze kunt vinden in de interface.

Platform Start extensies sturen onbewerkte gebeurtenisgegevens door naar verschillende typen doelen. Beschouw extensies als een **type bestemming voor doorsturen** van gebeurtenissen. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Gegineerde personalisatieuitbreiding](./catalog/personalization/gainsight.md) of de [Bevestiging Stem van de uitbreiding](./catalog/voice/confirmit-digital-feedback.md)van de Klant.

![Extensies van Experience Platforms Launch vergeleken met andere bestemmingen](./assets/common/launch-and-other-destinations.png)

### Wanneer gebruikt u verbindingen en extensies

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn handig wanneer u een volledig gecentraliseerd klantprofiel of een klantensegment voor activering wilt gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald segment te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker worden aangesloten.

## Doelcategorieën

De verbindingen en extensies in de [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Advertising**, **Cloud storage**, **Survey-platforms**, **Email marketing**, enz.), afhankelijk van het marketinggeval dat deze u helpen te maken. Raadpleeg de documentatie bij de [catalogus](./catalog/overview.md)Doelen voor meer informatie over elk van de categorieën en over de bestemmingen die in elke categorie zijn opgenomen.

![Doelcategorieën](./assets/destination-types/destination-categories-menu.png)

