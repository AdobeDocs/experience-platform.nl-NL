---
keywords: Experience Platform;ontwikkelaarsgids;eindpunt;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;de werkruimte van de wetenschap van gegevens;gegevenswetenschap
solution: Experience Platform
title: API-handleiding Sensei Machine Learning
topic: Developer guide
description: Met de API voor leren van Sensei-machines kunnen ontwikkelaars CRUD-bewerkingen uitvoeren op verschillende bronnen van de Data Science Workspace. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] API-handleiding

De [!DNL Sensei Machine Learning] API biedt een mechanisme voor gegevenswetenschappers om services voor machinaal leren te organiseren en te beheren, van algoritme aan boord tot experimenteren en implementatie van services.

Deze ontwikkelaarsgids verstrekt stappen om u te helpen beginnen [Sensei Machine het Leren API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) te gebruiken, en toont API vraag voor het uitvoeren van verrichtingen CRUD op diverse middelen van de Werkruimte van de Wetenschap van Gegevens aan.

## Aan de slag

U moet de [verificatie](https://www.adobe.com/go/platform-api-authentication-en) zelfstudie hebben voltooid om toegang tot de volgende verzoekkopballen te hebben om vraag aan [!DNL Adobe Experience Platform] APIs te maken:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

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