---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Aan de slag met Self-Serve Sources (Batch SDK)
topic-legacy: developer guide
description: Dit document verstrekt een inleiding aan de eerste vereiste informatie u moet kennen alvorens te proberen om een nieuwe bron tot stand te brengen gebruikend Zelfbediening Bronnen (de Band SDK).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Aan de slag met Self-Serve Sources (Batch SDK)

Met Self-Serve Sources (Batch SDK) kunt u uw eigen REST-gebaseerde bron integreren en batchgegevens naar Adobe Experience Platform overbrengen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Vereisten

Als u Self-Serve Sources (Batch SDK) wilt gebruiken, dient u ervoor te zorgen dat u toegang hebt tot een IMS Organisatie-sandbox die is ingericht met Adobe Experience Platform Sources.

Deze handleiding vereist ook een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De Self-Serve Bronnen (Batch SDK) en [!DNL Flow Service] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

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

Als u een nieuwe bron wilt maken met Self-Serve Sources (Batch SDK), raadpleegt u de zelfstudie over [een nieuwe bron maken](./create.md).
