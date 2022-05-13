---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;vraag
solution: Experience Platform
title: Overzicht van Query Service
topic-legacy: overview
description: Dit document verstrekt een overzicht van de rol van de Dienst van de Vraag binnen Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: c09a7a6198bf1ef3f94e53bdbdf3b0b93f6b2bd1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Query Service] - overzicht

Adobe Experience Platform neemt gegevens op uit een groot aantal verschillende bronnen. Een belangrijke uitdaging voor marketeers is het logisch van deze gegevens inzicht te krijgen in hun klanten. Adobe Experience Platform [!DNL Query Service] vergemakkelijkt dat door u toe te staan om standaardSQL aan vraaggegevens binnen te gebruiken [!DNL Platform]. Gebruiken [!DNL Query Service], kunt u zich bij om het even welke dataset in [!DNL Data Lake] en vang de vraagresultaten als nieuwe dataset voor gebruik in het melden, machine het leren, of voor opname in [!DNL Real-time Customer Profile]. Dit document biedt een overzicht van de rol van [!DNL Query Service] binnen [!DNL Experience Platform].

[!DNL Query Service] maakt het voor merken mogelijk om de online-aan-off-line klantenreis aan te sluiten en omni-channel attributie te begrijpen. In de volgende video ziet u hoe een zakelijke ervaring kan worden benut [!DNL Query Service] om belangrijke gebruiksgevallen te behandelen en hoe [!DNL Query Service] werkt.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Gebruiken [!DNL Query Service]

[!DNL Query Service] biedt een gebruikersinterface en een RESTful-API waarmee u SQL-query&#39;s kunt maken voor een betere analyse van uw gegevens. Met de gebruikersinterface kunt u query&#39;s schrijven en uitvoeren, eerder uitgevoerde query&#39;s weergeven en toegang krijgen tot query&#39;s die zijn opgeslagen door gebruikers binnen uw IMS-organisatie. De gebruikersinterface is bedoeld om als zandbak te worden gebruikt om uw vragen uit te testen alvorens hen op uw bredere dataset uit te voeren. Meer informatie over het gebruik van de interactieve service in [!DNL Platform] kunt u vinden in het dialoogvenster [Handleiding voor gebruikersinterface van Query Service](ui/overview.md). De RESTful API verstrekt een gelijkaardige ervaring, die u toestaat om vragen programmatically te schrijven en uit te voeren, vragen voor toekomstig gebruik en herhaling te plannen, evenals malplaatjes voor vragen te creëren u wenst te schrijven. Meer informatie over het gebruik van de [!DNL Query Service] API kan worden gevonden in de [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md).

## [!DNL Query Service] en [!DNL Experience Platform] diensten

[!DNL Query Service] interactie en kan samen met veelvoudige [!DNL Experience Platform] diensten. Om het beste te bereiken van [!DNL Query Service's] mogelijkheden, adviseert men dat u vertrouwd met deze diensten wordt en hoe zij met [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te verkrijgen uit gegevens die binnen [!DNL Experience Platform]. [!DNL Data Science Workspace] gegevenswetenschappers in staat stellen recepten op te bouwen op basis van gegevens uit de registratie- en tijdreeksen over klanten en hun activiteiten, waardoor voorspellingen zoals het kopen van neiging en aanbevolen aanbiedingen die het individu waarschijnlijk zal waarderen en gebruiken, worden vergemakkelijkt. U kunt SQL gebruiken binnen [!DNL Data Science Workspace] door [!DNL Query Service] in [!DNL JupyterLab], waarmee u Adobe Analytics-gegevens kunt verkennen, transformeren en analyseren. Lees de [!DNL Data Science Workspace] overzicht voor meer informatie over [!DNL Data Science Workspace]en de [!DNL Query Service] integratiegids voor meer informatie over hoe [!DNL Data Science Workspace] communiceert met [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] kunnen gebruikers hun klanten verdelen in kleinere groepen die gelijkaardige eigenschappen delen. Deze segmenten kunnen vervolgens worden geëvalueerd voor een betere analyse van uw [!DNL Real-time Customer Profile] gegevens. [!DNL Query Service] kan worden gebruikt om deze analyse te verstrekken door vragen over dit segmentgegevens binnen te lopen [!DNL Data Lake]. Lees de [!DNL Segmentation Service] overzicht voor meer informatie over segmentatie, en [!DNL Profile Query Language] (PQL) voor meer informatie over het analyseren van segmenten.

## Gebruiksscenario’s

[!DNL Query Service] biedt een flexibele benadering van uw gegevensverwerking die vele doeleinden dient. Het kan onder andere de lasten van segmentatie van marketeers verlichten, en helpen actionable publiek en zinvolle bedrijfsinzichten produceren. De volgende gebruiksgevallen bieden meer gedetailleerde voorbeelden van de kracht van [!DNL Query Service].

### Adobe Analytics browse-dissident

Dit [browservoorbeeld centreert bij gebruik van Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) gegevens om een bepaald actief publiek te creëren. [!DNL Query Service] past complexe logica voor segmentatie aan om diverse gepersonaliseerde attributen voor gebruik stroomafwaarts te berekenen, of zeer te vereenvoudigen hoe u uw segmenten bouwt.

### Laagere BI-dashboards

Met Adobe Experience Platform kunt u alle opgeslagen datasets, waaronder gedragsgegevens, CRM en verkooppuntgegevens, opnemen, opslaan, structureren en ophalen. Gebruiken [!DNL Experience Platform's Query Service], kunt u op deze datasets vragen en specifieke vragen over de zaken beantwoorden en dan beginnen het produceren van impactful inzichten. De volgende video toont de waarde aan van het bouwen van dashboards in bedrijfsintelligentie (BI) hulpmiddelen gebruikend [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Volgende stappen en extra bronnen

Door dit document te lezen, hebt u [!DNL Query Service] en hoe het functioneert binnen de grotere reikwijdte van [!DNL Experience Platform]. Voor meer informatie over interactie met verschillende eindpunten binnen [!DNL Query Service] API, lees de [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md). Voor meer informatie over het gebruik van de interactieve service in [!DNL Platform], lees de [Handleiding voor gebruikersinterface van Query Service](ui/overview.md). Voor een uitgebreide lijst over het verbinden van externe cliënten met [!DNL Query Service], lees de [Overzicht van Query Service-clients](clients/overview.md).

Bekijk de volgende video om uzelf beter voor te bereiden op het uitvoeren van query&#39;s. Deze video deelt uiteinden en beste praktijken voor het runnen van vragen in de interface van de vraagredacteur, cliënten PSQL, bedrijfsintelligentie (BI) oplossingen, en HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
