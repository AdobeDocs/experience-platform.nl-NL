---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van toegangsbeheer
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Handleiding voor ontwikkelaars van toegangsbeheer

Toegangsbeheer voor Experience Platform wordt beheerd via de [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden. Zie het [toegangsbeheeroverzicht](../home.md) voor meer informatie.

Deze ontwikkelaarsgids verstrekt informatie over hoe te om uw verzoeken aan de [Controle API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)van de Toegang te formatteren, en behandelt de volgende verrichtingen:

- [De namen van de lijst van toestemmingen en middeltypes](./permissions-and-resource-types.md)
- [Effectief beleid voor de huidige gebruiker weergeven](./effective-policies.md)

## Aan de slag

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Registratie API van het Schema te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene **API formaat**, een steekproef **verzoek** die vereiste kopballen tonen en behoorlijk geformatteerde lading, en een steekproefreactie **** voor een succesvolle vraag.