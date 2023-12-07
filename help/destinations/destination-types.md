---
keywords: doelen;doel;doeltypen
title: Doeltypen en -categorieën
description: Leer meer over de verschillende typen en categorieën bestemmingen in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: c6019737e93756f3f524d5a85ea57383baa1a31d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Doeltypen en -categorieën

Lees deze pagina om de verschillende typen en categorieën Adobe Experience Platform-bestemmingen te begrijpen.

## Doeltypen {#destination-types}

In Adobe Experience Platform maken we onderscheid tussen verschillende doeltypen - verbindingen, gegevenssetexport en extensies. Er zijn verscheidene soorten verbindingsbestemmingen, die u toestaan om gegevens naar op API-Gebaseerde bestemmingen, sociale bestemmingen, de platforms van CRM, en vele meer uit te voeren.

Ten slotte kan ook een onderscheid worden gemaakt tussen openbare bestemmingen die beschikbaar zijn in alle organisaties in de lijst met bestemmingen, en particuliere bestemmingen die Real-Time CDP Ultimate-klanten kunnen maken om aan hun specifieke gevallen van exportgebruik te voldoen.

![Soorten bestemmingsdiagram.](./assets/destination-types/types-of-destinations-no-highlight.png)

## Verbindingen {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Audience Export]**, en **[!DNL Edge Personalization]** doelen in Adobe Experience Platform leggen gebeurtenisgegevens vast, combineren deze met andere gegevensbronnen om de [Klantprofiel in realtime](../profile/home.md), segmentatie toe te passen, en publiek en gekwalificeerde profielen naar bestemmingen uit te voeren.

## Profielexportdoelen {#profile-export}

Profielexportdoelen ontvangen onbewerkte gegevens, vaak met e-mailadres als primaire sleutel. Experience Platform ondersteunt momenteel twee typen exportdoelen voor profielen:

* [Streaming profiel exportdoelen (ondernemingsdoelen)](#streaming-profile-export)
* [Batchbestemmingen (op basis van bestanden)](#file-based)

### Streaming profiel exportdoelen (ondernemingsdoelen) {#streaming-profile-export}

>[!IMPORTANT]
>
>De bestemmingen van de onderneming, of het stromen profiel de uitvoerbestemmingen, zijn beschikbaar aan [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) alleen aan klanten.

Gebruik gegevensconnectors voor bedrijfsdoelgegevens om Adobe Real-time Customer Data Platform-profielen in bijna realtime te leveren aan interne systemen of aan andere systemen van derden voor gegevenssynchronisatie, analyse en verdere gebruiksscenario&#39;s voor profielverrijking.

Deze doelen ontvangen publiek- en profielgegevens als gegevensstromen van Experience Platforms.

De bestemmingen van de onderneming omvatten:

* [HTTP API-bestemming](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Batchbestemmingen (op basis van bestanden) {#file-based}

Bestandsgebaseerde doelen ontvangen `.csv` bestanden met profielen en/of kenmerken. [Amazon S3](catalog/cloud-storage/amazon-s3.md) Dit is een voorbeeld van een bestemming waar u bestanden kunt exporteren die profielen bevatten.

## Streaming doelpubliek exporteren {#streaming-destinations}

De de uitvoerbestemmingen van het publiek van het publiek ontvangen de gegevens van het Experience Platform. Deze doelen gebruiken gebruikers-id&#39;s of gebruikers-id&#39;s. Reclame en sociale bestemmingen zoals [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), of [Facebook](catalog/social/facebook.md) zijn voorbeelden van dergelijke bestemmingen .

## Edge-verpersoonlijkingsdoelen {#edge-personalization-destinations}

De het verpersoonlijkingsbestemmingen van de rand in Experience Platform omvatten [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) en de [Aangepast aanpassingsdoel](/help/destinations/catalog/personalization/custom-personalization.md). Door deze bestemmingen te gebruiken, kunt u zelfde-pagina en volgende-pagina gebruiksgevallen van het verpersoonlijkingsgebruik voor uw klanten toelaten.

Meer informatie over hoe [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Exporteren van profielen en doelgroepen - video-overzicht {#video}

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Typen geëxporteerde soorten publiek {#exported-audiences-types}

U kunt drie soorten publiek van Experience Platform naar diverse bestemmingen uitvoeren:

* Personen
* Accountpubliek
* Doelgroepen

Meer informatie over de [verschillende soorten doelgroepen](/help/segmentation/ui/account-audiences.md#terminology).

Een symbool op de doelkaart geeft aan welke soorten publiek u naar elk doel kunt exporteren.

![Voorbeeld van doelkaart met symbolen die aangeven welke soorten publiek kunnen worden geëxporteerd.](/help/destinations/assets/destination-types/types-of-audiences.png)


## Dataset-exportdoelen {#dataset-export-destinations}

Sommige bestemmingen van de wolkenopslag in de catalogus van bestemmingen steunen dataset de uitvoer. Gebruik deze doelen om onbewerkte gegevenssets te exporteren naar opslaglocaties in de cloud.

Meer informatie over hoe [exportgegevenssets](/help/destinations/ui/export-datasets.md).

## Extensies {#extensions}

Platform maakt gebruik van de kracht en flexibiliteit van tagbeheer, zodat u tagextensies kunt configureren in de gebruikersinterface.

>[!TIP]
>
>Raadpleeg voor meer informatie over extensies van tags, waaronder gebruik en het zoeken van deze extensies in de interface de [overzicht van tagextensies](./catalog/launch-extensions/overview.md).

Met extensies kunt u onbewerkte gebeurtenisgegevens doorsturen naar verschillende typen doelen. Extensies beschouwen als een **Gebeurtenis doorsturen** type bestemming. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Verkrijg inzicht in verpersoonlijkingsuitbreiding](./catalog/personalization/gainsight.md) of de [Bevestiging Stem van de uitbreiding van de Klant](./catalog/voice/confirmit-digital-feedback.md).

![Extensies labelen in vergelijking met andere doelen](./assets/common/launch-and-other-destinations.png)

## Wanneer gebruiken verbindingen en uitbreidingen {#when-to-use}

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn nuttig wanneer het noodzakelijk is om een volledig gecentraliseerd klantprofiel of een klantenpubliek voor activering te gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald publiek te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker te worden aangesloten.

## Doelcategorieën {#categories}

De verbindingen en extensies in het dialoogvenster [doelcatalogus](https://platform.adobe.com/destination/catalog) worden gegroepeerd op doelcategorie (**Reclame**, **Cloud-opslag**, **Platformen voor enquêtes**, **E-mailmarketing**, enz.), afhankelijk van de marketingactie die ze u helpen te bereiken. Voor meer informatie over elk van de categorieën, evenals de bestemmingen inbegrepen in elke categorie, zie [Documentatie doelcatalogus](./catalog/overview.md).

![Doelcategorieën die zijn gemarkeerd in de cataloguspagina.](./assets/destination-types/destination-categories-menu.png)
