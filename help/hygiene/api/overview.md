---
title: API-handleiding voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Handleiding voor API voor gegevenshygiëne

Met de Data Hygiene-API kunt u via programmacode de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform corrigeren of verwijderen, en kunt u de vervaldatums voor gegevenssets plannen. Deze gids behandelt de eerste vereiste stappen aan het gebruiken van API en verstrekt verbindingen aan meer eindpunt-specifieke documentatie.

## Aan de slag

U hebt toegang tot de API voor gegevenshygiëne via het volgende hoofdpad: `https://platform.adobe.io/data/core/hygiene/`

In deze secties hieronder worden de kernconcepten beschreven die u moet kennen voordat u probeert aanroepen naar de API uit te voeren.

### Waarden verzamelen voor vereiste koppen

Om vraag aan de Hygiene API van Gegevens te maken, moet u uw authentificatiegeloofsbrieven eerst verzamelen. Volg de [&#x200B; API authentificatiegids &#x200B;](../../landing/api-authentication.md) om waarden voor elk van de vereiste kopballen voor de Hygiene API van Gegevens te produceren, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

### API-voorbeeldaanroepen lezen

Dit document bevat een voorbeeld-API-aanroep om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/api-guide.md#sample-api) in de begonnen gids voor Experience Platform APIs te lezen.

## Verlopen gegevensset

Een gegevenssetvervaldatum is een tijd-vertraagde actie &quot;schrapt een dataset&quot;. Door een datasetvervaldatum te creëren, specificeert u een toekomstige tijd waarbij die dataset zou moeten worden geschrapt. Zie de [&#x200B; gids van het de eindpuntgids van de datasetvervalsing &#x200B;](./dataset-expiration.md) voor details bij het plannen van datasetvervaldatums in API.

## Opnemen wordt verwijderd

>[!IMPORTANT]
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Zij zijn **niet** om voor de verzoeken van de rechten van gegevenssubject (naleving) zoals met betrekking tot privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) te worden gebruikt. Voor alle gevallen van het nalevingsgebruik, gebruik [&#x200B; Adobe Experience Platform Privacy Service &#x200B;](../../privacy-service/home.md) in plaats daarvan.

Met de API voor gegevenshygiëne kunt u alle records verwijderen die aan een identiteit in een of alle gegevenssets zijn gekoppeld. Alle taken van de gegevenslevenscyclus die identiteiten schrappen worden vertegenwoordigd door een constructie genoemd een het werkorde. Zie de [&#x200B; gids van het het eindpunt van de werkorde &#x200B;](./workorder.md) voor details bij het werken met verslag schrapt in API.

## Quota

Uw organisatie is beperkt tot een vooraf vastgesteld maandelijks taakquotum voor elk type levenscyclusbewerking van gegevens, dat kan variëren afhankelijk van licenties. Zie de [&#x200B; gids van het quotaeindpunt &#x200B;](./quota.md) voor details bij het bekijken van het huidige quotestatus van uw processen van de gegevenslevenscyclus.

## Volgende stappen

In deze handleiding wordt beschreven hoe u aanvragen voor de levenscyclus van gegevens kunt beheren met behulp van API-aanroepen. Voor informatie over hoe te om deze acties in Experience Platform UI uit te voeren, zie de [&#x200B; gids UI van de de levenscyclus van gegevens &#x200B;](../ui/overview.md).
