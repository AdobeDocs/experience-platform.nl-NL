---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Sensei Machine Learning API
topic: Developer guide
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# [!DNL Sensei Machine Learning] Handleiding voor API-ontwikkelaars

De [!DNL Sensei Machine Learning] API biedt gegevenswetenschappers een mechanisme voor het organiseren en beheren van services voor het leren van machines, van algoritme aan boord via experimenten en implementatie van services.

Deze ontwikkelaarsgids verstrekt stappen om u te helpen beginnen de het Leren API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei Machine te gebruiken, en toont API vraag voor het uitvoeren van verrichtingen CRUD op diverse middelen van de Werkruimte van de Wetenschap van Gegevens aan.

## Aan de slag

U moet de [autorisatiezelfstudie](../../tutorials/authentication.md) hebben voltooid om toegang te hebben tot de volgende aanvraagheaders om aanroepen van API&#39; [!DNL Adobe Experience Platform] s uit te voeren:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

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