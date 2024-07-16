---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;gebruikershandleiding;ui-handleiding;platform ui-handleiding;introductie op platform;dashboard;
solution: Experience Platform
title: Overzicht gebruikersinterface Experience Platform
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# Handleiding Adobe Experience Platform UI

Deze gids dient als inleiding aan het gebruiken van het gebruikersinterface van Adobe Experience Platform (UI), die verklaart wat de diverse componenten worden gebruikt voor en verbindingen aan verdere documentatie voor meer informatie verstrekt.

Om meer over Adobe Experience Platform te leren, te lezen gelieve het [ overzicht van het Experience Platform ](home.md).

## Startscherm

Na het registreren in Adobe Experience Platform, bent u op de [!UICONTROL Home] pagina, die van het [ metrieke dashboard ](#metrics), [ recente gegevens ](#recent-data), en [ geadviseerde het leren ](#recommended-learning) secties wordt samengesteld.

![](images/user-guide/homepage.png)

### Metrics

Het dashboard Metrics verstrekt kaarten die u informatie over datasets, profielen, segmenten, en bestemmingen binnen uw organisatie geven.

![](images/user-guide/homepage-dashboard.png)

De sectie **[!UICONTROL Datasets]** toont het aantal datasets binnen uw organisatie. Dit aantal wordt bijgewerkt wanneer een nieuwe dataset wordt gecreeerd. Meer informatie over datasets kan in het [ overzicht van datasets ](../catalog/datasets/overview.md) worden gevonden.

In de sectie **[!UICONTROL Profiles]** wordt het totale aantal personen met profielen binnen uw organisatie weergegeven, exclusief profielfragmenten. Dit totale aantal personen vertegenwoordigt het totale adresseerbare publiek en wordt elke 24 uur bijgewerkt. Meer informatie over profielen kan in het [ overzicht van het Profiel van de Klant in real time ](../profile/home.md) worden gevonden.

In de sectie **[!UICONTROL Segments]** ziet u het totale aantal segmenten dat binnen uw organisatie is gemaakt. Dit aantal wordt bijgewerkt wanneer een nieuw segment wordt gecreeerd. Meer informatie over segmenten kan in het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) worden gevonden.

De sectie **[!UICONTROL Destinations]** toont het totale aantal doelen dat voor de organisatie is gemaakt. Dit aantal wordt bijgewerkt wanneer een nieuwe bestemming wordt gecreeerd. Meer informatie over bestemmingen kan in het [ overzicht van bestemmingen ](../destinations/home.md) worden gevonden.

### Recente gegevens

Het recente gegevensdashboard verstrekt informatie over onlangs gecreeerde datasets, bronnen, segmenten, en bestemmingen.

![](images/user-guide/homepage-recent.png)

De sectie **[!UICONTROL Recent datasets]** bevat een lijst met de vijf meest recente gegevenssets die binnen uw organisatie zijn gemaakt. Deze lijst wordt bijgewerkt telkens als een nieuwe dataset wordt gecreeerd. U kunt een dataset van de lijst selecteren om meer informatie over de gespecificeerde dataset te bekijken of **[!UICONTROL View all]** selecteren om een lijst van alle gecreeerde datasets te zien. Meer informatie over datasets kan in het [ overzicht van datasets ](../catalog/datasets/overview.md) worden gevonden.

In de sectie **[!UICONTROL Recent sources]** worden de vijf meest recente bronconnectors binnen uw organisatie weergegeven. Deze lijst wordt bijgewerkt telkens als een nieuwe bronschakelaar wordt gecreeerd. U kunt een bronverbinding selecteren in de lijst om meer informatie over de opgegeven connector weer te geven of u kunt **[!UICONTROL View all]** selecteren om een lijst met alle gemaakte bronverbindingen weer te geven. Meer informatie over bronnen kan in het [ overzicht van bronnen ](../sources/home.md) worden gevonden.

De sectie **[!UICONTROL Recent segments]** bevat een lijst met de vijf meest recente segmentdefinities binnen uw organisatie. Deze lijst wordt bijgewerkt telkens als een nieuwe segmentdefinitie wordt gecreeerd. U kunt een segmentdefinitie in de lijst selecteren om meer informatie over de opgegeven segmentdefinitie weer te geven of **[!UICONTROL View all]** selecteren om een lijst met alle gemaakte segmentdefinities weer te geven. Meer informatie over segmenten kan in het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) worden gevonden.

