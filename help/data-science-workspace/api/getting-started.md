---
keywords: Experience Platform;ontwikkelaarsgids;eindpunt;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;de werkruimte van de wetenschap van gegevens;gegevenswetenschap
solution: Experience Platform
title: API-handleiding voor Sensei Machine Learning
topic-legacy: Developer guide
description: Met de API voor leren van Sensei-machines kunnen ontwikkelaars CRUD-bewerkingen uitvoeren op verschillende bronnen van Data Science Workspace. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] API-handleiding

De [!DNL Sensei Machine Learning] API biedt gegevenswetenschappers een mechanisme voor het organiseren en beheren van services voor het leren van machines, van algoritmen aan boord tot experimenten en het implementeren van services.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de functie [API voor leren werken met Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)en toont API-aanroepen aan voor het uitvoeren van CRUD-bewerkingen op verschillende bronnen van de Data Science Workspace.

## Aan de slag

U moet de [verificatie](https://www.adobe.com/go/platform-api-authentication-en) zelfstudie om toegang tot de volgende verzoekkopballen te hebben om vraag te maken aan [!DNL Adobe Experience Platform] API&#39;s:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

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
* [Aanhangsel](./appendix.md)
