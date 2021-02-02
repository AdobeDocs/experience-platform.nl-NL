---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: Handleiding voor ontwikkelaars van sandbox-API
topic: developer guide
description: Deze handleiding voor ontwikkelaars bevat stappen waarmee u sandbox-API kunt gebruiken voor het beheer van sandboxen in Experience Platform en voorbeelden van API-aanroepen voor het uitvoeren van verschillende bewerkingen.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van sandbox-API

Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u sandbox-API kunt gebruiken voor het beheer van sandboxen in Experience Platform en voorbeelden van API-aanroepen voor het uitvoeren van verschillende bewerkingen.

## Aan de slag met de sandbox-API

Als u sandboxen voor uw IMS-organisatie wilt beheren, moet u beschikken over de bevoegdheden voor Sandbox-beheer. Gebruikers zonder toegangsrechten kunnen alleen het eindpunt gebruiken voor het [weergeven van actieve sandboxen voor de huidige gebruiker](./list-active-sandboxes.md). Zie [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over hoe te om zandbaktoestemmingen voor Experience Platform toe te wijzen.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in de documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van de Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Deze gids vereist u om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te hebben voltooid om vraag aan Platform APIs met succes te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.