---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Aan de slag met de API voor observatiegegevens
topic: developer guide
description: Met de API Observability Insights kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document biedt een inleiding op de kernconcepten die u moet kennen voordat u probeert aanroepen te doen naar de API voor observatiegegevens.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

Met de [!DNL Observability Insights] API kunt u metrische gegevens ophalen voor verschillende Adobe Experience Platform-functies. Dit document biedt een inleiding tot de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Observability Insights] API te maken.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. [!DNL Observability Insights] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over hoe te om voorbeeldAPI vraag in de het oplossen van problemengids [van het](../../landing/troubleshooting.md)Experience Platform te lezen.

## Vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor alle aanvragen voor [!DNL Platform] API&#39;s is een header nodig die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

* `x-sandbox-name: {SANDBOX_NAME}`

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Observability Insights] API, ga aan de gids [van het](./metrics.md)metrieke eindpunt te werk.