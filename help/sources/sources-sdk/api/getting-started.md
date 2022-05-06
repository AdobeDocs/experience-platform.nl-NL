---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Aan de slag met Sources SDK (bèta)
topic-legacy: developer guide
description: Dit document verstrekt een inleiding aan de eerste vereiste informatie u moet kennen alvorens te proberen om een nieuwe bron tot stand te brengen gebruikend Bronnen SDK.
hide: true
hidefromtoc: true
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Aan de slag met Sources SDK (bèta)

>[!IMPORTANT]
>
>Bronnen-SDK bevindt zich momenteel in bètaversie en uw organisatie heeft mogelijk nog geen toegang tot deze SDK. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Bronnen met SDK kunt u uw eigen op REST gebaseerde bron integreren om gegevens over te brengen naar Adobe Experience Platform. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Vereisten

Om Bronnen SDK te gebruiken, moet u ervoor zorgen dat u toegang hebt tot een IMS Organisatie Sandbox voorzien van de Bronnen van Adobe Experience Platform.

Deze handleiding vereist ook een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De SDK van Bronnen en [!DNL Flow Service] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

## Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle middelen in Platform, met inbegrip van die welke toebehoren aan [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Platform raadpleegt u de [sandbox-documentatie](../../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Beginnen creërend een nieuwe bron met Bronnen SDK, zie het leerprogramma op [een nieuwe bron maken](./create.md).
