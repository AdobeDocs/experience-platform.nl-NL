---
title: Aan de slag met de API voor sandboxgereedschappen
description: Met de API voor het gereedschap Sandbox kunt u artefacten onderzoeken en een momentopname van sandboxconfiguraties tussen sandboxen exporteren en importeren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 4%

---

# Aan de slag met de API voor gereedschappen voor de sandbox {#getting-started}

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de API voor het bewerken van sandboxen kunt gebruiken voor het beheer van pakketten en gereedschappen in Adobe Experience Platform. Deze handleiding bevat voorbeelden van API-aanroepen voor het uitvoeren van verschillende bewerkingen.

## API-voorbeeldaanroepen lezen {#api-calls}

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON-gegevens die naar de API-reactie worden geretourneerd, worden ook verschaft. Voor informatie over de overeenkomsten die in de documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen {#headers}

Deze gids vereist u om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan Experience Platform APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen {#next-steps}

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.

Zie de volgende API-zelfstudies om aanroepen uit te voeren naar de API voor gereedschappen in de sandbox:

* [Pakketeindpunt](./packages.md)
* [Het eindpunt van Tools](./tools.md)