De sectie **[!UICONTROL Recent destinations]** bevat een lijst met de vijf laatst gemaakte doelen binnen uw organisatie. Deze lijst wordt bijgewerkt telkens wanneer een nieuwe bestemming wordt gecreeerd. U kunt een doel in de lijst selecteren om meer informatie over het opgegeven doel weer te geven of u kunt **[!UICONTROL View all]** selecteren om een lijst met alle gemaakte doelen weer te geven. Meer informatie over bestemmingen kan in het [ overzicht van bestemmingen ](../destinations/home.md) worden gevonden.

### Aanbevolen training

De sectie **[!UICONTROL Recommended learning]** bevat koppelingen naar handige documentatie die u kunt gebruiken om aan de slag te gaan met Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Bovenste navigatiebalk

De hoogste navigatiebar in Platform UI toont de organisatie u momenteel wordt ondertekend, en verstrekt verscheidene belangrijke controles.

Links op de navigatiebalk bevindt zich het Adobe Experience Platform-logo. Als u dit logo op elk gewenst moment selecteert, wordt de gebruikersinterface van het platform weer weergegeven.

![](./images/user-guide/homepage-top-nav-bar.png)

### Organisatieswitch

Het eerste punt op de rechterkant van de hoogste navigatiebar is de **schakelaar van de Organisatie**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Als u de schakeloptie selecteert, wordt een vervolgkeuzemenu geopend met organisaties waartoe u toegang hebt, indien beschikbaar. Als u naar een andere organisatie wilt overschakelen, selecteert u een vermelde optie.

### Overschakelen op toepassingen

Het volgende punt op de rechterkant van de hoogste navigatie is de **toepassingsschakelaar**, die door het ![ wordt vertegenwoordigd toepassingenschakelaar ](./images/user-guide/app-switcher-icon.png) pictogram. Wanneer u dit pictogram selecteert, kunt u schakelen tussen Adobe-toepassingen waartoe uw organisatie toegang heeft, zoals Experience Platform, Analytics, Assets en andere.

### Help

Aan het recht van de toepassingsschakelaar is de **hulp en steunmenu**, die door het ![ vraagteken/hulp ](./images/user-guide/help-icon.png) pictogram wordt vertegenwoordigd. Wanneer u dit pictogram selecteert, wordt een pop-upmenu weergegeven dat verschillende Help- en ondersteuningsbronnen bevat. Het tabblad **[!UICONTROL Help]** bevat een lijst met relevante documentatie voor de pagina die u momenteel hebt ingeschakeld. Op het tabblad **[!UICONTROL Support]** kunt u een ondersteuningsticket maken met het ondersteuningsteam voor Adoben. Op het tabblad **[!UICONTROL Feedback]** kunt u feedback over Platform verzenden naar Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Meldingen en aankondigingen

In de **berichten sectie**, die door ![ bel/Meldingen en het pictogram van Mededelingen ](images/user-guide/notification-icon.png) wordt vertegenwoordigd. Het tabblad **[!UICONTROL Notifications]** bevat belangrijke informatie over het product en andere relevante updates, terwijl op het tabblad **[!UICONTROL Announcements]** informatie over onderhoud van de service wordt weergegeven.

### Gebruikersprofiel

Het definitieve punt op de hoogste navigatiebar is de **gebruikersmontages**, die door het ![ worden vertegenwoordigd gebruikersmontages/pictogram van het Profiel van de Gebruiker ](images/user-guide/profile-icon.png). Selecteer dit pictogram om uw voorkeuren te bewerken of u af te melden.

U kunt schakelen tussen het lichte en donkere thema voor de interface van het Platform met de schakelaar die net onder uw naam en e-mail wordt gevestigd. Selecteer het gewenste thema.

![](images/theme.png)

### Sandboxes

