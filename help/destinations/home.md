---
title: Overzicht van doelen
description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: d3c7b416317034c8d57663e0c05c9dc4dbe6d2d4
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# [!DNL Destinations]-overzicht {#overview}

![Banner Overzicht van doelen.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Platform is het opnemen van uw gegevens van de eerste partij en het activeren van deze gegevens voor uw bedrijfsbehoeften. Gebruiken [bronnen](../sources/home.md) om gegevens in Platform en bestemmingen in te voeren om gegevens van Platform uit te voeren.

## Doelstappen {#steps}

* Kiezen uit een [zelfbedieningscatalogus](./catalog/overview.md) van alle bestemmingen beschikbaar in Platform.
* Gebruik bestemmingen om publiek of datasets naar de platforms van de marketing automatisering, digitale reclameplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

De besturingselementen in de [werkruimte doelen](./ui/destinations-workspace.md) staat u toe:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel Platform aan de account op het doelplatform;
* Selecteer welk publiek of welke datasets voor bestemmingen moeten worden geactiveerd;
* Selecteren [XDM-velden (Experience Data Model)](../xdm/home.md) om te exporteren wanneer het publiek wordt geactiveerd naar bepaalde doelen, zoals marketingdoelen voor e-mail, CRM-platforms, opslaglocaties voor de cloud en meer.
* Activeer verschillende soorten profielen en publiek aan bestemmingen - mensen, rekeningen, en vooruitzichten.

## Doeltypen en -categorieën {#types-and-categories}

Met Experience Platform, kunt u gegevens aan diverse soorten bestemmingen activeren, om aan uw activeringsgebruiksgevallen te voldoen. De bestemmingen variëren van op API-Gebaseerde integratie, tot integratie met dossierontvangstsystemen, de bestemmingen van de profielraadpleging, en meer. Voor gedetailleerde informatie over alle beschikbare bestemmingen, lees [doeltypen en -categorieën, overzicht](./destination-types.md).

## Adobe-gebouwde en partner-gebouwde bestemmingen {#adobe-and-partner-built-destinations}

Sommige schakelaars in de catalogus van de bestemmingen van het Experience Platform worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerbedrijven worden gebouwd en worden gehandhaafd gebruikend [Destination SDK](/help/destinations/destination-sdk/overview.md). Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bestemming door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld de [Amazon S3-connector](/help/destinations/catalog/cloud-storage/amazon-s3.md) wordt gemaakt door Adobe, terwijl de [TikTok-connector](/help/destinations/catalog/social/tiktok.md) wordt gemaakt en onderhouden door het TikTok-team.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door de Adobe ontworpen en onderhouden connectors contact op met uw Adobe of de klantenservice.

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Platform werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Ga voor informatie over de individuele machtigingen naar [toegangsbeheer in Adobe Experience Platform](../access-control/home.md) en schuift omlaag naar de tabel onder aan de pagina.

De volgende lijst schetst de toestemmingen en toestemmingscombinaties die worden vereist om bepaalde acties op bestemmingen uit te voeren:

| Machtigingsniveau | Beschrijving |
| ---- | ---- |
| **[!UICONTROL Manage Destinations]** | Om met bestemmingen te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** | Om het publiek aan bestemmingen te activeren en toelaat [toewijzingsstap](ui/activate-batch-profile-destinations.md#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** | Om het publiek aan bestemmingen te activeren en te verbergen [toewijzingsstap](ui/activate-batch-profile-destinations.md#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Identity Graph]** | Om te exporteren *identiteiten* aan bestemmingen, hebt u nodig **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie over toegangscontroles, zie [Gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md).

### Op kenmerken gebaseerd toegangsbeheer voor bestemmingen {#attribute-based-access}

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens naar een bestemming uitvoeren als u geen toegang tot alle gebieden in de dataset hebt.

Voor meer informatie over hoe de bestemmingen met op attribuut-gebaseerde toegangscontroles werken, lees [op attributen-gebaseerd toegangsbeheeroverzicht](../access-control/abac/overview.md#destinations).

## Controle van de bestemmingen {#destinations-monitoring}

Nadat u een verbinding met een doel hebt gemaakt en de activeringsworkflow hebt voltooid, kunt u de gegevens die u exporteert naar uw ontvangstsysteem controleren. Lees de [gids over het controleren van gegevensstromen aan bestemmingen in UI](/help/dataflows/ui/monitor-destinations.md) voor meer informatie .

![Voorbeeld van de pagina Doelen die controleren.](./assets/overview/monitoring-page-example.png)

U kunt ook controleren of gegevens naar uw bestemming zijn gekomen. De meeste doeldocumentatiepagina&#39;s in de catalogus hebben een *Sectie Gegevens exporteren valideren*, die erop wijst hoe u in het bestemmingsplatform kunt controleren dat de gegevens met succes van Experience Platform worden gebracht. Een voorbeeld van deze sectie weergeven voor de [Amazon Ads-bestemming](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Beperkingen inzake gegevensbeheer bij het activeren van gegevens naar bestemmingen {#data-governance}

Het gegevensbeheer wordt afgedwongen voor platformbestemmingen via:

* *Marketingacties* dat u in creeert bestemmingswerkschema kunt selecteren;
* *Beleid voor gegevensgebruik* die de activering van gegevens met bepaalde gebruiksetiketten beperken tot bestemmingen met bepaalde marketingacties.

Zie Data Governance in de documentatie van het Platform voor meer informatie over [marketingacties](../data-governance/policies/overview.md) en [gegevensbeleidsovertredingen oplossen](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in Platform voor meer informatie over het selecteren van marketingacties in de workflow voor het maken van doelen:

* [Reclamebestemmingen - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Reclamebestemmingen - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertentiebestemmingen - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Opslagdoelen voor cloud](./catalog/cloud-storage/overview.md)
* [E-mailmarketingdoelen](./catalog/email-marketing/overview.md)
* [Sociale bestemmingen](./catalog/social/overview.md)

Zie voor meer informatie over schendingen van gegevensbeleid in de workflow voor activering van het publiek de **[!UICONTROL Review]** stap in de volgende hulplijnen:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](./ui/activate-segment-streaming-destinations.md#review)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](./ui/activate-streaming-profile-destinations.md#review)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](./ui/activate-batch-profile-destinations.md#review)
