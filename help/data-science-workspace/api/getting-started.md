---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Sensei Machine Learning API
topic: Developer guide
translation-type: tm+mt
source-git-commit: 9e12c8087524f692a123b3389df4fdc324c4238d

---


# Handleiding voor ontwikkelaars van Sensei Machine Learning API

De Sensei Machine Learning-API biedt een mechanisme voor gegevenswetenschappers om services voor machinaal leren te organiseren en te beheren, van algoritme voor instappen tot experimenteren en implementatie van services.

Deze ontwikkelaarsgids verstrekt stappen om u te helpen beginnen de het Leren API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei Machine te gebruiken, en toont API vraag voor het uitvoeren van verrichtingen CRUD op diverse middelen van de Werkruimte van de Wetenschap van Gegevens aan.

## Aan de slag

U moet de [verificatiezelfstudie](../../tutorials/authentication.md) hebben voltooid om toegang te hebben tot de volgende aanvraagheaders om aanroepen te kunnen uitvoeren naar API&#39;s van het Adobe Experience Platform:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Zodra u de vereiste authentificatiegeloofsbrieven hebt verzameld, kunt u aan de verdere secties van deze ontwikkelaarsgids voor steekproefAPI vraag aan de volgende eindpuntgroepen te werk gaan:

* [Motoren](engines.md)
* [Experimenten](experiments.md)
* [Inzichten](insights.md)
* [MLInstances (Recipes)](mlinstances.md)
* [MLServices](mlservices.md)
* [Modellen](models.md)
* [Aanhangsel](appendix.md)