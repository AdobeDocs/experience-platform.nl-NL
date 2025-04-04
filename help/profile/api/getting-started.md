---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Aan de slag met de Real-Time Customer Profile API
type: Documentation
description: De gids van het begin van het Profiel API schetst de belangrijkste concepten en de basisfunctionaliteit die u moet kennen om eindpunten van API van het Profiel van de Klant in real time te gebruiken om basisbewerkingen van CRUD tegen de gegevens van het Profiel uit te voeren.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Aan de slag met de [!DNL Real-Time Customer Profile] API {#getting-started}

Gebruikend Echte - de eindpunten van het Profiel van de Klant van tijdProfiel, kunt u basisbewerkingen van CRUD tegen de gegevens van het Profiel uitvoeren, zoals het vormen van gegevens verwerkte attributen, de toegang tot entiteiten, het uitvoeren van de gegevens van het Profiel, en het schrappen van onnodige datasets of partijen.

Voor het gebruik van de handleiding voor ontwikkelaars is een goed begrip vereist van de verschillende Adobe Experience Platform-services die betrokken zijn bij het werken met [!DNL Profile] -gegevens. Voordat u begint te werken met de [!DNL Real-Time Customer Profile] API, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-Time Customer Profile]](../home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): verbeter een beter beeld van uw klant en zijn gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Hiermee kunt u een publiek maken op basis van realtime gegevens in het klantprofiel.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde raamwerk waarmee Experience Platform gegevens over de ervaring van klanten organiseert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen van [!DNL Profile] API-eindpunten te kunnen uitvoeren.

## API-voorbeeldaanroepen lezen

De API-documentatie van [!DNL Real-Time Customer Profile] biedt voorbeeld-API-aanroepen om aan te tonen hoe aanvragen op de juiste manier kunnen worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist u ook om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] eindpunten met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen van [!DNL Experience Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## Volgende stappen

Selecteer een van de beschikbare eindpunthulplijnen als u wilt beginnen met het aanroepen van de API [!DNL Real-Time Customer Profile] .
