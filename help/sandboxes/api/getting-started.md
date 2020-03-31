---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van sandbox-API
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# Handleiding voor ontwikkelaars van sandbox-API

Sandboxen in het Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.

Deze ontwikkelaarshandleiding bevat stappen waarmee u de sandbox-API kunt gebruiken voor het beheer van sandboxen in het Experience Platform. Deze handleiding bevat voorbeelden van API-aanroepen voor het uitvoeren van verschillende bewerkingen.

## Aan de slag met de sandbox-API

Als u sandboxen voor uw IMS-organisatie wilt beheren, moet u beschikken over de bevoegdheden voor Sandbox-beheer. Gebruikers zonder toegangsrechten kunnen alleen het eindpunt gebruiken voor het [weergeven van actieve sandboxen voor de huidige gebruiker](./list-active-sandboxes.md). Zie het [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over hoe te om zandbaktoestemmingen voor het Platform van de Ervaring toe te wijzen.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in de documentatie voor steekproef API vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Deze gids vereist u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan Platform APIs met succes te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene **API formaat**, een steekproef **verzoek** die vereiste kopballen tonen en behoorlijk geformatteerde lading, en een steekproefreactie **** voor een succesvolle vraag.