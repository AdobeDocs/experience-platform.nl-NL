---
keywords: Experience Platform;thuis;populaire onderwerpen;toegangsbeheer;api;aan de slag
solution: Experience Platform
title: API-handleiding voor toegangsbeheer
topic-legacy: developer guide
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende mogelijkheden van Platforms beheren met de Adobe Admin Console. De volgende secties verstrekken extra informatie die de ontwikkelaars zullen moeten weten om met succes vraag aan de Registratie API van het Schema te maken.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# [!DNL Access Control] API-handleiding

[!DNL Access control] for [!DNL Experience Platform] wordt toegediend via de [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden. Zie de [toegangsbeheeroverzicht](../home.md) voor meer informatie .

In deze handleiding voor ontwikkelaars vindt u informatie over het opmaken van uw verzoeken aan de [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)en heeft betrekking op de volgende activiteiten:

- [De namen van de lijst van toestemmingen en middeltypes](./permissions-and-resource-types.md)
- [Effectief beleid voor de huidige gebruiker weergeven](./effective-policies.md)

## Aan de slag

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Access Control] API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
