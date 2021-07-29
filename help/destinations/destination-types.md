---
keywords: doelen;doel;doeltypen
title: Doeltypen en -categorieën
seo-title: Doeltypen en -categorieën
description: Leer meer over de verschillende typen en categorieën bestemmingen in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Doeltypen en -categorieën

Lees deze pagina om de verschillende typen en categorieën Adobe Experience Platform-bestemmingen te begrijpen.

## Doeltypen

In Adobe Experience Platform maken we onderscheid tussen twee doeltypen: verbindingen en extensies. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](./assets/destination-types/types-of-destinations.png)

## Verbindingen {#connections}

**[!UICONTROL Profile Export]** en  **[!UICONTROL Segment Export]** bestemmingen in Adobe Experience Platform leggen gebeurtenisgegevens vast, combineren deze met andere gegevensbronnen om het  [Real-Time Klantprofiel](../profile/home.md) te vormen, segmentatie toe te passen, en segmenten en gekwalificeerde profielen te exporteren naar bestemmingen.

## Profielexportdoelen

Profielexportdoelen genereren een bestand met profielen en/of kenmerken. Deze bestemmingen gebruiken ruwe gegevens, vaak met e-mailadres als primaire sleutel. De [Amazon S3 wolkenopslagbestemming](./catalog/cloud-storage/amazon-s3.md) is een voorbeeld van bestemming waar u dossiers kunt neerzetten die profieluitvoer bevatten.

## Exportbestemmingen segment

De de uitvoerbestemmingen van het segment verzenden de profielen en de segmenten die zij voor aan bestemmingsplatforms kwalificeerden. Deze bestemmingen gebruiken segment ID of gebruiker IDs. Reclamebestemmingen zoals [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) of [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) zijn voorbeelden van deze soorten doelen.

## Exportdoelen profiel en segment - video-overzicht

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
