---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de API voor gegevensverwerking
type: Documentation
description: De gids Aan de slag van de Ingestie van Gegevens API schetst de belangrijkste concepten en de basisfunctionaliteit die u moet kennen alvorens u kunt beginnen gegevens in Experience Platform in te voeren gebruikend APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Aan de slag met de API voor gegevensverwerking {#getting-started}

Met de eindpunten van de API voor gegevensinname kunt u standaard-CRUD-bewerkingen uitvoeren om gegevens in Adobe Experience Platform in te voeren.

Het gebruik van de API-handleidingen vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met gegevens. Lees de documentatie voor de volgende services voordat u de API voor gegevensinname gebruikt:

* [ Inname van de Partij ](./overview.md): Staat u toe om gegevens in Adobe Experience Platform als partijdossiers in te voeren.
* [[!DNL Real-Time Customer Profile]](../home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee Platform gegevens voor klantervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen van [!DNL Profile] API-eindpunten te kunnen uitvoeren.

## API-voorbeeldaanroepen lezen

De documentatie van de API van de Ingestie van Gegevens verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist u ook om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Platform] eindpunten met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen van [!DNL Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).
