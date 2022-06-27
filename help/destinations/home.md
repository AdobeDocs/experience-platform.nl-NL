---
keywords: doelen;adobe Experience platform;platform;bestemmingen, overzicht;activate gegevens;activate;
title: Overzicht van doelen
description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Destinations] - overzicht {#overview}

![Overzicht van doelen banner](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Platform is het opnemen van uw gegevens van de eerste partij en het activeren ervan voor uw bedrijfsbehoeften. Gebruiken [bronnen](../sources/home.md) om gegevens in Platform en bestemmingen in te voeren om gegevens uit Platform uit te voeren.

## Doelstappen {#steps}

* Kiezen uit een [zelfbedieningscatalogus](./catalog/overview.md) van alle in Platform beschikbare bestemmingen.
* Gebruik bestemmingen om profielen of segmenten naar marketingautomatiseringsplatforms, digitale advertentieplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

De besturingselementen in de [Werkruimte Doelen](./ui/destinations-workspace.md) staat u toe:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel een Platform naar de account op het doelplatform;
* Selecteer welke segmenten moeten worden geactiveerd voor bestemmingen;
* Selecteren [XDM-velden (Experience Data Model)](../xdm/home.md) om te exporteren bij het activeren van segmenten naar marketingdoelen per e-mail.

## Doeltypen en -categorieën {#types-and-categories}

Zie voor meer informatie de [doeltypen en -categorieën, overzicht](./destination-types.md).

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Platform werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Voor informatie over de individuele toestemmingen, zie [Toegangsbeheer in Adobe Experience Platform](../access-control/home.md) en schuift omlaag naar de onderkant van de pagina.

Voor meer informatie over toegangscontroles, zie [Gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md).

## Beperkingen op gegevensbeheer bij het activeren van gegevens naar bestemmingen {#data-governance}

Het gegevensbeheer wordt afgedwongen voor bestemmingen in de Platform via:

* *Marketingacties* dat u in creeert bestemmingswerkschema kunt selecteren;
* *Beleid voor gegevensgebruik* die de activering van gegevens met bepaalde gebruiksetiketten beperken tot bestemmingen met bepaalde marketingacties.

Zie Gegevensbeheer in de documentatie van het Platform voor meer informatie over [marketingacties](../data-governance/policies/overview.md) en [gegevensbeleidsovertredingen oplossen](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in het Platform voor meer informatie over het selecteren van marketingacties in de workflow Doel maken:

* [Reclamebestemmingen - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Reclamebestemmingen - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertentiebestemmingen - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Opslagdoelen voor cloud](./catalog/cloud-storage/overview.md)
* [E-mailmarketingdoelen](./catalog/email-marketing/overview.md)
* [Sociale bestemmingen](./catalog/social/overview.md)

Zie de stap Controleren in de volgende handleidingen voor meer informatie over schendingen van gegevensbeleid in de workflow voor segmentactivering:

* [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](./ui/activate-segment-streaming-destinations.md#review)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](./ui/activate-streaming-profile-destinations.md#review)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](./ui/activate-batch-profile-destinations.md#review)
