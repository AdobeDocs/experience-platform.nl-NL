---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Aan de slag met de Real-Time Customer Profile API {#getting-started}

Met de Real-time API voor klantprofiel kunt u elementaire CRUD-bewerkingen uitvoeren op profielbronnen, zoals het configureren van berekende kenmerken, het openen van entiteiten, het exporteren van profielgegevens en het verwijderen van overbodige gegevenssets of batches.

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van het Adobe Experience Platform betrokken bij het werken met de gegevens van het Profiel. Lees de documentatie voor de volgende services voordat u begint te werken met de Real-time Customer Profile API:

* [Klantprofiel](../home.md)in realtime: Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Identiteitsdienst](../../identity-service/home.md)Adobe Experience Platform: Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Segmenteringsservice](../../segmentation/home.md)Adobe Experience Platform: Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de eindpunten van profiel API te maken.

## API-voorbeeldaanroepen lezen

De documentatie van de API van het Profiel van de Klant in real time verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan Platform eindpunten met succes te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, GEPUT, en de vraag van de PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## Volgende stappen

Beginnen het maken van vraag gebruikend Real-time het Profiel van de Klant API, selecteer één van de beschikbare eindpuntgidsen.