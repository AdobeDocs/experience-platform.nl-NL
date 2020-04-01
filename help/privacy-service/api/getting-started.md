---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van de privacyservice
description: Gebruik de RESTful-API om de persoonlijke gegevens van de betrokkenen in Adobe Experience Cloud-toepassingen te beheren
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a28ad2725094e0748e2860276ab2e7581d790ac

---


# Handleiding voor ontwikkelaars van de privacyservice

De Adobe Experience Platform Privacy Service biedt een RESTful API en een gebruikersinterface waarmee u de persoonlijke gegevens van uw betrokkenen (klanten) in alle Adobe Experience Cloud-toepassingen kunt beheren (openen en verwijderen). De Dienst van de privacy verstrekt ook een centraal controle en registratiemechanisme dat u toestaat om tot de status en de resultaten van banen toegang te hebben die de toepassingen van de Wolk van de Ervaring impliceren.

In deze handleiding wordt uitgelegd hoe u de API voor de privacyservice kunt gebruiken. Zie het overzicht [van de](../ui/overview.md)privacyservice voor meer informatie over het gebruik van de gebruikersinterface. Raadpleeg de [API-referentie](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)voor een uitgebreide lijst met alle beschikbare eindpunten in de API voor de privacyservice.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende functies van het Experience Platform:

* [Privacy-service](../home.md): Biedt een RESTful-API en -gebruikersinterface waarmee u toegang kunt beheren en aanvragen van uw betrokkenen (klanten) kunt verwijderen voor alle Adobe Experience Cloud-toepassingen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Dienst API van de Privacy te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](https://www.adobe.io/apis/experienceplatform/home/services/troubleshooting.html#!api-specification/markdown/narrative/technical_overview/platform_faq_and_troubleshooting/platform_faq_and_troubleshooting.md) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het maken vraag aan de Dienst API van de Privacy. Het document over [privacybanen](privacy-jobs.md) doorloopt de verschillende API-aanroepen die u kunt maken met de API van de privacydienst. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.
