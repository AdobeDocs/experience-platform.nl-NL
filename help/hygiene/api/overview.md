---
title: API-handleiding voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Handleiding voor API voor gegevenshygiëne

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die Adobe Shield voor gezondheidszorg hebben aangeschaft.

De hygiëne-API van Gegevens staat u toe om de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatically te verbeteren of te schrappen, evenals programma tijd-aan-levende (TTL) protocollen voor datasets. Deze gids behandelt de eerste vereiste stappen aan het gebruiken van API en verstrekt verbindingen aan meer eindpunt-specifieke documentatie.

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

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## Tijd om te leven (TTL) voor datasets

Een dataset TTL is een tijd-vertraagde &quot;schrapping een dataset&quot;actie. Door TTL te creëren, specificeert u een toekomstige tijd waarop die dataset zou moeten worden geschrapt. Zie de [dataset TTL eindpuntgids](./ttl.md) voor details over het plannen van dataset TTLs in API.

## Volgende stappen

Deze gids besprak hoe te om de verzoeken van de gegevenshygiëne te beheren gebruikend API vraag. Voor informatie over hoe te om deze acties in de UI van het Platform uit te voeren, zie [UI-gids voor gegevenshygiëne](../ui/overview.md).
