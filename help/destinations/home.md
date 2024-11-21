---
title: Overzicht van doelen
description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6d97f132788a249e0bf5c293e34d9d529325f099
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 3%

---

# [!DNL Destinations]-overzicht {#overview}

![ de overzichtsbanner van Doelen.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Platform is het opnemen van uw gegevens van de eerste partij en het activeren van deze gegevens voor uw bedrijfsbehoeften. Gebruik [ bronnen ](../sources/home.md) om gegevens in Platform en bestemmingen in te voeren om gegevens van Platform uit te voeren.

## Doelstappen {#steps}

* Kies van a [ zelfbedieningencatalogus ](./catalog/overview.md) van alle bestemmingen beschikbaar in Platform.
* Gebruik bestemmingen om publiek of datasets naar de platforms van de marketing automatisering, digitale reclameplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

De controles in de [ werkruimte van bestemmingen ](./ui/destinations-workspace.md) staan u toe:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel Platform aan de account op het doelplatform;
* Selecteer welk publiek of welke datasets voor bestemmingen moeten worden geactiveerd;
* Selecteer welke [ gebieden van de Gegevens van de Ervaring Model (XDM) ](../xdm/home.md) om te exporteren wanneer het activeren van publiek aan bepaalde bestemmingen zoals e-mail marketing bestemmingen, de platforms van CRM, de plaatsen van de wolkenopslag, en meer.
* Activeer verschillende soorten profielen en publiek aan bestemmingen - mensen, rekeningen, en vooruitzichten.

## Doeltypen en -categorieën {#types-and-categories}

Met Experience Platform, kunt u gegevens aan diverse soorten bestemmingen activeren, om aan uw activeringsgebruiksgevallen te voldoen. De bestemmingen variëren van op API-Gebaseerde integratie, tot integratie met dossierontvangstsystemen, de bestemmingen van de profielraadpleging, en meer. Voor gedetailleerde informatie over alle beschikbare bestemmingen, lees de [ bestemmingstypes en de categorieën overzicht ](./destination-types.md).

## Adobe-gebouwde en partner-gebouwde bestemmingen {#adobe-and-partner-built-destinations}

Sommige schakelaars in de de bestemmingscatalogus van het Experience Platform worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerondernemingen worden gebouwd en worden gehandhaafd gebruikend [ Destination SDK ](/help/destinations/destination-sdk/overview.md). Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bestemming door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld, wordt de [ schakelaar van Amazon S3 ](/help/destinations/catalog/cloud-storage/amazon-s3.md) gecreeerd door Adobe, terwijl de [ schakelaar van TikTok ](/help/destinations/catalog/social/tiktok.md) door het team van TikTok wordt gecreeerd en gehandhaafd.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door de Adobe ontworpen en onderhouden connectors contact op met uw Adobe of de klantenservice.

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Platform werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Voor informatie over de individuele toestemmingen, ga naar [ toegangsbeheer in Adobe Experience Platform ](../access-control/home.md) en rol neer aan de lijst bij de bodem van de pagina.

De volgende lijst schetst de toestemmingen en toestemmingscombinaties die worden vereist om bepaalde acties op bestemmingen uit te voeren.

| Machtigingsniveau | Beschrijving |
| ---- | ---- |
| **[!UICONTROL View Destinations]** | Om tot het bestemmingslusje in het Experience Platform UI toegang te hebben, hebt u de **[!UICONTROL View Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]** | Om met bestemmingen te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]** , **[!UICONTROL Activate Destinations]** , **[!UICONTROL View Profiles]** en **[!UICONTROL View Segments]** | Om publiek aan bestemmingen te activeren en de [ toewijzingsstap ](ui/activate-batch-profile-destinations.md#mapping) van het werkschema toe te laten, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]** , **[!UICONTROL Activate Segments without Mapping]** , **[!UICONTROL View Profiles]** en **[!UICONTROL View Segments]** | Om publiek van bestaande dataflows toe te voegen of te verwijderen zonder toegang tot de [ toewijzingsstap ](ui/activate-batch-profile-destinations.md#mapping) van het werkschema te hebben, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage and Activate Dataset Destinations]** | Om datasets naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Identity Graph]** | Om *identiteiten* naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Het diagram hieronder toont visueel welke toestemmingen u afhankelijk van de verrichtingen nodig hebt die u op bestemmingen wilt uitvoeren.

![ Diagram die de vereiste toestemmingen tonen om bepaalde acties op bestemmingen uit te voeren.](/help/destinations/assets/overview/permissions-diagram.png)

Voor meer informatie over toegangscontroles, zie de [ handleiding van de controlegebruiker van de Toegang ](../access-control/ui/overview.md).

### Op kenmerken gebaseerd toegangsbeheer voor bestemmingen {#attribute-based-access}

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens naar een bestemming uitvoeren als u geen toegang tot alle gebieden in de dataset hebt.

Voor meer informatie over hoe de bestemmingen met op attribuut-gebaseerde toegangscontroles werken, lees het [ op attribuut-gebaseerde overzicht van de toegangscontrole ](../access-control/abac/overview.md#destinations).

## Controle van de bestemmingen {#destinations-monitoring}

Nadat u een verbinding met een doel hebt gemaakt en de activeringsworkflow hebt voltooid, kunt u de gegevens die u exporteert naar uw ontvangstsysteem controleren. Lees de [ gids bij het controleren van dataflows aan bestemmingen in UI ](/help/dataflows/ui/monitor-destinations.md) voor meer informatie.

![ Doelen die paginavoorbeeld controleren.](./assets/overview/monitoring-page-example.png)

U kunt ook controleren of gegevens naar uw bestemming zijn gekomen. De meeste pagina&#39;s van de bestemmingsdocumentatie in de catalogus hebben de sectie van de a *de uitvoer van gegevens* bevestigen, die erop wijst hoe u in het bestemmingsplatform kunt controleren dat het gegeven met succes van Experience Platform wordt gebracht. Bekijk een voorbeeld van deze sectie voor de [ bestemming van de Advertentie van Amazon ](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Beperkingen inzake gegevensbeheer bij het activeren van gegevens naar bestemmingen {#data-governance}

Het gegevensbeheer wordt afgedwongen voor platformbestemmingen via:

* *marketing acties* die u in creeert bestemmingswerkschema kunt selecteren;
* *het gebruiksbeleid van Gegevens* dat gegevens beperkt die bepaalde gebruiksetiketten bevatten van worden geactiveerd aan bestemmingen met bepaalde marketing acties.

Zie het Beleid van Gegevens in de documentatie van het Platform voor meer informatie over [ marketing acties ](../data-governance/policies/overview.md) en [ het oplossen van de schendingen van het gegevensbeleid ](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in Platform voor meer informatie over het selecteren van marketingacties in de workflow voor het maken van doelen:

* [Advertising-bestemmingen - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Advertising-bestemmingen - Google-advertenties](./catalog/advertising/google-ads-destination.md)
* [Advertising-doelen - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Opslagdoelen voor cloud](./catalog/cloud-storage/overview.md)
* [E-mailmarketingdoelen](./catalog/email-marketing/overview.md)
* [Sociale bestemmingen](./catalog/social/overview.md)

Zie de stap **[!UICONTROL Review]** in de volgende handleidingen voor meer informatie over schendingen van het gegevensbeleid in de workflow voor publiekactivering:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](./ui/activate-segment-streaming-destinations.md#review)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](./ui/activate-streaming-profile-destinations.md#review)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](./ui/activate-batch-profile-destinations.md#review)

## Voorwaarden en bepalingen {#terms-and-conditions}

Door om het even welke Doelen te gebruiken die als bèta (&quot;Beta&quot;) worden geëtiketteerd, bevestigt u hierbij dat Beta ***&quot;zoals is&quot;zonder enige garantie van welke aard*** wordt verstrekt.

Adobe is niet verplicht de Beta te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden informatief te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke Beta en/of begeleidende materialen. De Beta wordt beschouwd als vertrouwelijke informatie over Adobe.

Elke &quot;feedback&quot; (informatie over de Beta, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de Beta, suggesties, verbeteringen en aanbevelingen) die u aan de Adobe verstrekt, wordt toegewezen aan de Adobe, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.