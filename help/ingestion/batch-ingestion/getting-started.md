---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de API voor gegevensverwerking
type: Documentation
description: In de gids Aan de slag met de API voor gegevensinsluiting worden de belangrijkste concepten en basisfuncties beschreven die u moet kennen voordat u gegevens met API's kunt invoeren in Experience Platform.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Aan de slag met de API voor gegevensverwerking {#getting-started}

Met de eindpunten van de API voor gegevensinname kunt u standaard-CRUD-bewerkingen uitvoeren om gegevens in Adobe Experience Platform in te voeren.

Het gebruik van de API-handleidingen vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met gegevens. Lees de documentatie voor de volgende services voordat u de API voor gegevensinname gebruikt:

* [ Inname van de Partij ](./overview.md): Staat u toe om gegevens in Adobe Experience Platform als partijdossiers in te voeren.
* [[!DNL Real-Time Customer Profile]](../home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde raamwerk waarmee Experience Platform gegevens over de ervaring van klanten organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen van [!DNL Profile] API-eindpunten te kunnen uitvoeren.

## API-voorbeeldaanroepen lezen

De documentatie van de API van de Ingestie van Gegevens verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist u ook om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] eindpunten met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen van [!DNL Experience Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).
