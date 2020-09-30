---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Overzicht van bestemmingen
seo-title: Overzicht van bestemmingen
description: Activeer de gegevens van het Platform aan bestemmingen voor kanaalmarketing campagnes, e-mail, gerichte reclame, en meer.
seo-description: Doelen zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van het Platform van de Gegevens van de Klant in real time toestaan. U kunt Doelen in het Adobe Real-time Platform van de Gegevens van de Klant gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
translation-type: tm+mt
source-git-commit: 4e358fda1c8f7aebe57a009a146b8b73cf88e169
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# [!DNL Destinations] overzicht {#overview}

![Overzicht van doelen banner](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**[!DNL Destinations]** zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van het Platform van de Gegevens van de Klant in real time toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

## Doelen en bronnen {#destinations-and-sources}

Één van de kernfuncties van CDP in real time neemt uw eerste-partijgegevens op en activeert het voor uw bedrijfsbehoeften. De bronnen van het gebruik om gegevens in CDP in real time en bestemmingen in te voeren om gegevens van CDP in real time uit te voeren.

## Doelstappen {#steps}

* Kies uit een [zelfbedieningencatalogus](/help/rtcdp/destinations/destinations-catalog.md) van alle bestemmingen beschikbaar in Echt - tijd CDP.
* Gebruik **[!UICONTROL Doelen]** om profielen of segmenten te [activeren](/help/rtcdp/destinations/activate-destinations.md) en te verzenden naar marketingautomatiseringsplatforms, digitale advertentieplatforms en meer.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

Met de besturingselementen in de werkruimte [](/help/rtcdp/destinations/destinations-workspace.md) Doelen kunt u:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account in een opslaglocatie of koppel Real-time CDP aan de account in het doelplatform.
* Selecteer welke segmenten moeten worden geactiveerd voor bestemmingen;
* Selecteer welke XDM-velden ( [](../../xdm/home.md) Experience Data Model) u wilt exporteren wanneer u segmenten activeert naar e-mailmarketingdoelen.

## Destination types and categories {#types-and-categories}

Voor gedetailleerde informatie, zie de [bestemmingstypes en categoriesoverzicht](/help/rtcdp/destinations/destination-types.md).

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in CDP in real time werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Zie [Toegangsbeheer in Adobe Experience Platform](../../access-control/home.md) en schuif omlaag naar de onderkant van de pagina voor informatie over de individuele machtigingen.

Voor meer informatie over toegangscontroles, zie de handleiding [van de controlegebruiker van de](../../access-control/ui/overview.md)Toegang.

## [!DNL Data Governance] beperkingen op het activeren van gegevens naar bestemmingen {#data-governance}

Het beheer van gegevens wordt afgedwongen voor CDP-bestemmingen in real time via:

* *Gebruiksgevallen* voor marketing die u kunt selecteren in de workflow voor het maken van doelen.
* *Beleid* voor gegevensgebruik dat gegevens met bepaalde gebruikslabels beperkt van activering tot bestemmingen met bepaalde gevallen van marketinggebruik.

Zie de [!DNL Data Governance] in CDP in real time documentatie voor meer informatie over de [marketing gebruiksgevallen](/help/rtcdp/privacy/data-governance-overview.md#destinations) en het [oplossen van de schendingen](/help/rtcdp/privacy/data-governance-overview.md#enforcement)van het gegevensbeleid.

Voor meer informatie over het selecteren van marketing gebruiksgevallen in creeer bestemmingswerkschema, zie de volgende pagina&#39;s voor de verschillende bestemmingstypes in Echt - tijd CDP:

* [Reclamebestemmingen - Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [Reclamebestemmingen - Google Ads](/help/rtcdp/destinations/google-ads-destination.md)
* [Advertentiebestemmingen - Google Display &amp; Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [Opslagdoelen voor cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [E-mailmarketingdoelen](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Sociale netwerkbestemmingen](/help/rtcdp/destinations/social-network-destinations-workflow.md)

Voor meer informatie over de schendingen van het gegevensbeleid in het werkschema van de segmentactivering, zie de stap van het Overzicht in [activeert profielen en segmenten aan een bestemming](/help/rtcdp/destinations/activate-destinations.md#review).