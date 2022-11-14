---
title: API-handleiding voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: b76e1bc6d5b346c32ea09612e24b68c6636f7deb
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Handleiding voor API voor gegevenshygiëne

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die deze producten hebben aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**.

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

## Verwijderen van consumenten

>[!IMPORTANT]
>
>Verzoeken om verwijdering van de consument zijn alleen beschikbaar voor organisaties die Adobe Healthcare Shield hebben aangeschaft.

Met de API voor gegevenshygiëne kunt u alle records verwijderen die zijn gekoppeld aan een consumentenidentiteit in een of alle gegevenssets. Alle taken op het gebied van gegevenshygiëne die de identiteit van de consument verwijderen, worden weergegeven door een constructie die een werkorder wordt genoemd. Zie de [eindpuntgids voor werkorders](./workorder.md) voor meer informatie over het werken met de consument verwijdert u de API.

## Quota

Uw organisatie is beperkt tot een vooraf vastgesteld maandelijks taakquotum voor elk type gegevenshygiënebewerking, dat kan variëren afhankelijk van de licentie. Zie de [hulplijn voor quotumeindpunt](./quota.md) voor meer informatie over het bekijken van de huidige quotastatus van uw gegevenshygiëneprocessen.

## Volgende stappen

Deze gids besprak hoe te om de verzoeken van de gegevenshygiëne te beheren gebruikend API vraag. Voor informatie over hoe te om deze acties in de UI van het Platform uit te voeren, zie [UI-gids voor gegevenshygiëne](../ui/overview.md).
