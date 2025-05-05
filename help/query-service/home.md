---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;query
solution: Experience Platform
title: Overzicht van Query Service
description: Leer over de rol van de Dienst van de Vraag binnen Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Overzicht van Query Service

Adobe Experience Platform neemt gegevens op uit een groot aantal verschillende bronnen. Een belangrijke uitdaging voor marketeers is om deze gegevens te begrijpen om inzicht te krijgen in hun klanten. Als u gegevens wilt opvragen in Experience Platform, kunt u standaard SQL en Adobe Experience Platform Query Service gebruiken. U kunt de Dienst van de Vraag gebruiken om zich bij om het even welke dataset in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname in [!DNL Real-Time Customer Profile] te vangen. Dit document biedt een overzicht van de rol van Query Service in Experience Platform.

U kunt de Dienst van de Vraag gebruiken om de online-aan-off-line klantenreis aan te sluiten en omni-channel attributie voor uw merk te begrijpen. De volgende video toont hoe een ervaringszaken de Dienst van de Vraag kunnen gebruiken om zeer belangrijke gebruiksgevallen te richten en hoe de Dienst van de Vraag werkt.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Query-service gebruiken {#usage}

Om uw gegevens te analyseren, creeer en voer SQL vragen met of de gebruikersinterface van de Dienst van de Vraag of RESTful API uit.
Met de Dienst UI van de Vraag kunt u schrijven, uitvoeren, en vragen plannen, eerder uitgevoerde vragen bekijken, en toegangsvragen die door gebruikers binnen uw organisatie worden bewaard. U kunt uw vragen ook uittesten alvorens hen op uw bredere dataset met de Redacteur van de Vraag uit te voeren. Zie de [ gids UI van de Dienst van de Vraag ](ui/overview.md) voor een overzicht van de functionaliteit UI.

De RESTful-API biedt een vergelijkbare ervaring. U kunt de API van de Dienst van de Vraag gebruiken om vragen programmatically te schrijven en uit te voeren, malplaatjes voor vragen tot stand te brengen en te bewaren die u wenst om aan te passen, of vragen voor geautomatiseerde uitvoering te plannen. Zie de [ de ontwikkelaarsgids van de Dienst van de Vraag ](api/getting-started.md) voor meer informatie bij het gebruiken van de Dienst API van de Vraag.

Als u snel aan de slag wilt met de functies van Query Service, kunt u het beste de volgende documenten lezen:

- [Algemene richtlijnen voor het uitvoeren van query&#39;s](./best-practices/writing-queries.md)
- [SQL-syntaxis in Query Service](./sql/syntax.md)
- [Afgeleide datasets maken met SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Query-service en Experience Platform-services {#experience-platform-services}

De Dienst van de vraag wisselt en kan met de veelvoudige diensten van Experience Platform worden gebruikt. Om de meesten uit de mogelijkheden van de Dienst van de Vraag te maken, zou u vertrouwd met deze diensten moeten worden en hoe zij met de Dienst van de Vraag communiceren. De [ documentatie die van Experience Platform pagina ](https://experienceleague.adobe.com/docs/experience-platform.html?lang=nl-NL) landen verstrekt samenvattingen en verbindingen aan de mogelijkheden van het platform.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzicht te krijgen in gegevens die in Experience Platform zijn opgeslagen. Gegevenswetenschappers kunnen de [!DNL Data Science Workspace] gebruiken om recepten te bouwen die op verslag en tijdreeksgegevens over klanten en hun activiteiten worden gebaseerd. Deze recepten maken voorspellingen mogelijk, zoals het kopen van neiging en aanbevolen aanbiedingen die de betrokkene waarschijnlijk zal waarderen en gebruiken. U kunt SQL binnen [!DNL Data Science Workspace] gebruiken door de Dienst van de Vraag in [!DNL JupyterLab] te integreren om, Adobe Analytics gegevens te onderzoeken om te zetten en te analyseren. Lees het [[!DNL Data Science Workspace]  overzicht ](../data-science-workspace/home.md) en [ Jupyter de verbindingsgids van het Notitieboekje ](./clients/jupyter-notebook.md) voor meer informatie over hoe [!DNL Data Science Workspace] met de Dienst van de Vraag in wisselwerking staat.

### [!DNL Segmentation Service] {#segmentation}

Gebruik de Adobe Experience Platform Segmentation Service om uw klanten in kleinere groepen te verdelen die gelijkaardige eigenschappen delen. Deze doelgroepen kunnen vervolgens worden geëvalueerd om een betere analyse te maken van de gegevens van uw realtime klantprofiel. U kunt de Dienst van de Vraag gebruiken om vragen op deze publieksgegevens binnen het gegevenshoek in werking te stellen en de analyse te verstrekken. Lees het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) en [[!DNL Profile Query Language]  (PQL) gids ](../segmentation/pql/overview.md) voor meer informatie over hoe te om publiek te analyseren.

## Gebruiksscenario’s {#use-cases}

De Dienst van de vraag verstrekt een flexibele benadering van uw gegevensverwerking die vele doeleinden dient. Het kan onder andere de last van segmentatie van marketeers verlichten, en helpen actionable publiek en zinvolle bedrijfsinzichten produceren. De volgende gebruiksgevallen bieden meer diepgaande voorbeelden van de macht van de Dienst van de Vraag.

### Adobe Analytics browse-dissident {#abandon-browse}

Dit [ doorbladert de voorbeeldcentra van de verlaten voorbestemming bij het gebruiken van Adobe  [!DNL Analytics]](./use-cases/abandoned-browse.md) gegevens om een bepaald actionable publiek tot stand te brengen. De Dienst van de vraag past complexe logica voor segmentatie aan om diverse gepersonaliseerde attributen voor gebruik stroomafwaarts te berekenen, of zeer te vereenvoudigen hoe u uw publiek bouwt.

## Inzichten genereren met aangepaste dashboards {#custom-dashboards}

Met Adobe Experience Platform kunt u alle opgeslagen datasets, waaronder gedragsgegevens, CRM en verkooppuntgegevens, opnemen, opslaan, structureren en ophalen. Gebruikend [!DNL Experience Platform's Query Service], kunt u op deze datasets vragen en specifieke vragen over de zaken beantwoorden en dan beginnen producerend impactful inzicht. Leer hoe te om douanedashboards te bouwen en te beheren waar u, op maat gemaakte widgets kunt creëren toevoegen en uitgeven om zeer belangrijke metriek met [ te visualiseren user-defined dashbaords ](../dashboards/standard-dashboards.md). U kunt zelfs [ uw eigen rapporten van Real-Time CDP ](../dashboards/data-models/cdp-insights-data-model-b2c.md) voor uw marketing en het gebruiksgevallen van KPI aanpassen door SQL vragen met de Modellen van Gegevens van de Gegevens van Real-Time Customer Data Platform te gebruiken.

## Volgende stappen en extra bronnen

Door dit document te lezen, bent u geïntroduceerd aan de Dienst van de Vraag en hoe het binnen het grotere werkingsgebied van Experience Platform functioneert. Om over de eigenschappen van de Dienst van de Vraag verder te leren, wordt u geadviseerd om de volgende documenten te lezen:

- De [ de ontwikkelaarsgids van de Dienst van de Vraag ](api/getting-started.md): Voor meer informatie bij het in wisselwerking staan met diverse eindpunten binnen de Dienst API van de Vraag.
- De [ gebruikersinterfacegids van de Dienst van de Vraag ](ui/overview.md): Voor meer informatie bij het gebruiken van de Redacteur van de Vraag en UI.
- Het [ overzicht van de cliënten van de Dienst van de Vraag ](clients/overview.md): Voor een uitvoerige lijst van externe cliënten om met de Dienst van de Vraag te verbinden.

Bekijk de volgende video om uzelf beter voor te bereiden op het uitvoeren van query&#39;s. Deze video deelt uiteinden en beste praktijken voor het runnen van vragen in de interface van de vraagredacteur, cliënten PSQL, bedrijfsintelligentie (BI) oplossingen, en HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
