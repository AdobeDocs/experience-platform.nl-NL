---
keywords: doelen;doel;doeltypen
title: Doeltypen en -categorieën
description: Leer meer over de verschillende typen en categorieën bestemmingen in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Doeltypen en -categorieën

Lees deze pagina om de verschillende typen en categorieën Adobe Experience Platform-bestemmingen te begrijpen.

## Doeltypen {#destination-types}

In Adobe Experience Platform maken we onderscheid tussen twee doeltypen: verbindingen en extensies. Er zijn twee soorten verbindingsbestemmingen, de bestemmingen van de Uitvoer van het Profiel en de bestemmingen van de Uitvoer van het Segment.

![Soorten bestemmingen](./assets/destination-types/types-of-destinations.png)

## Verbindingen {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Segment Export]**, en **[!DNL Edge Personalization]** doelen in Adobe Experience Platform leggen gebeurtenisgegevens vast, combineren deze met andere gegevensbronnen om de [Klantprofiel in realtime](../profile/home.md)segmentatie toepassen en segmenten en gekwalificeerde profielen exporteren naar bestemmingen.

## Profielexportdoelen {#profile-export}

Profielexportdoelen ontvangen onbewerkte gegevens, vaak met e-mailadres als primaire sleutel. Experience Platform ondersteunt momenteel twee typen exportdoelen voor profielen:

* [Streaming profiel exportdoelen (ondernemingsdoelen)](#streaming-profile-export)
* [Batchbestemmingen (op basis van bestanden)](#file-based)

### Streaming profiel exportdoelen (ondernemingsdoelen) {#streaming-profile-export}

>[!IMPORTANT]
>
>De bestemmingen van de onderneming, of het stromen profiel de uitvoerbestemmingen, zijn beschikbaar aan [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) alleen aan klanten.

Gebruik gegevensconnectors voor bedrijfsdoelgegevens om Adobe Real-time Customer Data Platform-profielen in bijna realtime te leveren aan interne systemen of aan andere systemen van derden voor gegevenssynchronisatie, analyse en verdere gebruiksscenario&#39;s voor profielverrijking.

Deze doelen ontvangen segment- en profielgegevens als gegevensstromen van Experience Platforms.

De bestemmingen van de onderneming omvatten:

* [HTTP API-bestemming](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Batchbestemmingen (op basis van bestanden) {#file-based}

Bestandsgebaseerde doelen ontvangen `.csv` bestanden met profielen en/of kenmerken. [Amazon S3](catalog/cloud-storage/amazon-s3.md) Dit is een voorbeeld van een bestemming waar u bestanden kunt exporteren die profielen bevatten.

## Streaming segment exportdoelen {#streaming-destinations}

De de uitvoerbestemmingen van het segment ontvangen Experience Platform segmentgegevens. Deze bestemmingen gebruiken segment IDs of gebruiker IDs. Reclame en sociale bestemmingen zoals [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), of [Facebook](catalog/social/facebook.md) zijn voorbeelden van dergelijke bestemmingen .

## Edge-verpersoonlijkingsdoelen {#edge-personalization-destinations}

De het verpersoonlijkingsbestemmingen van de rand in Experience Platform omvatten [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) en de [Aangepast aanpassingsdoel](/help/destinations/catalog/personalization/custom-personalization.md). Door deze bestemmingen te gebruiken, kunt u zelfde-pagina en volgende-pagina gebruiksgevallen van het verpersoonlijkingsgebruik voor uw klanten toelaten.

Meer informatie over hoe [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](/help/destinations/ui/configure-personalization-destinations.md).

## Exporteren van profielen en segmentexportdoelen - video-overzicht {#video}

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensies {#extensions}

Platform maakt gebruik van de kracht en flexibiliteit van tagbeheer, zodat u tagextensies kunt configureren in de gebruikersinterface.

>[!TIP]
>
>Raadpleeg voor meer informatie over extensies van tags, waaronder gebruiksgevallen en de manier waarop u deze kunt vinden in de interface de [overzicht van tagextensies](./catalog/launch-extensions/overview.md).

Met uitbreidingen worden onbewerkte gebeurtenisgegevens doorgestuurd naar verschillende typen doelen. Extensies beschouwen als een **Gebeurtenis doorsturen** type bestemming. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Verkrijg inzicht in verpersoonlijkingsuitbreiding](./catalog/personalization/gainsight.md) of de [Bevestiging Stem van de uitbreiding van de Klant](./catalog/voice/confirmit-digital-feedback.md).

![Extensies labelen in vergelijking met andere doelen](./assets/common/launch-and-other-destinations.png)

## Wanneer gebruikt u verbindingen en extensies {#when-to-use}

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn handig wanneer u een volledig gecentraliseerd klantprofiel of een klantensegment voor activering wilt gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald segment te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker worden aangesloten.

## Doelcategorieën {#categories}

De verbindingen en extensies in het dialoogvenster [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Reclame**, **Cloud-opslag**, **Platformen voor enquêtes**, **E-mailmarketing**, enz.), afhankelijk van de marketingactie die ze u helpen te bereiken. Voor meer informatie over elk van de categorieën, evenals de bestemmingen inbegrepen in elke categorie, zie [Documentatie doelcatalogus](./catalog/overview.md).

![Doelcategorieën](./assets/destination-types/destination-categories-menu.png)
