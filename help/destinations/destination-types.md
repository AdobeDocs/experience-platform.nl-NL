---
keywords: doelen;doel;doeltypen
title: Doeltypen en -categorieën
description: Leer meer over de verschillende typen en categorieën bestemmingen in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# Doeltypen en -categorieën

Lees deze pagina om de verschillende typen en categorieën Adobe Experience Platform-bestemmingen te begrijpen.

## Doeltypen {#destination-types}

In Adobe Experience Platform maken we onderscheid tussen verschillende doeltypen - verbindingen, gegevenssetexport en extensies. Er zijn verscheidene soorten verbindingsbestemmingen, die u toestaan om gegevens naar op API-Gebaseerde bestemmingen, sociale bestemmingen, de platforms van CRM, en vele meer uit te voeren.

Ten slotte kan ook een onderscheid worden gemaakt tussen openbare bestemmingen die beschikbaar zijn in alle organisaties in de lijst met bestemmingen, en particuliere bestemmingen die Real-Time CDP Ultimate-klanten kunnen maken om aan hun specifieke gevallen van exportgebruik te voldoen.

>[!BEGINSHADEBOX]

![&#x200B; Types van bestemmingsdiagram.](./assets/destination-types/types-of-destinations-no-highlight.png " Types van bestemmingsdiagram."){zoomable="yes"}

>[!ENDSHADEBOX]

## Verbindingen {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Audience Export]**, en **[!DNL Edge Personalization]** de bestemmingen in Adobe Experience Platform vangen gebeurtenisgegevens, combineren het met andere gegevensbronnen om het [&#x200B; Real-Time Profiel van de Klant &#x200B;](../profile/home.md) te vormen, segmentatie toe te passen, en uitvoerpubliek en gekwalificeerde profielen naar bestemmingen uit te voeren.

## Profielexportdoelen {#profile-export}

Profielexportdoelen ontvangen onbewerkte gegevens, vaak met e-mailadres als primaire sleutel. Experience Platform biedt momenteel ondersteuning voor twee typen exportdoelen voor profielen:

* [Batchbestemmingen (op basis van bestanden)](#file-based)
* [Geavanceerde zakelijke doelen (streamingprofielexportdoelen)](#advanced-enterprise-destinations)

### Geavanceerde zakelijke doelen (streamingprofielexportdoelen) {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>De geavanceerde ondernemingsbestemmingen, of het stromen de uitvoerbestemmingen van het profiel, zijn beschikbaar aan [&#x200B; Adobe Real-Time Customer Data Platform Ultimate &#x200B;](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) slechts klanten.

Gebruik de geavanceerde gegevensconnectors voor bedrijfsdoelgegevens om Adobe Real-Time Customer Data Platform-profielen in bijna realtime te leveren aan interne systemen of aan andere systemen van derden voor gegevenssynchronisatie, analyse en verdere gebruiksscenario&#39;s voor profielverrijking.

Deze doelen ontvangen publiek- en profielgegevens als Experience Platform-gegevensstromen.

De geavanceerde ondernemingsbestemmingen omvatten:

* [HTTP API-bestemming](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Batchbestemmingen (op basis van bestanden) {#file-based}

Bestandsdoelen ontvangen `.csv` -bestanden met profielen en/of kenmerken. [&#x200B; Amazon S3 &#x200B;](catalog/cloud-storage/amazon-s3.md) is een voorbeeld van een bestemming waar u dossiers kunt uitvoeren die profieluitvoer bevatten.

## Streaming doelpubliek exporteren {#streaming-destinations}

De de uitvoerbestemmingen van het publiek ontvangen de gegevens van het Experience Platform publiek. Deze doelen gebruiken gebruikers-id&#39;s of gebruikers-id&#39;s. Advertising en sociale bestemmingen zoals [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), of [&#x200B; Facebook &#x200B;](catalog/social/facebook.md) zijn voorbeelden van dergelijke bestemmingen.

## Edge-verpersoonlijkingsdoelen {#edge-personalization-destinations}

De de verpersoonlijkingsbestemmingen van Edge in Experience Platform omvatten [&#x200B; Adobe Target &#x200B;](/help/destinations/catalog/personalization/adobe-target-connection.md) en de [&#x200B; de verpersoonlijkingsbestemming van de Douane &#x200B;](/help/destinations/catalog/personalization/custom-personalization.md). Door deze bestemmingen te gebruiken, kunt u zelfde-pagina en volgende-pagina gebruiksgevallen van het verpersoonlijkingsgebruik voor uw klanten toelaten.

Lees meer over hoe te [&#x200B; verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking &#x200B;](/help/destinations/ui/activate-edge-personalization-destinations.md) vormen.

## Exporteren van profielen en doelgroepen - video-overzicht {#video}

In de onderstaande video worden de bijzonderheden van de twee soorten doelen uitgelegd:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Typen geëxporteerde soorten publiek {#exported-audiences-types}

U kunt drie soorten publiek vanuit Experience Platform exporteren naar verschillende doelen:

* Personen
* Accountdoelgroepen
* Doelgroepen

Leer meer over de [&#x200B; diverse publiekstypes &#x200B;](/help/segmentation/types/account-audiences.md#terminology).

Een symbool op de doelkaart geeft aan welke soorten publiek u naar elk doel kunt exporteren.

![&#x200B; de bestemmingskaart van het voorbeeld met symbolen die tonen welke publiekstypes kunnen worden uitgevoerd.](/help/destinations/assets/destination-types/types-of-audiences.png " de bestemmingskaart van het Voorbeeld met symbolen die tonen welke publiekstypes kunnen worden uitgevoerd."){zoomable="yes"}


## Dataset-exportdoelen {#dataset-export-destinations}

Sommige bestemmingen van de wolkenopslag in de catalogus van bestemmingen steunen dataset de uitvoer. Gebruik deze doelen om onbewerkte gegevenssets te exporteren naar opslaglocaties in de cloud.

Lees meer over hoe te [&#x200B; uitvoerdatasets &#x200B;](/help/destinations/ui/export-datasets.md).

## Extensies {#extensions}

Experience Platform maakt gebruik van de kracht en flexibiliteit van tagbeheer, zodat u tagextensies kunt configureren in de gebruikersinterface.

>[!TIP]
>
>Voor gedetailleerde informatie over markeringsuitbreidingen, met inbegrip van gebruiksgevallen en hoe te om hen in de interface te vinden, zie het [&#x200B; overzicht van markeringsuitbreidingen &#x200B;](./catalog/launch-extensions/overview.md).

Met extensies kunt u onbewerkte gebeurtenisgegevens doorsturen naar verschillende typen doelen. Denk aan uitbreidingen als **Gebeurtenis door:sturen** type van bestemming. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. De voorbeelden van die zijn de [&#x200B; Verkenningsverpersoonlijkingsuitbreiding van de Reeks &#x200B;](./catalog/personalization/gainsight.md) of de [&#x200B; Bevestiging Stem van de uitbreiding van de Klant &#x200B;](./catalog/voice/confirmit-digital-feedback.md).

![&#x200B; uitbreidingen van de Markering vergeleken met andere bestemmingen &#x200B;](./assets/common/launch-and-other-destinations.png)

## Wanneer gebruiken verbindingen en uitbreidingen {#when-to-use}

Als een markeerteken kunt u een combinatie van verbindingen en extensies gebruiken om uw gebruiksproblemen aan te pakken.

Verbindingen zijn nuttig wanneer het noodzakelijk is om een volledig gecentraliseerd klantprofiel of een klantenpubliek voor activering te gebruiken. Gebruik bijvoorbeeld verbindingen als u gedragsgegevens van een analysesysteem met geüploade CRM-gegevens samenvoegt om een gebruiker voor een bepaald publiek te kwalificeren voordat u een gepersonaliseerd bericht aan die gebruiker afgeeft.

Extensies zijn handig wanneer gebeurtenisgegevens worden gebruikt om een handeling te activeren of om segmentatie uit te voeren in een externe omgeving. Bijvoorbeeld, als de gedragsgegevens aan een extern systeem moeten worden door:sturen zonder aan andere gegevensbronnen op dossier voor een bepaalde gebruiker te worden aangesloten.

## Doelcategorieën {#categories}

De verbindingen en de uitbreidingen in de [&#x200B; bestemmingscatalogus &#x200B;](https://platform.adobe.com/destination/catalog) worden gegroepeerd door bestemmingscategorie (**Advertising**, **de opslag van de Wolk**, **platforms van het Onderzoek**, **E-mail marketing**, enz.), afhankelijk van de marketing actie die zij u helpen bereiken. Voor meer informatie over elk van de categorieën, evenals de bestemmingen inbegrepen in elke categorie, zie de [&#x200B; catalogusdocumentatie van Doelen &#x200B;](./catalog/overview.md).

![&#x200B; categorieën van de Bestemming die in de cataloguspagina worden benadrukt.](./assets/destination-types/destination-categories-menu.png " categorieën van de Bestemming die in de cataloguspagina worden benadrukt."){zoomable="yes"}
