---
title: API-handleiding voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Handleiding voor API voor gegevenshygiëne

Met de Data Hygiene-API kunt u via programmacode de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform corrigeren of verwijderen, en kunt u de vervaldatums voor gegevenssets plannen. Deze gids behandelt de eerste vereiste stappen aan het gebruiken van API en verstrekt verbindingen aan meer eindpunt-specifieke documentatie.

## Aan de slag

U hebt toegang tot de API voor gegevenshygiëne via het volgende hoofdpad: `https://platform.adobe.io/data/core/hygiene/`

In deze secties hieronder worden de kernconcepten beschreven die u moet kennen voordat u probeert aanroepen naar de API uit te voeren.

### Waarden verzamelen voor vereiste koppen

Om vraag aan de Hygiene API van Gegevens te maken, moet u uw authentificatiegeloofsbrieven eerst verzamelen. Volg de [API-verificatiegids](../../landing/api-authentication.md) om waarden voor elk van de vereiste kopballen voor de API van de Hygiëne van Gegevens te produceren, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

### API-voorbeeldaanroepen lezen

Dit document bevat een voorbeeld-API-aanroep om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/api-guide.md#sample-api) in de gids Aan de slag voor Experience Platform APIs.

## Verlopen gegevensset

Een gegevenssetvervaldatum is een tijd-vertraagde actie &quot;schrapt een dataset&quot;. Door een datasetvervaldatum te creëren, specificeert u een toekomstige tijd waarbij die dataset zou moeten worden geschrapt. Zie de [eindpuntgids gegevensset](./dataset-expiration.md) voor meer informatie over het plannen van datasetvervaldata in API.

## Opnemen wordt verwijderd

>[!IMPORTANT]
>
>Aanvragen voor het verwijderen van records zijn alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Gezondheidsschild**.
>
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Ze zijn **niet** te gebruiken voor verzoeken om rechten van betrokkenen (naleving) met betrekking tot privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR). Gebruik voor alle gevallen waarin aan de eisen wordt voldaan [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) in plaats daarvan.

Met de API voor gegevenshygiëne kunt u alle records verwijderen die aan een identiteit in een of alle gegevenssets zijn gekoppeld. Alle taken van de gegevenslevenscyclus die identiteiten schrappen worden vertegenwoordigd door een constructie genoemd een het werkorde. Zie de [eindpuntgids voor werkorders](./workorder.md) verwijdert de API voor meer informatie over het werken met records.

## Quota

Uw organisatie is beperkt tot een vooraf vastgesteld maandelijks taakquotum voor elk type levenscyclusbewerking van gegevens, dat kan variëren afhankelijk van licenties. Zie de [hulplijn voor quotumeindpunt](./quota.md) voor meer informatie over het bekijken van de huidige quotastatus van uw processen van de gegevenslevenscyclus.

## Volgende stappen

In deze handleiding wordt beschreven hoe u aanvragen voor de levenscyclus van gegevens kunt beheren met behulp van API-aanroepen. Voor informatie over hoe te om deze acties in Platform UI uit te voeren, zie [UI-gids voor gegevenslevenscyclus](../ui/overview.md).
