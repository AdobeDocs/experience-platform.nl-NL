---
keywords: Experience Platform;home;popular topics;access control;api;getting started
solution: Experience Platform
title: Handleiding voor ontwikkelaars van toegangsbeheer
topic: developer guide
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende mogelijkheden van Platforms beheren met de Adobe Admin Console. De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Registratie API van het Schema te maken.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# [!DNL Access control] ontwikkelaarsgids

[!DNL Access control] for [!DNL Experience Platform] wordt toegediend via de [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden. Zie het [toegangsbeheeroverzicht](../home.md) voor meer informatie.

Deze ontwikkelaarsgids verstrekt informatie over hoe te om uw verzoeken aan te maken, [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)en behandelt de volgende verrichtingen:

- [De namen van de lijst van toestemmingen en middeltypes](./permissions-and-resource-types.md)
- [Effectief beleid voor de huidige gebruiker weergeven](./effective-policies.md)

## Aan de slag

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Schema Registry] API te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
