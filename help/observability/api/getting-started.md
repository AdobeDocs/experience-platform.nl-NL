---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
solution: Experience Platform
title: Aan de slag met de API voor observatiegegevens
description: Met de API Observability Insights kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document biedt een inleiding op de kernconcepten die u moet kennen voordat u probeert aanroepen te doen naar de API voor observatiegegevens.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Aan de slag met de [!DNL Observability Insights] API

Met de API [!DNL Observability Insights] kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document bevat een inleiding op de kernconcepten die u moet kennen voordat u de API van [!DNL Observability Insights] aanroept.

## API-voorbeeldaanroepen lezen

De API-documentatie van [!DNL Observability Insights] biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie over hoe te voorbeeld API vraag in de [ het oplossen van problemengids van Experience Platform ](../../landing/troubleshooting.md) lezen.

## Vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Volgende stappen

Begin makend vraag gebruikend [!DNL Observability Insights] API, ga aan de [ gids van het metrieke eindpunt ](./metrics.md) te werk.