Direct onder de bovenste navigatiebalk bevindt zich de sandboxbalk. Deze balk geeft aan welke sandbox u momenteel gebruikt voor Platform. Meer informatie over zandbakken kan in het [ overzicht van zandbakken ](../sandboxes/home.md) worden gevonden.

## Linkernavigatie {#left-nav}

De navigatie op de linkerkant van het scherm maakt een lijst van alle verschillende diensten die in de UI van het Platform worden gesteund.

Klik op het menupictogram om het linkernavigatievenster weer te geven of te verbergen.

![](images/user-guide/hidemenu.png)

U kunt de navigatie op de open positie vergrendelen door nogmaals te klikken nadat u het deelvenster hebt weergegeven.

>[!IMPORTANT]
>
>Op de linkernavigatiebalk ziet u alleen de functies waartoe u toegang hebt. In eerdere versies van Adobe Experience Platform werden niet-beschikbare items uitgeschakeld. Neem contact op met de systeembeheerder als u van mening bent dat u toegang moet hebben tot een sectie die niet wordt weergegeven.

![](images/user-guide/homepage-left.png)

Met de sectie **[!UICONTROL Home]** kunt u terugkeren naar de startpagina van de gebruikersinterface van het platform.

De sectie **[!UICONTROL Workflows]** bevat een lijst met meerstapsworkflows voor het uitvoeren van bewerkingen binnen het platform. Meer informatie over werkschema&#39;s kan in het [ overzicht van werkschema&#39;s ](./workflows.md) worden gevonden.

### [!UICONTROL Connections]

Met de sectie **[!UICONTROL Sources]** kunt u bronverbindingen maken, bijwerken en verwijderen, zodat u gegevens van externe bronnen kunt opnemen in Platform. Meer informatie over bronnen kan in het [ overzicht van bronnen ](../sources/home.md) worden gevonden.

Met de sectie **[!UICONTROL Destinations]** kunt u doelen maken, bijwerken en verwijderen, zodat u gegevens van Platform naar veel externe doelen kunt exporteren. Meer informatie over bestemmingen kan in het [ overzicht van bestemmingen ](../destinations/home.md) worden gevonden.

### [!UICONTROL Customer]

In de sectie **[!UICONTROL Profiles]** kunt u door klantprofielen bladeren, profielmetriek bekijken, samenvoegbeleid maken en beheren en vakbondsschema&#39;s weergeven. Meer over het gebruiken van de [!UICONTROL Profiles] sectie leren, gelieve de [[!DNL Profile]  gebruikersgids ](../profile/ui/user-guide.md) te lezen. Meer informatie over het Profiel van de Klant in real time kan in het [ Real-Time overzicht van het Profiel van de Klant ](../profile/home.md) worden gevonden.

In de sectie **[!UICONTROL Audiences]** kunt u segmentdefinities maken en beheren. Om meer over het gebruiken van de [!UICONTROL Audiences] sectie te leren, te lezen gelieve de [ gids van de segmentatiegebruiker ](../segmentation/ui/overview.md). Meer informatie over de Dienst van de Segmentatie kan in het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) worden gevonden.

Met de sectie **[!UICONTROL Identities]** kunt u naamruimten maken en beheren. Voor meer informatie over de [!UICONTROL Identities] sectie, met inbegrip van informatie over identiteit namespaces en hoe te om identiteiten in het Platform UI te gebruiken, gelieve te verwijzen naar het [ overzicht van identiteitskaart namespace ](../identity-service/features/namespaces.md).

### [!UICONTROL Privacy]

In de sectie **[!UICONTROL Policies]** kunt u beleid voor gegevensgebruik maken en beheren. Om meer over het gebruiken van de sectie van het Beleid te leren, te lezen gelieve de [ gebruikersgids van het gegevensgebruiksbeleid ](../data-governance/policies/user-guide.md). Meer informatie over het beleid van het gegevensgebruik kan in het [ overzicht van het beleid van het gegevensgebruik ](../data-governance/policies/overview.md) worden gevonden.

