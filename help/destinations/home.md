---
title: Overzicht van doelen
description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 3%

---

# [!DNL Destinations]-overzicht {#overview}

![&#x200B; de overzichtsbanner van Doelen.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Experience Platform is het opnemen van uw gegevens van de eerste partij en het activeren ervan voor uw bedrijfsbehoeften. Gebruik [&#x200B; bronnen &#x200B;](../sources/home.md) om gegevens in Experience Platform en bestemmingen in te voeren om gegevens van Experience Platform uit te voeren.

## Doelstappen {#steps}

* Kies van a [&#x200B; zelfbedieningencatalogus &#x200B;](./catalog/overview.md) van alle bestemmingen beschikbaar in Experience Platform.
* Gebruik bestemmingen om publiek of datasets naar de platforms van de marketing automatisering, digitale reclameplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

De controles in de [&#x200B; werkruimte van bestemmingen &#x200B;](./ui/destinations-workspace.md) staan u toe:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel Experience Platform aan de account op het doelplatform.
* Selecteer welk publiek of welke datasets voor bestemmingen moeten worden geactiveerd;
* Selecteer welke [&#x200B; gebieden van de Gegevens van de Ervaring Model (XDM) &#x200B;](../xdm/home.md) om te exporteren wanneer het activeren van publiek aan bepaalde bestemmingen zoals e-mail marketing bestemmingen, de platforms van CRM, de plaatsen van de wolkenopslag, en meer.
* Activeer verschillende soorten profielen en publiek aan bestemmingen - mensen, rekeningen, en vooruitzichten.

## Doeltypen en -categorieën {#types-and-categories}

Met Experience Platform kunt u gegevens activeren voor verschillende soorten doelen, zodat u tevreden bent met de gebruiksproblemen bij activering. De bestemmingen variëren van op API-Gebaseerde integratie, tot integratie met dossierontvangstsystemen, de bestemmingen van de profielraadpleging, en meer. Voor gedetailleerde informatie over alle beschikbare bestemmingen, lees de [&#x200B; bestemmingstypes en de categorieën overzicht &#x200B;](./destination-types.md).

## Door Adobe gebouwde en door partners gebouwde bestemmingen {#adobe-and-partner-built-destinations}

Sommige schakelaars in de de bestemmingscatalogus van Experience Platform worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerbedrijven worden gebouwd en worden gehandhaafd gebruikend [&#x200B; Destination SDK &#x200B;](/help/destinations/destination-sdk/overview.md). Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bestemming door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld, wordt de [&#x200B; schakelaar van Amazon S3 &#x200B;](/help/destinations/catalog/cloud-storage/amazon-s3.md) gecreeerd door Adobe, terwijl de [&#x200B; schakelaar van TikTok &#x200B;](/help/destinations/catalog/social/tiktok.md) door het team van TikTok wordt gecreeerd en gehandhaafd.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door Adobe ontworpen en onderhouden connectors contact op met uw Adobe-vertegenwoordiger of de klantenservice.

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Experience Platform werkt met Adobe Experience Platform toegangsbeheertoestemmingen. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Voor informatie over de individuele toestemmingen, ga naar [&#x200B; toegangsbeheer in Adobe Experience Platform &#x200B;](../access-control/home.md) en rol neer aan de lijst bij de bodem van de pagina.

De volgende lijst schetst de toestemmingen en toestemmingscombinaties die worden vereist om bepaalde acties op bestemmingen uit te voeren.

| Machtigingsniveau | Beschrijving |
| ---- | ---- |
| **[!UICONTROL View Destinations]** | Om tot het bestemmingslusje in Experience Platform UI toegang te hebben, hebt u de **[!UICONTROL View Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]** | Om met bestemmingen te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]** , **[!UICONTROL Activate Destinations]** , **[!UICONTROL View Profiles]** en **[!UICONTROL View Segments]** | Om publiek aan bestemmingen te activeren en de [&#x200B; toewijzingsstap &#x200B;](ui/activate-batch-profile-destinations.md#mapping) van het werkschema toe te laten, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]** , **[!UICONTROL Activate Segments without Mapping]** , **[!UICONTROL View Profiles]** en **[!UICONTROL View Segments]** | Om publiek van bestaande dataflows toe te voegen of te verwijderen zonder toegang tot de [&#x200B; toewijzingsstap &#x200B;](ui/activate-batch-profile-destinations.md#mapping) van het werkschema te hebben, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage and Activate Dataset Destinations]** | Om datasets naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. |
| **[!UICONTROL View Identity Graph]** | Om *identiteiten* naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Het diagram hieronder toont visueel welke toestemmingen u afhankelijk van de verrichtingen nodig hebt die u op bestemmingen wilt uitvoeren.

![&#x200B; Diagram die de vereiste toestemmingen tonen om bepaalde acties op bestemmingen uit te voeren.](/help/destinations/assets/overview/permissions-diagram.png)

Voor meer informatie over toegangscontroles, zie de [&#x200B; handleiding van de controlegebruiker van de Toegang &#x200B;](../access-control/ui/overview.md).

### Op kenmerken gebaseerd toegangsbeheer voor bestemmingen {#attribute-based-access}

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens naar een bestemming uitvoeren als u geen toegang tot alle gebieden in de dataset hebt.

Voor meer informatie over hoe de bestemmingen met op attribuut-gebaseerde toegangscontroles werken, lees het [&#x200B; op attribuut-gebaseerde overzicht van de toegangscontrole &#x200B;](../access-control/abac/overview.md#destinations).

## Profiel verwijderen van doelen {#profile-removal}

Wanneer een profiel wordt verwijderd uit een publiek dat aan een bestemming wordt geactiveerd, wordt dat profiel ook verwijderd uit het overeenkomstige publiek in het bestemmingsplatform. Als bijvoorbeeld een profiel wordt verwijderd uit een publiek dat eerder is geactiveerd voor LinkedIn, wordt dat profiel verwijderd uit de gekoppelde [!UICONTROL LinkedIn Matched Audience] .

Profielverwijdering van bestemmingen — ook wel segmentatie genoemd — vindt plaats op hetzelfde moment als segmentatie. Zodra een profiel uit een publiek in Experience Platform wordt verwijderd, weerspiegelt de volgende geplande gegevensstroom aan de bestemming die verandering en verwijdert het profiel uit het bestemmingspubliek.

De werkelijke snelheid waarmee de profielverwijdering van kracht wordt op het doelplatform, kan variëren afhankelijk van de opname en het verwerkingsgedrag van de bestemming.

## Controle van de bestemmingen {#destinations-monitoring}

Nadat u een verbinding met een doel hebt gemaakt en de activeringsworkflow hebt voltooid, kunt u de gegevens die u exporteert naar uw ontvangstsysteem controleren. Lees de [&#x200B; gids bij het controleren van dataflows aan bestemmingen in UI &#x200B;](/help/dataflows/ui/monitor-destinations.md) voor meer informatie.

![&#x200B; Doelen die paginavoorbeeld controleren.](./assets/overview/monitoring-page-example.png)

U kunt ook controleren of gegevens naar uw bestemming zijn gekomen. De meeste pagina&#39;s van de bestemmingsdocumentatie in de catalogus hebben de sectie van de a *de uitvoer van gegevens* bevestigen, die erop wijst hoe u in het bestemmingsplatform kunt controleren dat het gegeven met succes van Experience Platform wordt gebracht. Bekijk een voorbeeld van deze sectie voor de [&#x200B; bestemming van de Advertentie van Amazon &#x200B;](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Beperkingen inzake gegevensbeheer bij het activeren van gegevens naar bestemmingen {#data-governance}

Het gegevensbeheer wordt afgedwongen voor Experience Platform-bestemmingen via:

* *marketing acties* die u in creeert bestemmingswerkschema kunt selecteren;
* *het gebruiksbeleid van Gegevens* dat gegevens beperkt die bepaalde gebruiksetiketten bevatten van worden geactiveerd aan bestemmingen met bepaalde marketing acties.

Zie het Beleid van Gegevens in de documentatie van Experience Platform voor meer informatie over [&#x200B; marketing acties &#x200B;](../data-governance/policies/overview.md) en [&#x200B; het oplossen van de schendingen van het gegevensbeleid &#x200B;](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in Experience Platform voor meer informatie over het selecteren van marketingacties in de workflow voor het maken van doelen:

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

Adobe is niet verplicht de Beta te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden informatief te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke Beta en/of begeleidende materialen. De Beta wordt beschouwd als vertrouwelijke informatie van Adobe.

Alle &quot;Feedback&quot; (informatie over de Beta, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de Beta, suggesties, verbeteringen en aanbevelingen) die u aan Adobe verstrekt, worden hierbij aan Adobe toegewezen, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.