---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Aan de slag met de Real-time API voor klantprofiel
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Getting started with the [!DNL Real-time Customer Profile] API {#getting-started}

Met behulp van de [!DNL Real-time Customer Profile] API kunt u elementaire CRUD-bewerkingen uitvoeren op profielbronnen, zoals het configureren van berekende kenmerken, het openen van entiteiten, het exporteren van profielgegevens en het verwijderen van overbodige gegevenssets of batches.

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van Adobe Experience Platform betrokken bij het werken met [!DNL Profile] gegevens. Voordat u begint te werken met de [!DNL Real-time Customer Profile] API, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Profile] API eindpunten te maken.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe aanvragen correct moeten worden opgemaakt. [!DNL Real-time Customer Profile] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen voor [!DNL Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## Volgende stappen

Om beginnen het maken vraag gebruikend [!DNL Real-time Customer Profile] API, selecteer één van de beschikbare eindpuntgidsen.