---
keywords: Experience Platform;home;populaire onderwerpen;Op kenmerk-Gebaseerd Toegangsbeheer;op attributen-gebaseerd toegangsbeheer
title: Aan de slag met de API voor toegangsbeheer op basis van kenmerken
description: Met de API voor toegangsbeheer op basis van kenmerken kunt u rollen en toegangsbeleid in Adobe Experience Platform programmatisch beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# Aan de slag met de op kenmerken gebaseerde API voor toegangsbeheer

Deze ontwikkelaarsgids verstrekt stappen om u te helpen de op attribuut-gebaseerde toegangsbeheer API gebruiken om rollen, producten, toestemmingscategorieën, en toestemmingsreeksen in Adobe Experience Platform te beheren, en omvat steekproefAPI vraag voor het uitvoeren van diverse verrichtingen.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in de documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Deze gids vereist u om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan Experience Platform APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Naast de verificatieheaders is voor alle aanvragen een header vereist met de naam van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.

Zie de volgende API leerprogramma&#39;s beginnen vraag aan op attribuut-gebaseerde toegangsbeheer API te maken:

* [Het eindpunt van rollen](./roles.md)
* [Het eindpunt van producten](./products.md)
