---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Aan de slag met Self-Serve Bronnen (Batch SDK)
description: Dit document verstrekt een inleiding aan de eerste vereiste informatie u moet kennen alvorens om een nieuwe bron te proberen tot stand te brengen gebruikend Zelfbediening Bronnen (Batch SDK).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Aan de slag met Self-Serve Bronnen (Batch SDK)

Met Self-Serve Sources (Batch SDK) kunt u uw eigen REST-gebaseerde bron integreren om batchgegevens naar Adobe Experience Platform over te brengen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) te maken.

## Vereisten

Als u Self-Serve Sources (Batch SDK) wilt gebruiken, moet u ervoor zorgen dat u toegang hebt tot een organisatie-sandbox die is ingericht met Adobe Experience Platform Sources.

Deze handleiding vereist ook een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## API-voorbeeldaanroepen lezen

De Self-Serve Bronnen (Batch SDK) en de [!DNL Flow Service] API-documentatie bieden voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Experience Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in Experience Platform, inclusief die van [!DNL Flow Service] , zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen aan Experience Platform API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Experience Platform, zie de [ zandbakdocumentatie ](../../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Beginnen creërend een nieuwe bron met Zelfbediening Bronnen (Partij SDK), zie het leerprogramma op [ creërend een nieuwe bron ](./create.md).
