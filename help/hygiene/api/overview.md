---
title: API-handleiding voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Handleiding voor API voor gegevenshygiëne

Met de Data Hygiene-API kunt u via programmacode de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform corrigeren of verwijderen, en kunt u de vervaldatums voor gegevenssets plannen. Deze gids behandelt de eerste vereiste stappen aan het gebruiken van API en verstrekt verbindingen aan meer eindpunt-specifieke documentatie.

## Aan de slag

U hebt toegang tot de API voor gegevenshygiëne via het volgende hoofdpad: `https://platform.adobe.io/data/core/hygiene/`

In deze secties hieronder worden de kernconcepten beschreven die u moet kennen voordat u probeert aanroepen naar de API uit te voeren.

### Waarden verzamelen voor vereiste koppen

Om vraag aan de Hygiene API van Gegevens te maken, moet u uw authentificatiegeloofsbrieven eerst verzamelen. Volg de [ API authentificatiegids ](../../landing/api-authentication.md) om waarden voor elk van de vereiste kopballen voor de Hygiene API van Gegevens te produceren, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

### API-voorbeeldaanroepen lezen

Dit document bevat een voorbeeld-API-aanroep om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/api-guide.md#sample-api) in de begonnen gids voor Experience Platform APIs te lezen.

## Verlopen gegevensset

Een gegevenssetvervaldatum is een tijd-vertraagde actie &quot;schrapt een dataset&quot;. Door een datasetvervaldatum te creëren, specificeert u een toekomstige tijd waarbij die dataset zou moeten worden geschrapt. Zie de [ gids van het de eindpuntgids van de datasetvervalsing ](./dataset-expiration.md) voor details bij het plannen van datasetvervaldatums in API.

## Opnemen wordt verwijderd

>[!IMPORTANT]
>
>De schrappingsverzoeken van het verslag zijn slechts beschikbaar voor organisaties die **het Schild van de Gezondheidszorg van Adobe** hebben gekocht.
>
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Zij zijn **niet** om voor de verzoeken van de rechten van gegevenssubject (naleving) zoals met betrekking tot privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) te worden gebruikt. Voor alle gevallen van het nalevingsgebruik, gebruik [ Adobe Experience Platform Privacy Service ](../../privacy-service/home.md) in plaats daarvan.

Met de API voor gegevenshygiëne kunt u alle records verwijderen die aan een identiteit in een of alle gegevenssets zijn gekoppeld. Alle taken van de gegevenslevenscyclus die identiteiten schrappen worden vertegenwoordigd door een constructie genoemd een het werkorde. Zie de [ gids van het het eindpunt van de werkorde ](./workorder.md) voor details bij het werken met verslag schrapt in API.

## Quota

Uw organisatie is beperkt tot een vooraf vastgesteld maandelijks taakquotum voor elk type levenscyclusbewerking van gegevens, dat kan variëren afhankelijk van licenties. Zie de [ gids van het quotaeindpunt ](./quota.md) voor details bij het bekijken van het huidige quotestatus van uw processen van de gegevenslevenscyclus.

## Volgende stappen

In deze handleiding wordt beschreven hoe u aanvragen voor de levenscyclus van gegevens kunt beheren met behulp van API-aanroepen. Voor informatie over hoe te om deze acties in Experience Platform UI uit te voeren, zie de [ gids UI van de de levenscyclus van gegevens ](../ui/overview.md).
