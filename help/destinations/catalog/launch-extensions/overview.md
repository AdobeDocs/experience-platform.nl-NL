---
keywords: tagextensies;tagextensie;lanceerdoelen; platformtagextensies;platform tagextensie;platform launch-bestemmingen
title: Tagextensies in Adobe Experience Platform
description: Adobe Experience Platform biedt de volgende generatie mogelijkheden voor tagbeheer van Adobe. Platform biedt u een eenvoudige manier om alle analyses, marketing en reclametags te implementeren en te beheren die nodig zijn om de ervaring van klanten te verbeteren.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Extensies labelen in Adobe Experience Platform

Adobe Experience Platform biedt de volgende generatie mogelijkheden voor tagbeheer van Adobe. Platform biedt u een eenvoudige manier om alle analyses, marketing en reclametags te implementeren en te beheren die nodig zijn om de ervaring van klanten te verbeteren. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element.

Zie de volgende bronnen voor een inleiding op tags:

- [Overzicht van codes](../../../tags/home.md)
- [Snelle startgids](../../../tags/quick-start/quick-start.md)

## Hoe te om markeringsuitbreidingen in de interface van het Platform te vinden {#how-to-find-extensions-in-interface}

Als u de extensies wilt zoeken in de interface Platform, bladert u naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** en selecteert u **[!UICONTROL Extensions]** in het filter **[!UICONTROL Types]**.

![Extensies, filter in de interface](../../assets/catalog/launch-extensions/filter.png)

## Hoe werken tagextensies? {#how-extensions-work}

Extensies sturen onbewerkte gebeurtenisgegevens door naar verschillende typen doelen. Beschouw extensies als een **Event Forwarding**-type van bestemming. Dit is een eenvoudiger type integratie met doelplatforms, die alleen onbewerkte gebeurtenisgegevens doorsturen. Voorbeelden hiervan zijn de [Grondige personalisatie-extensie](../personalization/gainsight.md) of de [Spraak van de klant-extensie bevestigen](../voice/confirmit-digital-feedback.md).

**Profiel/segment** Exportbestemmingen in Adobe Experience Platform leggen gebeurtenisgegevens vast, combineren deze met andere gegevensbronnen, passen segmentatie toe, en exporteer segmenten en gekwalificeerde profielen naar bestemmingen. Voorbeelden hiervan zijn de [Amazon S3 cloudopslagbestemming](../cloud-storage/amazon-s3.md) of de [Google Display &amp; Video 360 advertentiebestemming](../advertising/google-dv360.md).

![Extensies labelen in vergelijking met andere doelen](../../assets/common/launch-and-other-destinations.png)

## Voordelen van het gebruik van tagextensies {#extensions-benefits}

De mogelijkheden voor tags van Platform zijn gratis voor bestaande Experience Cloud-klanten. Het systeem vereenvoudigt de implementatie van tags op uw website via eenvoudig te gebruiken extensies die u kunt installeren, configureren, bijwerken en verwijderen. Met labels blijft er een kleine voetafdruk op uw website staan, zodat uw pagina&#39;s snel kunnen worden geladen.

Hoewel u segmenten niet kunt activeren om extensies te labelen, kunt u regels instellen om alleen gebeurtenisgegevens in bepaalde situaties door te sturen. Met deze krachtige functionaliteit kunt u gebeurtenisgegevens alleen in bepaalde situaties doorsturen, in tegenstelling tot het verzenden van gebeurtenisgegevens voor elke interactie. Lees voor meer informatie de regels in de [tagdocumentatie](../../../tags/ui/managing-resources/rules.md).

## Voorbeeld van gebruik voor extensies {#extensions-use-cases}

De uitbreidingen laten u toe om diverse klantengebruiksgevallen tevreden te stellen. U kunt bijvoorbeeld extensies gebruiken in de volgende gevallen:

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
