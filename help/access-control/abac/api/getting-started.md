---
keywords: Experience Platform;huis;populaire onderwerpen;Op kenmerk-Gebaseerd Toegangsbeheer;op attribuut-gebaseerde toegangscontrole
title: Aan de slag met het op kenmerken gebaseerde toegangsbeheer
description: Met het op kenmerken gebaseerde toegangsbeheer kunt u rollen en beleid in Adobe Experience Platform programmatisch beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Aan de slag met het op kenmerken gebaseerde toegangsbeheer

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

Deze ontwikkelaarsgids verstrekt stappen om u te helpen het op attribuut-gebaseerde toegangsbeheer gebruiken om rollen, producten, toestemmingscategorieën, en toestemmingsreeksen in Adobe Experience Platform te beheren, en omvat steekproefAPI vraag voor het uitvoeren van diverse verrichtingen.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in de documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

## Waarden verzamelen voor vereiste koppen

Voor deze handleiding is het vereist dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag aan Platform APIs te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.

Zie de volgende API leerprogramma&#39;s beginnen vraag aan op attribuut-gebaseerde toegangsbeheer API te maken:

* [Het eindpunt van rollen](./roles.md)
* [Het eindpunt van producten](./products.md)
