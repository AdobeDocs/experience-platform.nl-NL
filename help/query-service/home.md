---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;vraag
solution: Experience Platform
title: Overzicht van Query Service
description: Leer over de rol van de Dienst van de Vraag binnen Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Overzicht van Query Service

Adobe Experience Platform neemt gegevens op uit een groot aantal verschillende bronnen. Een belangrijke uitdaging voor marketeers is om deze gegevens te begrijpen om inzicht te krijgen in hun klanten. Als u gegevens wilt opvragen in Platform, kunt u standaard SQL en Adobe Experience Platform Query Service gebruiken. U kunt de Dienst van de Vraag gebruiken om zich bij om het even welke dataset in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname te vangen in [!DNL Real-Time Customer Profile]. Dit document verstrekt een overzicht van de rol van de Dienst van de Vraag binnen Experience Platform.

U kunt de Dienst van de Vraag gebruiken om de online-aan-off-line klantenreis aan te sluiten en omni-channel attributie voor uw merk te begrijpen. De volgende video toont hoe een ervaringszaken de Dienst van de Vraag kunnen gebruiken om zeer belangrijke gebruiksgevallen te richten en hoe de Dienst van de Vraag werkt.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Query-service gebruiken {#usage}

Om uw gegevens te analyseren, creeer en voer SQL vragen met of de gebruikersinterface van de Dienst van de Vraag of RESTful API uit.
Met de Dienst UI van de Vraag kunt u schrijven, uitvoeren, en vragen plannen, eerder uitgevoerde vragen bekijken, en toegangsvragen die door gebruikers binnen uw organisatie worden bewaard. U kunt uw vragen ook uittesten alvorens hen op uw bredere dataset met de Redacteur van de Vraag uit te voeren. Zie de [Handleiding voor Query Service](ui/overview.md) voor een overzicht van de UI-functionaliteit.

De RESTful-API biedt een vergelijkbare ervaring. U kunt de API van de Dienst van de Vraag gebruiken om vragen programmatically te schrijven en uit te voeren, malplaatjes voor vragen tot stand te brengen en te bewaren die u wenst om aan te passen, of vragen voor geautomatiseerde uitvoering te plannen. Zie de [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md) voor meer informatie over het gebruik van de API van de Query Service.

Als u snel aan de slag wilt met de functies van Query Service, kunt u het beste de volgende documenten lezen:

- [Algemene richtlijnen voor het uitvoeren van query&#39;s](./best-practices/writing-queries.md)
- [SQL-syntaxis in Query Service](./sql/syntax.md)
- [Afgeleide datasets maken met SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Query-service en Experience Platform {#experience-platform-services}

De Dienst van de vraag wisselt en kan met de veelvoudige diensten van het Experience Platform worden gebruikt. Om de meesten uit de mogelijkheden van de Dienst van de Vraag te maken, zou u vertrouwd met deze diensten moeten worden en hoe zij met de Dienst van de Vraag communiceren. De [Experience Platform documentatie landingspagina](https://experienceleague.adobe.com/docs/experience-platform.html) bevat samenvattingen en koppelingen naar de mogelijkheden van het platform.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzicht te krijgen in gegevens die in het Experience Platform zijn opgeslagen. Gegevenswetenschappers kunnen de [!DNL Data Science Workspace] recepten op te bouwen op basis van gegevens uit de registratie- en tijdreeksen over klanten en hun activiteiten. Deze recepten maken voorspellingen mogelijk, zoals het kopen van neiging en aanbevolen aanbiedingen die de betrokkene waarschijnlijk zal waarderen en gebruiken. U kunt SQL gebruiken binnen [!DNL Data Science Workspace] door de Dienst van de Vraag in te integreren [!DNL JupyterLab] Adobe Analytics-gegevens verkennen, transformeren en analyseren. Lees de [[!DNL Data Science Workspace] overzicht](../data-science-workspace/home.md) en de [Verbindingshandleiding voor Jupyter-laptop](./clients/jupyter-notebook.md) voor meer informatie over hoe [!DNL Data Science Workspace] communiceert met de Dienst van de Vraag.

### [!DNL Segmentation Service] {#segmentation}

Gebruik de Adobe Experience Platform Segmentation Service om uw klanten in kleinere groepen te verdelen die gelijkaardige eigenschappen delen. Deze doelgroepen kunnen vervolgens worden geëvalueerd om een betere analyse te maken van de gegevens van uw realtime klantprofiel. U kunt de Dienst van de Vraag gebruiken om vragen op deze publieksgegevens binnen het gegevenshoek in werking te stellen en de analyse te verstrekken. Lees de [Overzicht van segmentatieservice](../segmentation/home.md) en de [[!DNL Profile Query Language] (PQL)-hulplijn](../segmentation/pql/overview.md) voor meer informatie over de manier waarop het publiek kan worden geanalyseerd.

## Gebruiksscenario’s {#use-cases}

De Dienst van de vraag verstrekt een flexibele benadering van uw gegevensverwerking die vele doeleinden dient. Het kan onder andere de last van segmentatie van marketeers verlichten, en helpen actionable publiek en zinvolle bedrijfsinzichten produceren. De volgende gebruiksgevallen bieden meer diepgaande voorbeelden van de macht van de Dienst van de Vraag.

### Adobe Analytics browse-dissident {#abandon-browse}

Dit [browservoorbeeld centreert bij gebruik van Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) gegevens om een bepaald actief publiek te creëren. De Dienst van de vraag past complexe logica voor segmentatie aan om diverse gepersonaliseerde attributen voor gebruik stroomafwaarts te berekenen, of zeer te vereenvoudigen hoe u uw publiek bouwt.

## Inzichten genereren met aangepaste dashboards {#custom-dashboards}

Met Adobe Experience Platform kunt u alle opgeslagen datasets, waaronder gedragsgegevens, CRM en verkooppuntgegevens, opnemen, opslaan, structureren en ophalen. Gebruiken [!DNL Experience Platform's Query Service], kunt u op deze datasets vragen en specifieke vragen over de zaken beantwoorden en dan beginnen het produceren van impactful inzichten. Leer hoe u aangepaste dashboards kunt maken en beheren waar u op maat gemaakte widgets kunt maken, toevoegen en bewerken om belangrijke metriek te visualiseren met [door de gebruiker gedefinieerde dashbaords](../dashboards/user-defined-dashboards.md). U kunt zelfs [je eigen Real-Time CDP-rapporten aanpassen](../dashboards/data-models/cdp-insights-data-model-b2c.md) voor uw marketing en KPI gebruiksgevallen door SQL vragen met de Modellen van Gegevens van de Gegevens van Real-time Customer Data Platform te gebruiken.

## Volgende stappen en extra bronnen

Door dit document te lezen, bent u geïntroduceerd aan de Dienst van de Vraag en hoe het binnen het grotere werkingsgebied van Experience Platform functioneert. Om over de eigenschappen van de Dienst van de Vraag verder te leren, wordt u geadviseerd om de volgende documenten te lezen:

- De [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md): Voor meer informatie bij het in wisselwerking staan met diverse eindpunten binnen de Dienst API van de Vraag.
- De [Handleiding voor gebruikersinterface van Query Service](ui/overview.md): Voor meer informatie bij het gebruiken van de Redacteur van de Vraag en UI.
- De [Overzicht van Query Service-clients](clients/overview.md): Voor een uitvoerige lijst van externe cliënten om met de Dienst van de Vraag te verbinden.

Bekijk de volgende video om uzelf beter voor te bereiden op het uitvoeren van query&#39;s. Deze video deelt uiteinden en beste praktijken voor het runnen van vragen in de interface van de vraagredacteur, cliënten PSQL, bedrijfsintelligentie (BI) oplossingen, en HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
