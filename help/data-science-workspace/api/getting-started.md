---
keywords: Experience Platform;ontwikkelaarsgids;eindpunt;Gegevens Wetenschap Workspace;populaire onderwerpen;de werkruimte van de wetenschap van gegevens;gegevenswetenschap
solution: Experience Platform
title: API-handleiding voor Sensei Machine Learning
description: Met de API voor leren van Sensei Machine Learning kunnen ontwikkelaars CRUD-bewerkingen uitvoeren op verschillende Data Science Workspace-bronnen. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 5%

---

# [!DNL Sensei Machine Learning] API-handleiding

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

De API van [!DNL Sensei Machine Learning] verstrekt een mechanisme voor gegevenswetenschappers om machine het leren diensten te organiseren en te beheren, van algoritme op het instappen door experimenteren en aan de dienstplaatsing.

Deze ontwikkelaarsgids verstrekt stappen om u te helpen beginnen te gebruiken [ het Leren API van de Machine van Sensei ](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/), en toont API vraag voor het uitvoeren van verrichtingen CRUD op diverse middelen van Workspace van de Wetenschap van Gegevens aan.

## Aan de slag

U moet het [ authentificatie ](https://www.adobe.com/go/platform-api-authentication-en) leerprogramma hebben voltooid om toegang tot de volgende verzoekkopballen te hebben om vraag aan [!DNL Adobe Experience Platform] APIs te maken:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Zodra u de vereiste authentificatiegeloofsbrieven hebt verzameld, kunt u aan de verdere secties van deze ontwikkelaarsgids voor steekproefAPI vraag aan de volgende eindpuntgroepen te werk gaan:

* [Motoren](./engines.md)
* [Experimenten](./experiments.md)
* [Inzichten](./insights.md)
* [MLInstances (Recipes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modellen](./models.md)
* [Bijlage](./appendix.md)
