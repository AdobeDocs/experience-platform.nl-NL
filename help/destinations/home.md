---
keywords: doelen;adobe Experience platform;platform;bestemmingen, overzicht;activate gegevens;activate;
title: Overzicht van doelen
seo-title: Overzicht van doelen
description: Leer hoe u Adobe Experience Platform-gegevens activeert naar bestemmingen voor marketingcampagnes over verschillende kanalen, e-mails, gerichte advertenties en meer.
seo-description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# [!DNL Destinations] overzicht  {#overview}

![Overzicht van doelen banner](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Platform is het opnemen van uw gegevens van de eerste partij en het activeren ervan voor uw bedrijfsbehoeften. Gebruik [bronnen](../sources/home.md) om gegevens in te voeren in Platform en bestemmingen om gegevens uit Platform te exporteren.

## Doelstappen {#steps}

* Kies uit een [zelfbedieningencatalogus](./catalog/overview.md) van alle bestemmingen beschikbaar in Platform.
* Gebruik bestemmingen om [te activeren](./ui/activate-destinations.md) en profielen of segmenten naar marketing automatiseringsplatforms, digitale reclameplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

Met de besturingselementen in de [werkruimte Doelen](./ui/destinations-workspace.md) kunt u:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel een Platform naar de account op het doelplatform;
* Selecteer welke segmenten moeten worden geactiveerd voor bestemmingen;
* Selecteer welke [XDM-velden (Experience Data Model)](../xdm/home.md) moeten worden geëxporteerd wanneer u segmenten activeert naar marketingdoelen via e-mail.

## Doeltypen en -categorieën {#types-and-categories}

Voor gedetailleerde informatie, zie [bestemmingstypes en categorieën overzicht](./destination-types.md).

## Bestemmingen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Platform werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Voor informatie over de individuele toestemmingen, zie [Toegangsbeheer in Adobe Experience Platform](../access-control/home.md) en rol neer aan de bodem van de pagina.

Voor meer informatie over toegangscontroles, zie [de gebruikershandleiding van het Toegangsbeheer](../access-control/ui/overview.md).

## [!DNL Data Governance] beperkingen op het activeren van gegevens naar bestemmingen  {#data-governance}

Het gegevensbeheer wordt afgedwongen voor bestemmingen in de Platform via:

* *Marketingacties* die u kunt selecteren in de workflow voor het maken van doelen.
* *Beleid* voor gegevensgebruik dat beperkt dat gegevens met bepaalde gebruikslabels worden geactiveerd tot bestemmingen met bepaalde marketingacties.

Zie [!DNL Data Governance] in de documentatie van het Platform voor meer informatie over [marketing acties](../data-governance/policies/overview.md) en [het oplossen van de schendingen van het gegevensbeleid](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in het Platform voor meer informatie over het selecteren van marketingacties in de workflow Doel maken:

* [Reclamebestemmingen - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Reclamebestemmingen - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertentiebestemmingen - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [Opslagdoelen voor cloud](./catalog/cloud-storage/workflow.md)
* [E-mailmarketingdoelen](./catalog/email-marketing/overview.md)
* [Sociale bestemmingen](./catalog/social/workflow.md)

Voor meer informatie over de schendingen van gegevensbeleid in het werkschema van de segmentactivering, zie de stap van het Overzicht in [Activate profielen en segmenten aan een bestemming](./ui/activate-destinations.md#review).
