---
keywords: doelen;doel;doeltypen
title: Doeltypen en -categorieën
seo-title: Doeltypen en -categorieën
description: Leer meer over de verschillende typen en categorieën bestemmingen in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 5a6f14ba65584a6bd61d62c4fb0b46e8f9e8e96d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Doeltypen en -categorieën

Lees deze pagina om de verschillende typen en categorieën Adobe Experience Platform-bestemmingen te begrijpen.

## Doeltypen

In Adobe Experience Platform maken we onderscheid tussen twee doeltypen: verbindingen en extensies. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](./assets/destination-types/types-of-destinations.png)

## Verbindingen {#connections}

**[!UICONTROL Profile Export]** en  **[!UICONTROL Streaming Segment Export]** bestemmingen in Adobe Experience Platform leggen gebeurtenisgegevens vast, combineren deze met andere gegevensbronnen om het  [Real-Time Klantprofiel](../profile/home.md) te vormen, segmentatie toe te passen, en segmenten en gekwalificeerde profielen te exporteren naar bestemmingen.

## Profielexportdoelen

Profielexportdoelen ontvangen onbewerkte gegevens, vaak met e-mailadres als primaire sleutel. Experience Platform ondersteunt momenteel twee typen exportdoelen voor profielen:

* [Streaming profiel exporteren doelen](#streaming-profile-export)
* [Bestandsgebaseerde doelen](#file-based)

### Streaming profiel exporteren doelen {#streaming-profile-export}

Streaming profiel exportdoelen ontvangen segment- en profielgegevens als gegevensstreams voor Experience Platforms. [Amazon ](catalog/cloud-storage/amazon-kinesis.md) Kinesisand  [Azure Event ](catalog/cloud-storage/azure-event-hubs.md) Hubsare voorbeelden van dergelijke bestemmingen.

### Bestandsgebaseerde doelen {#file-based}

Bestandsdoelen ontvangen `.csv` bestanden met profielen en/of kenmerken. [Amazon S3](catalog/cloud-storage/amazon-s3.md) is een voorbeeld van een bestemming waar u bestanden met geëxporteerde profielen kunt neerzetten.

## Streaming segment exportdoelen

De de uitvoerbestemmingen van het segment ontvangen Experience Platform segmentgegevens. Deze bestemmingen gebruiken segment IDs of gebruiker IDs. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md) en  [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) zijn voorbeelden van dergelijke bestemmingen.

## Exporteren van profielen en segmentexportdoelen - video-overzicht

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensies {#extensions}

Platform maakt gebruik van de kracht en flexibiliteit van tagbeheer, zodat u tagextensies kunt configureren in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Zie [overzicht van tagextensies](./catalog/launch-extensions/overview.md) voor gedetailleerde informatie over tagextensies, waaronder gebruiksgevallen en het zoeken van deze extensies in de interface.

Met uitbreidingen worden onbewerkte gebeurtenisgegevens doorgestuurd naar verschillende typen doelen. Beschouw extensies als een **Event Forwarding**-type van bestemming. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Grondige personalisatie-extensie](./catalog/personalization/gainsight.md) of de [Spraak van de klant-extensie bevestigen](./catalog/voice/confirmit-digital-feedback.md).

![Extensies labelen in vergelijking met andere doelen](./assets/common/launch-and-other-destinations.png)

## Wanneer gebruikt u verbindingen en extensies

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn handig wanneer u een volledig gecentraliseerd klantprofiel of een klantensegment voor activering wilt gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald segment te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker worden aangesloten.

## Doelcategorieën

De verbindingen en extensies in de [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Reclame**, **Cloudopslag**, **Beoordelingsplatforms**, **E-mailmarketing**, enz.), afhankelijk van de marketingactie die zij u helpen bereiken. Zie de [documentatie bij de catalogus Doelen](./catalog/overview.md) voor meer informatie over elk van de categorieën en de bestemmingen die in elke categorie zijn opgenomen.

![Doelcategorieën](./assets/destination-types/destination-categories-menu.png)
