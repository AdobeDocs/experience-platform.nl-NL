---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2025
description: Aanvullende informatie voor Adobe Experience Platform van februari 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c4064771a384a90d94903ba1761fc9ee20f47747
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 92%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Deze release bevat verbeteringen aan de add-on Samenstelling van Federated-doelgroep. Raadpleeg voor meer informatie de [aanvullende informatie over Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes).

**Releasedatum: 18 februari 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [AI-assistent](#ai-assistant)
- [Catalogusservice](#catalog-service)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Bronnen](#sources)
- [Segmentatieservice](#segmentation)
- [Documentatie-updates](#documentation-updates)
   - [Edge network- en hubvergelijking](#edge)
   - [Uitgebreide Flow Service API voor bronnen](#flow-service)
   - [Back-ups maken van objectconfiguraties met behulp van sandbox-tools](#back-up-object-configurations)
   - [Een expertisecentrum inschakelen met behulp van sandbox-tools](#center-of-excellence)
   - [Retentie dataset Experience-gebeurtenis in data lake](#experience-event-dataset-retention)

## AI-assistent {#ai-assistant}

AI-assistent in Adobe Experience Platform is een gesprekservaring waarmee u uw workflows in Adobe-applicaties kunt versnellen. Met AI-assistent krijgt u meer inzicht in productkennis, kunt u problemen oplossen of informatie doorzoeken en operationele inzichten verkrijgen. AI-assistent biedt ondersteuning voor Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van operationele inzichten | De operationele inzichten in AI-assistent bevinden zich nu in GA. Operationele inzichten zijn antwoorden die de AI-assistent genereert over uw metadata-objecten (attributen, doelgroepen, gegevensstromen, datasets, bestemmingen, trajecten, schema&#39;s en bronnen), waaronder aantallen, opzoekacties en impact van herkomst. Operationele inzichten kijkt niet naar gegevens in de sandbox. Voor meer informatie, raadpleegt u de [handleiding voor de gebruikersinterface van de AI-assistent](../../ai-assistant/ui-guide.md). |
| Ondersteuning voor automatisch aanvullen van vragen | Als u een vraag aan AI-assistent stelt, kunt u nu kiezen uit een lijst met aanbevolen vragen die AI-assistent biedt. Gebruik deze functie om uw workflows met AI-assistent verder te versnellen. Voor meer informatie, raadpleegt u de handleiding over [het automatisch aanvullen van vragen met de AI-assistent](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Ondersteuning voor de waarneming van datasets | U kunt nu AI-assistent gebruiken om vragen te beantwoorden over specifieke dataset-statistieken, zoals opslaggroottes en rijaantallen. Vragen over de observatie van gegevens ondersteunen kwalificaties waarmee u uw query&#39;s kunt filteren op een bepaalde periode. Voor meer informatie, raadpleegt u de [vragenhandleiding voor AI-assistent](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van de AI-assistent](../../ai-assistant/home.md).

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Nieuw API-eindpunt | Beheer de metadata van uw Adobe Experience Platform-dataset efficiënter met het nieuwe [eindpunt Catalogusservice-API /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). U kunt eenvoudig complexe, diep geneste datasetkenmerken bijwerken, omdat het systeem automatisch ontbrekende padniveaus maakt. Zo bespaart u tijd, beperkt u het aantal handmatige stappen en minimaliseert u fouten. |

{style="table-layout:auto"}

Voor meer informatie over de catalogusservice, raadpleegt u het [Overzicht van de Catalogusservice](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Gebruik gegevensvoorbereiding om gegevens toe te wijzen, te transformeren en te valideren van en naar Experience-datamodel (XDM).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde ondersteuning voor het importeren en exporteren van toewijzingen | U kunt nu toewijzingen exporteren naar een CSV-bestand en ze lokaal configureren op een spreadsheet. U kunt uw bijgewerkte toewijzingen vervolgens naar Experience Platform importeren met de toewijzingsinterface in de gebruikersinterface. U kunt dit vermogen gebruiken om grote aantallen toewijzingen te configureren zonder dat u ze handmatig in de gebruikersinterface hoeft samen te stellen. Wanneer u een nieuwe gegevensstroom maakt, kunt u bovendien een kopie van uw toewijzingen rechtstreeks naar Experience Platform uploaden om uw workflow te versnellen. Voor meer informatie, raadpleegt u de handleiding voor [het importeren en exporteren van toewijzingen](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [Overzicht van Gegevensvoorbereiding](../../data-prep/home.md).

## Doelen (bijgewerkt op 20 februari) {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Gebruik de [!DNL Marketo Engage Person Sync]-connector om updates te streamen van persoonsdoelgroepen naar de corresponderende records in uw [!DNL Marketo Engage]-instantie. Deze bestemmingsconnector bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen. |
| [De Trade Desk CRM-verbinding](/help/destinations/catalog/advertising/tradedesk-emails.md) algemene beschikbaarheid | [!DNL The Trade Desk CRM]-verbinding is nu algemeen beschikbaar. Gebruik de CRM-bestemming [!DNL The Trade Desk] om profielen voor uw [!DNL Trade Desk]-account te activeren voor doelgroeptargeting en -onderdrukking op basis van CRM-gegevens. |
| [RainFocus Attendee Profiles-verbinding](/help/destinations/catalog/marketing-automation/rainfocus.md) | Gebruik de bestemming [!DNL RainFocus Attendee Profiles] om klantprofielen van Adobe Experience Platform naar het [!DNL RainFocus]-platform te streamen om deelnemersprofielen te maken en bij te werken. |
| [Criteo-verbinding](/help/destinations/catalog/advertising/criteo.md) algemene beschikbaarheid | De [!DNL Criteo]-verbinding is nu algemeen beschikbaar. Criteo maakt betrouwbare en effectieve reclame mogelijk om elke consument op het open internet een rijkere ervaring te bieden. Met &#39;s werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk contactpunt tijdens het winkeltraject gepersonaliseerd is om klanten op het juiste moment met de juiste advertentie te bereiken. |
| [[!DNL Amazon Ads] verbinding](../../destinations/catalog/advertising/amazon-ads.md) | De [!DNL Amazon Ads]-connector, voorheen in bèta, is nu algemeen beschikbaar. De connector is ook bijgewerkt om een &#x200B;&#x200B;toestemmingssignaal te versturen naar alle profielen die toestemming hebben gegeven voor het gebruik van hun persoonlijke gegevens voor advertenties. Meer informatie over het nieuwe besturingselement [Amazon Ads Consent Signal](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| Toegangslabels gebruiken om gebruikerstoegang tot bestemmingsgegevensstromen te beheren | Als deel van de [[!UICONTROL attribute-based access control]](/help/access-control/abac/overview.md)-functionaliteit in Real-Time CDP, kunt u nu toegangslabels op [bestemmingsgegevensstromen](/help/dataflows/ui/monitor-destinations.md) toepassen. Op deze manier kunt u ervoor zorgen dat alleen een subset van gebruikers in uw organisatie toegang krijgt tot specifieke bestemmingsgegevensstromen. <br> **Belangrijk**: Wanneer u met behulp van het zoekvak boven aan de gebruikersinterface van Experience Platform naar bestemmingsgegevensstromen zoekt, kunnen de resultaten bestemmingsgegevensstromen bevatten die u niet kunt zien vanwege uw gebruikerstoegangslabels. Dit gedrag wordt in een toekomstige update gecorrigeerd. |
| [Rapportage op doelgroepniveau](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) voor de [Marketo Engage-verbinding](/help/destinations/catalog/adobe/marketo-engage.md) | U kunt nu [informatie weergeven](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) over de geactiveerde, uitgesloten of mislukte identiteiten, uitgesplitst op doelgroepniveau, voor elke doelgroep die deel uitmaakt van de gegevensstromen voor deze bestemming. |
| Ondersteuning voor externe doelgroepen voor de verbindingen [TikTok](/help/destinations/catalog/social/tiktok.md) en [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | U kunt externe doelgroepen activeren voor deze bestemmingen vanuit [aangepaste uploads](../../segmentation/ui/audience-portal.md#import-audience) en [samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/start/audiences). |
| Arrays, kaarten en objecten exporteren naar cloudopslagdoelen | Door de nieuwe **[!UICONTROL Export arrays, maps, objects]** -schakeloptie te gebruiken wanneer u verbinding maakt met een bestemming voor cloudopslag, kunt u nieuwe complexe objecten exporteren om doelen te selecteren. [Meer informatie](/help/destinations/ui/export-arrays-calculated-fields.md) over de nieuwe functionaliteit. |

{style="table-layout:auto"}

**Opgeloste problemen en verbeteringen** {#destinations-fixes-and-enhancements}

- Een probleem met de Destination SDK-testtools is opgelost. Sommige klanten of partners ondervonden problemen met de [tool voor het genereren van voorbeeldprofielen](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) vanwege een niet-ondersteunde indeling wanneer het schema dat werd gebruikt voor het genereren van profielen gegevenstypen met een `No format`-selector bevatte.
- Een probleem met het bijwerken van de `targetConnection`-specificatie van bestemmingen met de Flow Service API is opgelost. In sommige gevallen gedroeg de PATCH-bewerking zich op een manier die vergelijkbaar is met een POST-bewerking, waardoor bestaande gegevensstromen beschadigd raken. Dit probleem is nu opgelost en alle klanten kunnen de Flow Service API gebruiken om hun `targetConnection`-specificatie bij te werken. [Meer informatie](/help/destinations/api/edit-destination.md#patch-target-connection).
- Wanneer u profielen exporteert naar op een bestand gebaseerde doelen, zorgt deduplicatie ervoor dat slechts één profiel wordt geëxporteerd wanneer meerdere profielen dezelfde deduplicatietoets en dezelfde tijdstempel hebben. Deze release bevat een update van het deduplicatieproces, waarbij ervoor wordt gezorgd dat opeenvolgende uitvoeringen met dezelfde coördinaten altijd dezelfde resultaten opleveren, hetgeen de consistentie ten goede komt. [Meer informatie](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Blijvende splitsing | Audience Composition ondersteunt nu permanente splitsingen. U kunt uw gesplitste publiek constant laten blijven wanneer het verdelen door profiel door een identiteitsnamespace aan uw Gesplitste blok toe te voegen. Meer informatie over deze eigenschap kan in de [ documentatie van de Samenstelling van het Publiek ](../../segmentation/ui/audience-composition.md) worden gevonden. |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor weergaven in [!DNL Microsoft Dynamics] | U kunt nu `"entityType": "view"` toevoegen wanneer u de [!DNL Microsoft Dynamics]-bron gebruikt. Voor meer informatie kunt u de handleiding over het [verbinden van een [!DNL Microsoft Dynamics] bron met Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md) raadplegen. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).

## Documentatie-updates {#documentation-updates}

### Edge Network- en hubvergelijking {#edge}

De [vergelijking tussen Edge Network en hub](../../landing/edge-and-hub-comparison.md) biedt een overzicht met de verschillen tussen de twee servertypen voor Adobe Experience Platform (hub en Edge Network), inclusief welke services beschikbaar zijn op elk servertype, de locaties van de servers en aanbevolen scenario&#39;s voor het gebruik van elk servertype.

### Uitgebreide Flow Service API-referentie voor bronnen {#flow-service}

De [[!DNL Flow Service] API-referentie](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) voor bronnen is bijgewerkt met nieuwe voorbeelden van API-aanvragen en -reacties. Gebruik de uitgebreide API-referentie om verbindingsspecificaties te maken en bij te werken wanneer u uw eigen bron integreert met Experience Platform. U kunt de uitgebreide API-referentie ook gebruiken om statusovergangen op uw bronentiteiten uit te voeren, bestaande bron- en doelverbindingen bij te werken, en workflows en workflowspecificaties op te halen op basis van specifieke filtercriteria.

### Back-ups maken van objectconfiguraties met behulp van sandbox-tools {#back-up-object-configurations}

Lees de [handleiding voor back-ups maken van objectconfiguratiesn](../../sandboxes/use-cases/backup-object-configuration.md) voor stapsgewijze instructies over het maken van een back-uppakket met behulp van sandbox-tools om ervoor te zorgen dat uw objectconfiguraties worden opgeslagen en beveiligd.

### Een expertisecentrum inschakelen met behulp van sandbox-tools {#center-of-excellence}

Lees de [handleiding voor het expertisecentrum](../../sandboxes/use-cases/center-of-excellence.md) voor stapsgewijze instructies voor het maken van een &#39;golden sandbox&#39;-pakket dat fungeert als een expertisecentrum om belangrijke configuraties efficiënt te delen.

### Retentie dataset Experience-gebeurtenis in data lake {#experience-event-dataset-retention}

Neem controle over het bewaren van de dataset van de Experience-gebeurtenis in Adobe Experience Platform met behulp van Time-To-Live (TTL). [Deze handleiding](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) begeleidt u bij het evalueren, configureren en beheren van TTL-instellingen om verouderde records automatisch te verwijderen, opslag te optimaliseren en uw gegevens relevant te houden. Ontdek best practices, praktijkvoorbeelden en belangrijke overwegingen om uw levenscyclusbeheer van gegevens te verbeteren.
