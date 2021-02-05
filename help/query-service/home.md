---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;vraag
solution: Experience Platform
title: Overzicht van Query Service
topic: overview
description: Dit document verstrekt een overzicht van de rol van de Dienst van de Vraag binnen Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# [!DNL Query Service] - overzicht

Adobe Experience Platform neemt gegevens op uit een groot aantal verschillende bronnen. Een belangrijke uitdaging voor marketeers is het logisch van deze gegevens inzicht te krijgen in hun klanten. Adobe Experience Platform [!DNL Query Service] vergemakkelijkt dat door u toe te staan om standaardSQL aan vraaggegevens in [!DNL Platform] te gebruiken. Gebruikend [!DNL Query Service], kunt u zich bij om het even welke dataset in [!DNL Data Lake] aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname in [!DNL Real-time Customer Profile]. Dit document biedt een overzicht van de rol van [!DNL Query Service] binnen [!DNL Experience Platform].

[!DNL Query Service] maakt het voor merken mogelijk om de online-aan-off-line klantenreis aan te sluiten en omni-channel attributie te begrijpen. In de volgende video ziet u hoe een bedrijf met ervaring omgaat met het gebruik van belangrijke zaken en hoe [!DNL Query Service] werkt.[!DNL Query Service]

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## [!DNL Query Service] gebruiken

[!DNL Query Service] biedt een gebruikersinterface en een RESTful-API waarmee u SQL-query&#39;s kunt maken voor een betere analyse van uw gegevens. Met de gebruikersinterface kunt u query&#39;s schrijven en uitvoeren, eerder uitgevoerde query&#39;s weergeven en toegang krijgen tot query&#39;s die zijn opgeslagen door gebruikers binnen uw IMS-organisatie. De gebruikersinterface is bedoeld om als zandbak te worden gebruikt om uw vragen uit te testen alvorens hen op uw bredere dataset uit te voeren. Meer informatie over het gebruik van de interactieve service binnen [!DNL Platform] vindt u in de [Handleiding voor de gebruikersinterface van Query Service](ui/overview.md). De RESTful API verstrekt een gelijkaardige ervaring, die u toestaat om vragen programmatically te schrijven en uit te voeren, vragen voor toekomstig gebruik en herhaling te plannen, evenals malplaatjes voor vragen te creëren u wenst te schrijven. Meer informatie over het gebruik van de [!DNL Query Service] API vindt u in de [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md).

## [!DNL Query Service] en  [!DNL Experience Platform] diensten

[!DNL Query Service] wisselt en kan samen met de veelvoudige  [!DNL Experience Platform] diensten worden gebruikt. Als u optimaal wilt profiteren van [!DNL Query Service's] mogelijkheden, is het raadzaam bekend te raken met deze services en te weten hoe deze met [!DNL Query Service] werken.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te verkrijgen van gegevens die zijn opgeslagen in [!DNL Experience Platform]. [!DNL Data Science Workspace] gegevenswetenschappers in staat stellen recepten op te bouwen op basis van gegevens uit de registratie- en tijdreeksen over klanten en hun activiteiten, waardoor voorspellingen zoals het kopen van neiging en aanbevolen aanbiedingen die het individu waarschijnlijk zal waarderen en gebruiken, worden vergemakkelijkt. U kunt SQL binnen [!DNL Data Science Workspace] gebruiken door [!DNL Query Service] in [!DNL JupyterLab] te integreren, toestaand u om, Adobe Analytics gegevens te onderzoeken te transformeren en te analyseren. Lees het [!DNL Data Science Workspace]-overzicht voor meer informatie over [!DNL Data Science Workspace] en de [!DNL Query Service]-integratiegids voor meer informatie over hoe [!DNL Data Science Workspace] communiceert met [!DNL Query Service].

### [!DNL Segmentation Service]

Met Adobe Experience Platform [!DNL Segmentation Service] kunnen gebruikers hun klanten opdelen in kleinere groepen die vergelijkbare kenmerken hebben. Deze segmenten kunnen vervolgens worden geëvalueerd voor een betere analyse van uw [!DNL Real-time Customer Profile]-gegevens. [!DNL Query Service] kan worden gebruikt om deze analyse te verstrekken door vragen over dit segmentgegevens binnen te lopen  [!DNL Data Lake]. Lees het [!DNL Segmentation Service]-overzicht voor meer informatie over segmentatie en de [!DNL Profile Query Language]-hulplijn (PQL) voor meer informatie over het analyseren van segmenten.

### Gebruikszaak van Looker BI

Met Adobe Experience Platform kunt u alle opgeslagen datasets, waaronder gedragsgegevens, CRM en verkooppuntgegevens, opnemen, opslaan, structureren en ophalen. Gebruikend [!DNL Experience Platform's Query Service], kunt u op deze datasets vragen en specifieke vragen over de zaken beantwoorden en dan beginnen producerend impactful inzichten. In de volgende video ziet u hoe belangrijk het is om dashboards te bouwen in Business Intelligence (BI)-gereedschappen met [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Volgende stappen en extra bronnen

Door dit document te lezen, bent u geïntroduceerd aan [!DNL Query Service] en hoe het binnen het grotere werkingsgebied van [!DNL Experience Platform] functioneert. Lees voor meer informatie over interactie met verschillende eindpunten binnen de [!DNL Query Service] API de [Handleiding voor ontwikkelaars van Query Service](api/getting-started.md). Lees voor meer informatie over het gebruik van de interactieve service binnen [!DNL Platform] de [Handleiding voor de gebruikersinterface van Query Service](ui/overview.md). Lees voor een uitgebreide lijst over het verbinden van externe clients met [!DNL Query Service] het [Overzicht van Query Service-clients](clients/overview.md).

Bekijk de volgende video om uzelf beter voor te bereiden op het uitvoeren van query&#39;s. Deze video deelt uiteinden en beste praktijken voor het runnen van vragen in de interface van de vraagredacteur, cliënten PSQL, bedrijfsintelligentie (BI) oplossingen, en HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
