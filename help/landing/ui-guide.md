---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;gebruikershandleiding;ui-handleiding;platform ui-handleiding;introductie op platform;dashboard;
solution: Experience Platform
title: Overzicht gebruikersinterface Experience Platform
topic: ui guide
description: 'Adobe Experience Platform '
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 0%

---


# Handleiding Adobe Experience Platform UI

Deze gids dient als inleiding aan het gebruiken van het gebruikersinterface van Adobe Experience Platform (UI), die verklaart wat de diverse componenten worden gebruikt voor en verbindingen verstrekt aan verdere documentatie voor meer informatie.

Lees voor meer informatie over Adobe Experience Platform het [overzicht van het Experience Platform](home.md).

## Startscherm

Nadat u zich hebt aangemeld bij Adobe Experience Platform, bevindt u zich op de pagina [!UICONTROL Home], die bestaat uit het [dashboard voor meetgegevens](#metrics), [recente gegevens](#recent-data) en [aanbevolen leersecties](#recommended-learning).

![](images/user-guide/homepage.png)

### Metrics

Het dashboard van metriek verstrekt kaarten die u informatie over datasets, profielen, segmenten, en bestemmingen binnen uw organisatie geven.

![](images/user-guide/homepage-dashboard.png)

De **[!UICONTROL sectie Datasets]** toont het aantal datasets binnen uw organisatie IMS. Dit aantal wordt bijgewerkt wanneer een nieuwe dataset wordt gecreeerd. Meer informatie over datasets vindt u in het [overzicht van datasets](../catalog/datasets/overview.md).

In de sectie **[!UICONTROL Profielen]** wordt het totale aantal personen met profielen binnen uw IMS-organisatie weergegeven, exclusief profielfragmenten. Dit totale aantal personen vertegenwoordigt het totale adresseerbare publiek en wordt elke 24 uur bijgewerkt. Meer informatie over profielen vindt u in het [Real-time overzicht van het Klantprofiel](../profile/home.md).

In de sectie **[!UICONTROL Segmenten]** wordt het totale aantal segmenten weergegeven dat binnen uw IMS-organisatie is gemaakt. Dit aantal wordt bijgewerkt wanneer een nieuw segment wordt gecreeerd. Meer informatie over segmenten vindt u in het [Overzicht van de segmentatieservice](../segmentation/home.md).

De **[!UICONTROL sectie Doelen]** toont het totale aantal bestemmingen die voor de Organisatie IMS worden gecreeerd. Dit aantal wordt bijgewerkt wanneer een nieuwe bestemming wordt gecreeerd. Meer informatie over bestemmingen kan in [bestemmingen overzicht](../destinations/home.md) worden gevonden.

### Recente gegevens

Het recente gegevensdashboard verstrekt informatie over onlangs gecreeerde datasets, bronnen, segmenten, en bestemmingen.

![](images/user-guide/homepage-recent.png)

De **[!UICONTROL Recente datasets]** sectie maakt een lijst van de vijf onlangs gecreeerde datasets binnen uw IMS Organisatie. Deze lijst wordt bijgewerkt telkens als een nieuwe dataset wordt gecreeerd. U kunt een dataset van de lijst selecteren om meer informatie over de gespecificeerde dataset te bekijken of **[!UICONTROL allen te selecteren]** om een lijst van alle gecreeerde datasets te zien. Meer informatie over datasets vindt u in het [overzicht van datasets](../catalog/datasets/overview.md).

De **[!UICONTROL Recente bronnen]** sectie maakt een lijst van de vijf onlangs gecreeerde bronschakelaars binnen uw IMS Organisatie. Deze lijst wordt bijgewerkt telkens als een nieuwe bronschakelaar wordt gecreeerd. U kunt een bronverbinding van de lijst selecteren om meer informatie over de gespecificeerde schakelaar te bekijken of **[!UICONTROL allen bekijken]** om een lijst van alle gecreeerde bronverbindingen te zien. Meer informatie over bronnen vindt u in het [overzicht van bronnen](../sources/home.md).

De **[!UICONTROL Recente segmenten]** sectie maakt een lijst van de vijf onlangs gecreeerd segmentdefinities binnen uw IMS Organisatie. Deze lijst wordt bijgewerkt telkens als een nieuwe segmentdefinitie wordt gecreeerd. U kunt een segmentdefinitie van de lijst selecteren om meer informatie over de gespecificeerde segmentdefinitie te bekijken of **[!UICONTROL allen]** te selecteren om een lijst van alle gecreeerde segmentdefinities te zien. Meer informatie over segmenten vindt u in het [Overzicht van de segmentatieservice](../segmentation/home.md).

De **[!UICONTROL Recente bestemmingen]** sectie maakt een lijst van de vijf onlangs gecreeerde bestemmingen binnen uw organisatie IMS. Deze lijst wordt bijgewerkt telkens wanneer een nieuwe bestemming wordt gecreeerd. U kunt een bestemming van de lijst selecteren om meer informatie over de gespecificeerde bestemming te bekijken of **[!UICONTROL allen]** te selecteren om een lijst van alle gecreeerde bestemmingen te zien. Meer informatie over bestemmingen kan in [bestemmingen overzicht](../destinations/home.md) worden gevonden.

### Aanbevolen training

In de sectie **[!UICONTROL Aanbevolen training]** vindt u koppelingen naar handige documentatie die u kunt gebruiken om aan de slag te gaan met Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Bovenste navigatiebalk

Op de bovenste navigatiebalk in de gebruikersinterface van het Platform wordt de IMS-organisatie weergegeven waarvoor u zich momenteel hebt aangemeld en zijn diverse belangrijke besturingselementen beschikbaar.

Links op de navigatiebalk bevindt zich het Adobe Experience Platform-logo. Als u dit op elk gewenst moment selecteert, wordt de gebruikersinterface van het Platform weer weergegeven.

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS-organisatieschakelaar

Het eerste item aan de rechterkant van de bovenste navigatiebalk is de **IMS Organization switch**.

![](./images/user-guide/homepage-ims-org.png)

Als u de schakeloptie selecteert, wordt een vervolgkeuzemenu geopend met IMS-organisaties waartoe u toegang hebt, indien aanwezig. Selecteer een weergegeven optie om over te schakelen naar die IMS-organisatie.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Overschakelen op toepassingen

Het volgende punt op de rechterkant van de hoogste navigatie is **toepassingsschakelaar**, die door ![toepassingsschakelaar](./images/user-guide/app-switcher-icon.png) pictogram wordt vertegenwoordigd. Wanneer u dit pictogram selecteert, kunt u schakelen tussen Adobe-toepassingen waartoe uw IMS-organisatie toegang heeft, zoals Experience Platform, Analytics, Assets en Launch.

### Help

Rechts van de toepassingsschakeloptie bevindt zich het **help- en ondersteuningsmenu**, dat wordt weergegeven door het ![vraagteken/help](./images/user-guide/help-icon.png)-pictogram. Wanneer u dit pictogram selecteert, wordt een pop-upmenu weergegeven dat verschillende Help- en ondersteuningsbronnen bevat. Het **[!UICONTROL Help]** lusje toont een lijst van relevante documentatie voor de pagina u momenteel op bent. Met het tabblad **[!UICONTROL Ondersteuning]** kunt u een ondersteuningsticket maken met het ondersteuningsteam Adobe. Met het tabblad **[!UICONTROL Feedback]** kunt u feedback over Platform verzenden naar Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Meldingen en aankondigingen

In **berichtensectie**, die door ![bel/Meldingen en Aankondigingen](images/user-guide/notification-icon.png) pictogram wordt vertegenwoordigd. Het tabblad **[!UICONTROL Meldingen]** bevat belangrijke informatie over het product en andere relevante updates, terwijl op het tabblad **[!UICONTROL Aankondigingen]** informatie over onderhoud van de service wordt weergegeven.

### Gebruikersprofiel

Het laatste item op de bovenste navigatiebalk is de **gebruikersinstellingen**, die wordt weergegeven door het pictogram ![gebruikersinstellingen/Gebruikersprofiel](images/user-guide/profile-icon.png). Selecteer dit pictogram om uw voorkeuren te bewerken of u af te melden.

### Sandboxen

Direct onder de bovenste navigatiebalk bevindt zich de sandboxbalk. Deze balk geeft aan welke sandbox u momenteel gebruikt voor Platform. Meer informatie over sandboxen vindt u in het [overzicht van sandboxen](../sandboxes/home.md).

## Linkernavigatie {#left-nav}

De navigatie op de linkerkant van het scherm maakt een lijst van alle verschillende diensten die in de UI van het Platform worden gesteund.

>[!IMPORTANT]
>
>Sommige secties op de linkernavigatiebalk worden mogelijk niet weergegeven of zijn grijs weergegeven. Dit komt omdat u geen toegang hebt tot deze functies. Neem contact op met de systeembeheerder als u van mening bent dat u toegang tot deze secties moet hebben.

![](images/user-guide/homepage-left.png)

Met de sectie **[!UICONTROL Home]** kunt u terugkeren naar de startpagina van de gebruikersinterface van het Platform.

In de sectie **[!UICONTROL Workflows]** wordt een lijst weergegeven met uit meerdere stappen bestaande workflows voor het uitvoeren van bewerkingen binnen het Platform. Meer informatie over workflows vindt u in het [overzicht van workflows](./workflows.md).

### [!UICONTROL Verbindingen]

Met de sectie **[!UICONTROL Bronnen]** kunt u bronverbindingen maken, bijwerken en verwijderen, zodat u gegevens van externe bronnen in Platform kunt invoeren. Meer informatie over bronnen vindt u in het [overzicht van bronnen](../sources/home.md).

Met de sectie **[!UICONTROL Doelen]** kunt u doelen maken, bijwerken en verwijderen, zodat u gegevens van Platform kunt exporteren naar vele externe doelen. Meer informatie over bestemmingen kan in [bestemmingen overzicht](../destinations/home.md) worden gevonden.

### [!UICONTROL Klant]

Met de sectie **[!UICONTROL Profielen]** kunt u door klantprofielen bladeren, profielmetriek bekijken, samenvoegbeleid maken en beheren en vakbondsschema&#39;s weergeven. Lees de [[!DNL Profile] gebruikershandleiding](../profile/ui/user-guide.md) voor meer informatie over het gebruik van de sectie [!UICONTROL Profielen]. Meer informatie over het profiel van de Klant in real time kan in [overzicht van het Profiel van de Klant in real time worden gevonden](../profile/home.md).

Met de sectie **[!UICONTROL Segmenten]** kunt u segmentdefinities maken en beheren. Lees de [gebruikershandleiding voor segmentatie](../segmentation/ui/overview.md) voor meer informatie over het gebruik van de sectie [!UICONTROL Segments]. Meer informatie over de Dienst van de Segmentatie vindt u in [Overzicht van de Dienst van de Segmentatie](../segmentation/home.md).

Met de sectie **[!UICONTROL Identiteiten]** kunt u naamruimten maken en beheren. Voor meer informatie over de [!UICONTROL sectie van Identiteiten], met inbegrip van informatie over identiteitsnamespaces en hoe te om identiteiten in de UI van het Platform te gebruiken, gelieve te verwijzen naar [identity namespace overzicht](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

Met de sectie **[!UICONTROL Beleid]** kunt u beleid voor gegevensgebruik maken en beheren. Lees de [Gebruikershandleiding voor gegevensgebruiksbeleid](../data-governance/policies/user-guide.md) voor meer informatie over het gebruik van de sectie Beleid. Meer informatie over het beleid voor gegevensgebruik vindt u in het [overzicht van het beleid voor gegevensgebruik](../data-governance/policies/overview.md).

Met de sectie **[!UICONTROL Verzoeken]** kunt u privacyverzoeken maken en beheren. U moet zijn toegevoegd op lijst van gewenste personen om toegang te hebben tot de gebruikersinterface van de Privacy Service. Lees voor meer informatie over het gebruik van de sectie Verzoeken de [gebruikershandleiding voor de Privacy Service](../privacy-service/ui/user-guide.md). Meer informatie over Privacy Service vindt u in het [overzicht van de Privacy Service](../privacy-service/home.md).

### [!UICONTROL Gegevenswetenschap]

De sectie **[!UICONTROL Laptops]** biedt toegang tot JupyterLab, een interactieve ontwikkelomgeving waarmee u uw gegevens kunt verkennen, analyseren en modelleren. Lees de [JupyterLab-gebruikershandleiding](../data-science-workspace/jupyterlab/overview.md) voor meer informatie over het gebruik van de sectie Laptops. Meer informatie over de Werkruimte van de Wetenschap van Gegevens vindt u in [Overzicht van de Werkruimte van de Wetenschap van Gegevens](../data-science-workspace/home.md)

Met de sectie **[!UICONTROL Modellen]** kunt u leren van machines en kunstmatige intelligentie gebruiken om modellen te maken, te ontwikkelen, te trainen en af te stemmen om voorspellingen te maken. Meer informatie over de sectie Modellen vindt u in de zelfstudie over [training en het evalueren van een model](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

Met de sectie **[!UICONTROL Services]** kunt u uw gepubliceerde modellen voor geplande Adobe beheren, of de Intelligente services van de klant benutten, een reeks AI-services die realtime, persoonlijke ervaringen bieden. Meer informatie over de sectie Services vindt u in de [Publishing a Model as a Service tutorial](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

Met de sectie **[!UICONTROL Schemas]** kunt u XDM-schema&#39;s (Experience Data Model) maken en beheren. Lees de zelfstudie over het maken van een schema](../xdm/tutorials/create-schema-ui.md) voor meer informatie over schema&#39;s. [ Meer informatie over XDM vindt u in het [XDM System overview](../xdm/home.md).

Met de sectie **[!UICONTROL Datasets]** kunt u gegevenssets maken en beheren. Meer informatie over datasets kan in [datasets worden gevonden gebruikersgids](../catalog/datasets/user-guide.md).

Met de sectie **[!UICONTROL Query&#39;s]** kunt u query&#39;s maken en beheren, SQL-query&#39;s van de Adobe Experience Platform Query Service registreren en uw PostSQL-referenties bekijken. Meer informatie over vragen kan in [de gebruikersgids van de Dienst van de Vraag](../query-service/ui/overview.md) worden gevonden.

Met de sectie **[!UICONTROL Monitoring]** kunt u batch- en streaming-opname controleren. Meer informatie over controle vindt u in de [gebruikershandleiding voor het controleren van gegevensinvoer](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Beslissing]

Offer Decisioning is een toepassingsservice die is geïntegreerd met Adobe Experience Platform. Zo kunt u Experience Platform gebruiken om uw klanten de beste aanbieding en ervaring te bieden op alle aanraakpunten op het juiste moment. Voor meer informatie over Offer Decisioning, zoals het werken met [!UICONTROL Aanbiedingen] en [!UICONTROL Activiteiten], bezoek de [documentatie van Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Beheer]

De gebruikersinterface van het Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Dit kan worden betreden door **[!UICONTROL Vergunningsgebruik]** in de navigatie te selecteren. Ga voor meer informatie over het dashboard voor licentiegebruik naar [Handleiding voor licentiegebruik](license-usage-dashboard.md).

>[!IMPORTANT]
>
>De dashboardfunctionaliteit voor licentiegebruik bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Volgende stappen

Door deze gids te lezen, bent u nu geïntroduceerd aan de homepage en belangrijkste navigatie elementen van de Platform UI. Voor meer informatie over het werken in het gebruikersinterface, gelieve te verwijzen naar de documentatie voor elke individuele dienst van het Platform. Koppelingen naar deze documentatie vindt u in de sectie [linkernavigatie](#left-nav) die eerder in dit document is gevonden.