---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Aan de slag met de Real-time API voor klantprofiel
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Aan de slag met de [!DNL Real-time Customer Profile] API {#getting-started}

Met behulp van de [!DNL Real-time Customer Profile] API kunt u elementaire CRUD-bewerkingen uitvoeren op profielbronnen, zoals het configureren van berekende kenmerken, het openen van entiteiten, het exporteren van profielgegevens en het verwijderen van overbodige gegevenssets of batches.

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van het Adobe Experience Platform betrokken bij het werken met [!DNL Profile] gegevens. Voordat u begint te werken met de [!DNL Real-time Customer Profile] API, raadpleegt u de documentatie voor de volgende services:

* [!DNL Real-time Customer Profile](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Profile] API eindpunten te maken.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe aanvragen correct moeten worden opgemaakt. [!DNL Real-time Customer Profile] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## Vereiste koppen

The API documentation also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Voor aanvragen voor [!DNL Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

All requests with a payload in the request body (such as POST, PUT, and PATCH calls) must include a `Content-Type` header. Accepted values specific to each call are provided in the call parameters.

## Volgende stappen

To begin making calls using the [!DNL Real-time Customer Profile] API, select one of the available endpoint guides.