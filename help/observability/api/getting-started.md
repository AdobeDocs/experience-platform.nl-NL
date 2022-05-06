---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
solution: Experience Platform
title: Aan de slag met de API voor observatiegegevens
topic-legacy: developer guide
description: Met de API Observability Insights kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document biedt een inleiding op de kernconcepten die u moet kennen voordat u probeert aanroepen te doen naar de API voor observatiegegevens.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Aan de slag met de [!DNL Observability Insights] API

De [!DNL Observability Insights] Met API kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [!DNL Observability Insights] API.

## API-voorbeeldaanroepen lezen

De [!DNL Observability Insights] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over het lezen van voorbeeld-API-aanroepen in de [Handleiding voor het oplossen van problemen met Experience Platforms](../../landing/troubleshooting.md).

## Vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Observability Insights] API, ga door naar de [eindhulplijn metrisch eindpunt](./metrics.md).
