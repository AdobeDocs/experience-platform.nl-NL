---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;api;aan de slag
solution: Experience Platform
title: API-handleiding voor toegangsbeheer
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende Experience Platform-mogelijkheden beheren met behulp van de Adobe Admin Console. De volgende secties verstrekken extra informatie die de ontwikkelaars zullen moeten weten om met succes vraag aan de Registratie API van het Schema te maken.
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# [!DNL Access Control] API-handleiding

[!DNL Access control] voor [!DNL Experience Platform] wordt beheerd door [ Adobe Admin Console ](https://adminconsole.adobe.com). Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers koppelen aan machtigingen en sandboxen. Zie het [ overzicht van de toegangscontrole ](../home.md) voor meer informatie.

Deze ontwikkelaarsgids verstrekt informatie over hoe te om uw verzoeken aan [[!DNL Access Control API] te formatteren ](https://www.adobe.io/experience-platform-apis/references/access-control/), en behandelt de volgende verrichtingen:

- [De namen van de lijst van toestemmingen en middeltypes](./permissions-and-resource-types.md)
- [Effectief toegangsbeleid voor de huidige gebruiker weergeven](./effective-policies.md)

## Aan de slag

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen naar de [!DNL Access Control] API te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