In de sectie **[!UICONTROL Requests]** kunt u privacyverzoeken maken en beheren. U moet zijn gevoegd op lijst van gewenste personen om toegang te hebben tot de gebruikersinterface van de Privacy Service. Om meer over het gebruiken van de sectie van Verzoeken te leren, te lezen gelieve de [ gebruikersgids van de Privacy Service ](../privacy-service/ui/user-guide.md). Meer informatie over Privacy Service kan in het [ overzicht van de Privacy Service ](../privacy-service/home.md) worden gevonden.

### [!UICONTROL Data Science]

De sectie **[!UICONTROL Notebooks]** biedt toegang tot JupyterLab, een interactieve ontwikkelomgeving waarmee u uw gegevens kunt verkennen, analyseren en modelleren. Om meer over het gebruiken van de sectie van Notities te leren, te lezen gelieve de [ JupyterLab gebruikersgids ](../data-science-workspace/jupyterlab/overview.md). Meer informatie over de Wetenschap van Gegevens Workspace kan in het [ overzicht van Workspace van de Wetenschap van Gegevens ](../data-science-workspace/home.md) worden gevonden

Met de sectie **[!UICONTROL Models]** kunt u leren van machines en kunstmatige intelligentie gebruiken om modellen te maken, te ontwikkelen, te trainen en af te stemmen om voorspellingen te maken. Meer informatie over de sectie van Modellen kan in het leerprogramma op [ opleiding worden gevonden en een model ](../data-science-workspace/models-recipes/train-evaluate-model-ui.md) evalueren.

Met de sectie **[!UICONTROL Services]** kunt u uw gepubliceerde modellen voor geplande training en scoring beheren, of de Intelligente services van de Adobe gebruiken, een set AI-services die realtime persoonlijke klantervaringen bieden. Meer informatie over de sectie van de Diensten kan in [ worden gevonden het Publiceren van een Model als leerprogramma van de Dienst ](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

Met de sectie **[!UICONTROL Schemas]** kunt u XDM-schema&#39;s (Experience Data Model) maken en beheren. Om meer over schema&#39;s te leren, te lezen gelieve het leerprogramma op [ creërend een schema ](../xdm/tutorials/create-schema-ui.md). Meer informatie over XDM kan in het [ XDM overzicht van het Systeem ](../xdm/home.md) worden gevonden.

Met de sectie **[!UICONTROL Datasets]** kunt u gegevenssets maken en beheren. De meer informatie over datasets kan in de [ gids van de datasetgebruiker ](../catalog/datasets/user-guide.md) worden gevonden.

In de sectie **[!UICONTROL Queries]** kunt u query&#39;s maken en beheren, SQL-query&#39;s van Adobe Experience Platform Query Service registreren en uw [!DNL PostgreSQL] -referenties bekijken. Meer informatie over vragen kan in de [ gebruikersgids van de Dienst van de Vraag ](../query-service/ui/overview.md) worden gevonden.

In de sectie **[!UICONTROL Monitoring]** kunt u de opname via batches en streaming controleren. Meer informatie over controle kan in de [ controle gegevens worden gevonden gebruikershandleiding ](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Adobe Journey Optimizer is een toepassingsservice die boven op het Experience Platform is gebouwd. Het staat u toe om krachtige beslissingstechnologieën te gebruiken om de beste aanbieding en ervaring aan uw klanten over alle aanrakingspunten op het juiste ogenblik te leveren. Meer over Journey Optimizer leren, met inbegrip van het werken met [!UICONTROL Offers] en [!UICONTROL Activities] bezoek de [ documentatie van Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer.html).

### [!UICONTROL Administration]

De gebruikersinterface van het Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. U kunt dit dashboard openen door **[!UICONTROL License usage]** te selecteren in de navigatie. Meer over het dashboard van het vergunningsgebruik leren, bezoek de [ gids van het vergunningsgebruik dashboard ](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>De dashboardfunctionaliteit voor licentiegebruik bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Volgende stappen

Door deze gids te lezen, bent u nu geïntroduceerd aan de homepage en belangrijkste navigatie elementen van Platform UI. Voor meer gedetailleerde informatie over het werken in het gebruikersinterface, gelieve te verwijzen naar de documentatie voor elke individuele dienst van het Platform. De verbindingen aan deze documentatie worden verstrekt in de [ verlaten navigatie ](#left-nav) sectie die vroeger in dit document wordt gevonden.
