---
solution: Experience Platform
title: Aan de slag met de Unified Tags API
description: De volgende documentatie verstrekt extra informatie die u moet weten om met de Verenigde Tags API met succes te werken.
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Aan de slag met de API voor Unified Tags {#getting-started}

Met de API voor Unified Tags kunt u uw bedrijfsobjecten in Adobe Experience Platform indelen en beheren.

De volgende secties verstrekken extra informatie die u zult moeten weten om met de Verenigde Tags API met succes te werken.

## API-voorbeeldaanroepen lezen

De Unified Tags API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

## Vereiste koppen

De API-documentatie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag aan de eindpunten van het Platform te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over het werken met sandboxen in [!DNL Experience Platform], zie de [sandboxen - documentatie](../../sandboxes/home.md).

## Volgende stappen

Om vraag te maken die de Verenigde Markeringen API gebruikt, selecteer één van de beschikbare eindpuntgidsen of gebruikend de linkernavigatie of binnen [overzicht van ontwikkelaarsgids](./overview.md)
