---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de API voor gegevensverwerking
type: Documentation
description: De gids Aan de slag van de Ingestie van Gegevens API schetst de belangrijkste concepten en de basisfunctionaliteit die u moet kennen alvorens u kunt beginnen gegevens in Experience Platform in te voeren gebruikend APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Aan de slag met de API voor gegevensverwerking {#getting-started}

Met de eindpunten van de API voor gegevensinname kunt u standaard-CRUD-bewerkingen uitvoeren om gegevens in Adobe Experience Platform in te voeren.

Het gebruik van de API-handleidingen vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met gegevens. Lees de documentatie voor de volgende services voordat u de API voor gegevensinname gebruikt:

* [Inname in batch](./overview.md): Hiermee kunt u gegevens als batchbestanden in Adobe Experience Platform invoeren.
* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Profile] API-eindpunten.

## API-voorbeeldaanroepen lezen

De documentatie van de API van de Ingestie van Gegevens verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

## Vereiste koppen

De API-documentatie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag te maken aan [!DNL Platform] eindpunten. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een omvatten `Content-Type` header. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken om [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).
