---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2025
description: Aanvullende informatie voor Adobe Experience Platform van februari 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 22%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Deze versie omvat verbeteringen aan de Federated Audience Composition toe:voegen-on. Voor meer informatie, lees de [ Federated de versiedetecten van de Samenstelling van het publiek ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes).

**Releasedatum: woensdag 18 februari 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [AI-assistent](#ai-assistant)
- [Catalogusservice](#catalog-service)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Bronnen](#sources)
- [Documentatie-updates](#documentation-updates)
   - [Edge-netwerk- en hubvergelijking](#edge)
   - [Uitgebreide Flow Service API voor bronnen](#flow-service)
   - [Back-ups maken van objectconfiguraties met behulp van sandboxgereedschappen](#back-up-object-configurations)
   - [Een expertisecentrum inschakelen met behulp van sandboxgereedschappen](#center-of-excellence)
   - [De Dataset van de Gebeurtenis van de ervaring Behoud in het gegevenspeer](#experience-event-dataset-retention)

## AI-assistent {#ai-assistant}

AI-assistent in Adobe Experience Platform is een gesprekservaring waarmee u uw workflows in Adobe-applicaties kunt versnellen. Met AI-assistent krijgt u meer inzicht in productkennis, kunt u problemen oplossen of informatie doorzoeken en operationele inzichten verkrijgen. AI Assistant ondersteunt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor automatisch aanvullen van vragen | Als u een vraag naar AI Assistant invoegt, kunt u een keuze maken uit een lijst met aanbevolen vragen die door AI Assistant worden geboden. Gebruik deze functie om uw workflows met AI Assistant verder te versnellen. Voor meer informatie, lees de gids op [ gebruikend vraag autocomplete met AI Medewerker ](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Ondersteuning voor de waarneming van gegevenssets | U kunt AI Medewerker nu gebruiken om vragen over specifieke datasetmetriek zoals opslaggrootte en rijaantallen te beantwoorden. Vragen over gegevenswaarneming ondersteunen kwalificatietoetsen die u kunt gebruiken om query&#39;s te filteren op een bepaalde tijdsperiode. Voor meer informatie, lees de [ AI Medewerker de vraaggids ](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Voor meer informatie, lees het [ AI Hulpoverzicht ](../../ai-assistant/home.md).

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Nieuw API-eindpunt | Beheer efficiënter uw gegevens van de dataset van Adobe Experience Platform met de nieuwe [ Dienst API /v2/dataSets/{DATASET_ID} eindpunt ](../../catalog/api/update-object.md#patch-v2-notation) van de Catalogus. Werk eenvoudig complexe, diep genestelde datasetattributen bij aangezien het systeem automatisch ontbrekende wegniveaus creeert om u tijd te besparen, handstappen te verminderen, en fouten te minimaliseren. |

{style="table-layout:auto"}

Voor meer informatie over de Dienst van de Catalogus, lees het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Gebruik gegevensvoorbereiding om gegevens toe te wijzen, te transformeren en te valideren van en naar Experience-datamodel (XDM).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde ondersteuning voor het importeren en exporteren van toewijzingen | U kunt nu toewijzingen exporteren naar een CSV-bestand en ze lokaal configureren op een spreadsheet. U kunt uw bijgewerkte toewijzingen vervolgens naar Experience Platform importeren met de toewijzingsinterface in de gebruikersinterface. U kunt dit vermogen gebruiken om grote aantallen afbeeldingen te vormen zonder het moeten hen manueel in UI bouwen. Bovendien kunt u bij het maken van een nieuwe gegevensstroom een kopie van uw toewijzingen rechtstreeks uploaden naar Experience Platform om uw workflow te versnellen. Voor meer informatie, lees de gids over [ het invoeren en het uitvoeren van afbeeldingen ](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Voor meer informatie, lees het [ Overzicht van de Prep van Gegevens ](../../data-prep/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [ (Beta) Marketo Engage Person Sync ](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Gebruik de [!DNL Marketo Engage Person Sync] -connector om updates te streamen van het persoonlijke publiek naar de corresponderende records in uw [!DNL Marketo Engage] -instantie. Deze bestemmingsschakelaar is in bèta en slechts beschikbaar om klanten te selecteren. Neem contact op met uw Adobe-vertegenwoordiger als u toegang wilt aanvragen. |
| [ De verbinding van CRM van het Handelsbureau ](/help/destinations/catalog/advertising/tradedesk-emails.md) algemene beschikbaarheid | De verbinding met [!DNL The Trade Desk CRM] is nu over het algemeen beschikbaar. Gebruik [!DNL The Trade Desk] CRM-bestemming om profielen te activeren voor uw [!DNL Trade Desk] -account voor publiek dat zich richt op en onderdrukt op basis van CRM-gegevens. |
| [ RainFocus de Verbinding van Profielen van de Deelnemer ](/help/destinations/catalog/marketing-automation/rainfocus.md) | Gebruik de bestemming [!DNL RainFocus Attendee Profiles] om klantprofielen vanuit Adobe Experience Platform te streamen naar het [!DNL RainFocus] -platform om deelnemerprofielen te maken en bij te werken. |
| ](/help/destinations/catalog/advertising/criteo.md) algemene beschikbaarheid van de verbinding van 0} Criteo[ | De [!DNL Criteo] -verbinding is nu over het algemeen beschikbaar. Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. Met &#39;s werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken. |
| [[!DNL Amazon Ads]  verbinding ](../../destinations/catalog/advertising/amazon-ads.md) | De [!DNL Amazon Ads] -connector, voorheen in bèta, is nu over het algemeen beschikbaar. De aansluiting is ook bijgewerkt om een signaal te verzenden dat toestemming geeft voor alle profielen die ermee hebben ingestemd dat hun persoonsgegevens voor reclame worden gebruikt. Lees meer over de nieuwe ](../../destinations/catalog/advertising/amazon-ads.md#destination-details) controle van het Signaal van de Toestemming van Amazon [. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| De toegangslabels van het gebruik om gebruikerstoegang tot bestemmingsdataflows te beheren | Als deel van de [[!UICONTROL attribute-based access control]](/help/access-control/abac/overview.md) functionaliteit in Real-Time CDP, kunt u toegangslabels op [ bestemmingsdataflows ](/help/dataflows/ui/monitor-destinations.md) nu toepassen. Op deze manier kunt u ervoor zorgen dat alleen een subset van gebruikers in uw organisatie toegang krijgt tot specifieke doelgegevens. <br> **Belangrijk**: Wanneer het zoeken naar bestemmingsdataflows gebruikend de onderzoeksdoos bij de bovenkant van het gebruikersinterface van Experience Platform, kunnen de resultaten bestemmingsdataflows omvatten die uw etiketten van de gebruikerstoegang u van het zien beperken. Dit gedrag wordt in een toekomstige update gecorrigeerd. |
| [ publiek-niveau die ](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) voor de [ verbinding van Marketo Engage ](/help/destinations/catalog/adobe/marketo-engage.md) melden | U kunt [ informatie ](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) over de geactiveerde, uitgesloten, of ontbroken identiteiten nu bekijken die op een publieksniveau, voor elk publiek worden verdeeld dat deel van de dataflows voor deze bestemming uitmaakt. |
| De externe publiekssteun voor [ TikTok ](/help/destinations/catalog/social/tiktok.md) en [ Breuk Inc ](/help/destinations/catalog/advertising/snap-inc.md) verbindingen | U kunt extern publiek aan deze bestemmingen van [ douane activeren uploadt ](../../segmentation/ui/audience-portal.md#import-audience) en [ Federatieve Samenstelling van het Publiek ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

**Correcties en verhogingen** {#destinations-fixes-and-enhancements}

- Een probleem met de Destination SDK-testgereedschappen is opgelost. Sommige klanten of partners kwamen kwesties met het [ hulpmiddel van de de generatie van het steekproefprofiel ](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) toe te schrijven aan een niet gestaafd formaat wanneer het schema dat voor het produceren van profielen werd gebruikt gegevenstypes met a `No format` selecteur omvatte.
- Een probleem met het bijwerken van de `targetConnection` -specificatie van doelen met de Flow Service API is opgelost. In sommige gevallen zou de PATCH-bewerking zich op dezelfde manier gedragen als een POST-bewerking, waardoor bestaande gegevensstromen zouden worden beschadigd. Dit probleem is nu opgelost en alle klanten kunnen de Flow Service API gebruiken om hun `targetConnection` specificatie bij te werken. [Meer informatie](/help/destinations/api/edit-destination.md#patch-target-connection).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor weergaven in [!DNL Microsoft Dynamics] | U kunt nu `"entityType": "view"` invoeren wanneer u de [!DNL Microsoft Dynamics] -bron gebruikt. Voor meer informatie, lees de gids op [ verbindend a  [!DNL Microsoft Dynamics]  bron met Experience Platform ](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).

## Documentatie-updates {#documentation-updates}

### Edge Network- en hubvergelijking {#edge}

De [ Edge Network en hubvergelijking ](../../landing/edge-and-hub-comparison.md) verstrekt een overzicht die de verschillen tussen de twee servertypes voor Adobe Experience Platform (hub en Edge Network) specificeren, met inbegrip van welke diensten op elk servertype, plaatsen van de servers, evenals geadviseerde scenario&#39;s voor het gebruiken van elk servertype beschikbaar zijn.

### Uitgebreide Flow Service API-referentie voor bronnen {#flow-service}

De [[!DNL Flow Service]  API verwijzing ](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) voor bronnen is bijgewerkt met nieuwe API verzoek en reactievoorbeelden. Gebruik de uitgebreide API-referentie om verbindingsspecificaties te maken en bij te werken wanneer u uw eigen bron integreert met Experience Platform. U kunt de uitgebreide API verwijzing ook gebruiken om statusovergangen op uw bronentiteiten uit te voeren, bestaande bron en doelverbindingen bij te werken, en stromen en stroomspecificaties terug te winnen gegeven een specifieke het filtreren criteria.

### Back-ups maken van objectconfiguraties met behulp van sandboxgereedschappen {#back-up-object-configurations}

Lees de [ gids van de de hulpobjecten configuratie ](../../sandboxes/use-cases/backup-object-configuration.md) voor geleidelijke instructies bij het creëren van een reservepakket gebruikend zandbakhulpmiddel om uw objecten configuraties te verzekeren wordt opgeslagen en beveiligd.

### Een expertisecentrum inschakelen met behulp van sandboxgereedschappen {#center-of-excellence}

Lees het [ centrum van topgids ](../../sandboxes/use-cases/center-of-excellence.md) voor geleidelijke instructies bij het creëren van een &quot;gouden zandbak&quot;pakket dat als centrum van uitmuntendheid dienst doet om zeer belangrijke configuraties efficiënt te delen.

### De Dataset van de Gebeurtenis van de ervaring Behoud in het gegevenspeer {#experience-event-dataset-retention}

Neem controle over het bewaren van de Dataset van de Gebeurtenis in Adobe Experience Platform gebruikend tijd-aan-Levend (TTL). [ deze gids ](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) loopt u door het evalueren van, het vormen van, en het beheren van de montages van TTL om verouderde verslagen automatisch te verwijderen, opslag te optimaliseren, en uw gegevens relevant te houden. Ontdek best practices, praktijkvoorbeelden en belangrijke overwegingen om uw levenscyclusbeheer van gegevens te verbeteren.
