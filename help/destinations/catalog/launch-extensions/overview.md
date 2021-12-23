---
keywords: tagextensies;tagextensie;lanceerdoelen; platformtagextensies;platform tagextensie;platform launch-bestemmingen
title: Tagextensies in Adobe Experience Platform
description: Adobe Experience Platform biedt de volgende generatie mogelijkheden voor tagbeheer van Adobe. Platform biedt u een eenvoudige manier om alle analyses, marketing en reclametags te implementeren en te beheren die nodig zijn om de ervaring van klanten te verbeteren.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Extensies labelen in Adobe Experience Platform

Adobe Experience Platform biedt de volgende generatie mogelijkheden voor tagbeheer van Adobe. Platform biedt u een eenvoudige manier om alle analyses, marketing en reclametags te implementeren en te beheren die nodig zijn om de ervaring van klanten te verbeteren. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element.

Zie de volgende bronnen voor een inleiding op tags:

- [Overzicht van codes](../../../tags/home.md)
- [Snelle startgids](../../../tags/quick-start/quick-start.md)

## Hoe te om markeringsuitbreidingen in de interface van het Platform te vinden {#how-to-find-extensions-in-interface}

Blader naar de extensies in de interface Platform om de extensies te zoeken **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** en selecteert u **[!UICONTROL Extensions]** in de **[!UICONTROL Types]** filter.

![Extensies, filter in de interface](../../assets/catalog/launch-extensions/filter.png)

## Hoe werken tagextensies? {#how-extensions-work}

A [tagextensie](../../../tags/home.md#extensions) is een pakket code dat de functionaliteit van een website of mobiele app verbetert. Dit kan onder andere het verzenden van onbewerkte gebeurtenisgegevens naar een bestemming [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) maar ze kunnen ook andere functies vervullen .

Het is belangrijk om tussen markering en gebeurtenis te onderscheiden die uitbreidingen door:sturen. De extensies die worden weergegeven in de gebruikersinterface van de Platform-bestemmingen zijn *tagextensies*. Raadpleeg het overzicht over het doorsturen van gebeurtenissen voor meer informatie over de [verschillen tussen tags en gebeurtenissen doorsturen](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Voordelen van het gebruik van tagextensies {#extensions-benefits}

De mogelijkheden voor tags van Platform zijn gratis voor bestaande Experience Cloud-klanten. Het systeem vereenvoudigt de implementatie van tags op uw website via eenvoudig te gebruiken extensies die u kunt installeren, configureren, bijwerken en verwijderen. Met labels blijft er een kleine voetafdruk op uw website staan, zodat uw pagina&#39;s snel kunnen worden geladen.

Hoewel u segmenten niet kunt activeren om extensies te labelen, kunt u regels instellen om alleen gebeurtenisgegevens in bepaalde situaties door te sturen. Met deze krachtige functionaliteit kunt u gebeurtenisgegevens alleen in bepaalde situaties doorsturen, in tegenstelling tot het verzenden van gebeurtenisgegevens voor elke interactie. Lees voor meer informatie over de regels in het dialoogvenster [codedocumentatie](../../../tags/ui/managing-resources/rules.md).

## Voorbeeld van gebruik voor extensies {#extensions-use-cases}

De uitbreidingen laten u toe om diverse klantengebruiksgevallen tevreden te stellen. Voorbeelden hiervan zijn:

- U kunt website- of native toepassingsgegevens naar Facebook verzenden via de Facebook-pixelextensie. Facebook Pixel geeft aan naar welke delen van uw site of app een bezoeker is genavigeerd, die informatie doorstuurt naar Facebook en u uw bezoeker kunt richten via Facebook.
- U kunt gebeurtenisgegevens van uw websites en apps doorsturen naar Google Analytics om deze te analyseren en beslissingen te nemen op basis van die gegevens.
- U kunt op het juiste moment een chatbox-app voor de client inschakelen op basis van de manier waarop uw gebruikers met uw pagina&#39;s communiceren, volgens de regels die u instelt.

## Extensiecategorieën {#extension-categories}

Extensies kunnen in Platform onder de volgende categorieën vallen:

- [Reclame](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Platform voor gegevensbeheer](../data-management/overview.md)
- [E-mailmarketingdoelen](../email-marketing/overview.md)
- [Personalisatie](../personalization/overview.md)
- [Enquêtes](../survey/overview.md)
- [Stem van de klant](../voice/overview.md)
