---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de Real-Time Customer Profile API
topic-legacy: guide
type: Documentation
description: In de gids Aan de slag met profiel API worden de belangrijkste concepten en basisfuncties beschreven die u moet kennen om de eindpunten van de API-eindpunten van het profiel van de klant in real time te kunnen gebruiken om standaard-CRUD-bewerkingen uit te voeren ten opzichte van profielgegevens.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Aan de slag met de [!DNL Real-time Customer Profile] API {#getting-started}

Met de eindpunten van de API van het Profiel van de Klant in real time, kunt u basisbewerkingen van CRUD tegen de gegevens van het Profiel uitvoeren, zoals het vormen van gegevens verwerkte attributen, de toegang tot entiteiten, het uitvoeren van de gegevens van het Profiel, en het schrappen van onnodige datasets of partijen.

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van Adobe Experience Platform betrokken bij het werken met [!DNL Profile] gegevens. Voordat u begint te werken met de [!DNL Real-time Customer Profile] API, raadpleeg de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Profile] API-eindpunten.

## API-voorbeeldaanroepen lezen

De [!DNL Real-time Customer Profile] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe aanvragen correct moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

## Vereiste koppen

De API-documentatie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag te maken aan [!DNL Platform] eindpunten. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken om [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een omvatten `Content-Type` header. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Real-time Customer Profile] API, selecteert u een van de beschikbare eindpunthulplijnen.
