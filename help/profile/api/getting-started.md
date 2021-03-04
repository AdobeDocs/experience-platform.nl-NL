---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de Real-Time Customer Profile API
topic: hulplijn
type: Documentatie
description: In de gids Aan de slag met profiel-API worden de belangrijkste concepten en basisfuncties beschreven die u moet kennen om de eindpunten van de API-eindpunten van het profiel van de klant in realtime te kunnen gebruiken om standaard-CRUD-bewerkingen uit te voeren ten opzichte van profielgegevens.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Aan de slag met de [!DNL Real-time Customer Profile]-API {#getting-started}

Met de eindpunten van de API van het Profiel van de Klant in real time, kunt u basisbewerkingen van CRUD tegen de gegevens van het Profiel uitvoeren, zoals het vormen van gegevens verwerkte attributen, de toegang tot entiteiten, het uitvoeren van de gegevens van het Profiel, en het schrappen van onnodige datasets of partijen.

Het gebruik van de ontwikkelaarshandleiding vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met [!DNL Profile]-gegevens. Lees de documentatie voor de volgende services voordat u begint te werken met de [!DNL Real-time Customer Profile]-API:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Profile] API eindpunten te maken.

## API-voorbeeldaanroepen lezen

De [!DNL Real-time Customer Profile] API documentatie verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen voor [!DNL Platform] API&#39;s is een header vereist die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## Volgende stappen

Om beginnen het maken vraag gebruikend [!DNL Real-time Customer Profile] API, selecteer één van de beschikbare eindpuntgidsen.