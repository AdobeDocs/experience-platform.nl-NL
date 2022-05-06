---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: Aan de slag met de sandbox-API
topic-legacy: developer guide
description: Met de sandbox-API kunnen ontwikkelaars sandboxen in Adobe Experience Platform programmatisch beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Aan de slag met de sandbox-API

Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u sandbox-API kunt gebruiken voor het beheer van sandboxen in Experience Platform en voorbeelden van API-aanroepen voor het uitvoeren van verschillende bewerkingen.

## Vereisten

Als u sandboxen voor uw IMS-organisatie wilt beheren, moet u beschikken over de bevoegdheden voor Sandbox-beheer. Gebruikers zonder toegangsrechten kunnen alleen de [beschikbaar sandboxeindpunt](./available.md) om actieve sandboxen voor de huidige gebruiker weer te geven. Zie de [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over het toewijzen van sandboxmachtigingen voor Experience Platform.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in de documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

### Waarden verzamelen voor vereiste koppen

Voor deze handleiding is het vereist dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag aan Platform APIs te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
