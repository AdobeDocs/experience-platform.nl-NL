---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de API voor gegevensverwerking
type: Documentation
description: De gids Aan de slag van de Ingestie van Gegevens API schetst de belangrijkste concepten en de basisfunctionaliteit die u moet kennen alvorens u kunt beginnen gegevens in Experience Platform in te voeren gebruikend APIs.
source-git-commit: 19837e820ab3abdaa0bc8569ad78ce51dec1d21e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Aan de slag met de API voor gegevensverwerking {#getting-started}

Met de eindpunten van de API voor gegevensinname kunt u standaard-CRUD-bewerkingen uitvoeren om gegevens in Adobe Experience Platform in te voeren.

Het gebruik van de API-handleidingen vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met gegevens. Lees de documentatie voor de volgende services voordat u de API voor gegevensinname gebruikt:

* [Inname](./overview.md) in batch: Hiermee kunt u gegevens als batchbestanden in Adobe Experience Platform invoeren.
* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Profile] API eindpunten te maken.

## API-voorbeeldaanroepen lezen

De documentatie van de API van de Ingestie van Gegevens verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen voor [!DNL Platform] API&#39;s is een header vereist die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].
