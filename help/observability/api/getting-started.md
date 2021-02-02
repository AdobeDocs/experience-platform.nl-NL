---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
solution: Experience Platform
title: Aan de slag met de API voor observatiegegevens
topic: developer guide
description: Met de API Observability Insights kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document biedt een inleiding op de kernconcepten die u moet kennen voordat u probeert aanroepen te doen naar de API voor observatiegegevens.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Aan de slag met de [!DNL Observability Insights]-API

Met de API [!DNL Observability Insights] kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Observability Insights] API te maken.

## API-voorbeeldaanroepen lezen

De [!DNL Observability Insights] API documentatie verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over hoe te om voorbeeld API vraag in [Experience Platform het oplossen van problemengids](../../landing/troubleshooting.md) te lezen.

## Vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

* `x-sandbox-name: {SANDBOX_NAME}`

## Volgende stappen

Ga naar de [eindpunthulplijn voor metriek](./metrics.md) om te beginnen met het aanroepen van de [!DNL Observability Insights] API.