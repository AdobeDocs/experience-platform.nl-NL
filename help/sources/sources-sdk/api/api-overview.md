---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Self-Serve Sources (Batch SDK) API Guide
description: Dit document biedt een overzicht van het proces voor het maken van een nieuwe bron, inclusief stappen voor het ophalen, schrijven en verzenden van een nieuwe verbindingsspecificatie met behulp van de Flow Service API.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Self-Serve Sources (Batch SDK) API Guide

Dit document verstrekt een overzicht van het proces om een nieuwe bron tot stand te brengen, met inbegrip van stappen op om een nieuwe verbindingsspecificatie te schrijven en voor te leggen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Experience Platform. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

De [!DNL Flow Service] API verstrekt verscheidene eindpunten die u toestaan om de verbinding en stroomspecificaties voor een nieuwe bron programmatically te beheren die u door Zelfbediening Bronnen (Batch SDK) integreert.

## Een nieuwe verbindingsspecificatie maken

De eerste stap in het vormen van een nieuwe bron is een nieuwe verbindingsspecificatie tot stand te brengen.

Verbindingsspecificaties retourneren de verbindingseigenschappen van een bron. Zij omvatten authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen en een vaste identiteitskaart van de verbindingsspecificatie die aan een bepaalde bron wordt toegewezen. De specificaties van de verbinding zijn huurder en organisatie agnostisch. Een typische verbindingsspecificatie bevat basisinformatie over een bepaalde bron en drie verschillende secties: `authSpec`, `sourceSpec` en `exploreSpec` .

Voor gedetailleerde instructies, zie de gids bij [ het creëren van een nieuwe verbindingsspecificatie ](./create.md). Voor informatie over de eigenschappen en de waarden die voor een verbindingsspecificatie, met inbegrip van details bij het vormen van authentificatie worden gebruikt, bron, en onderzoeken specificaties, zie het [ document van de configuratieopties ](../config/config.md).

## Stroomspecificaties bijwerken

Nadat u een verbindingsspecificatie hebt gemaakt, moet u de `RestStorageToAEP` flow-specificatie toevoegen om de gegevensbron in staat te stellen een gegevensstroom te maken.

De specificaties van de stroom bevatten informatie die een stroom bepaalt, met inbegrip van bron en doel verbindings IDs die het steunt, transformatiespecificaties die nodig zijn om op de gegevens worden toegepast, en het plannen van parameters die worden vereist om een stroom te produceren.

Voor gedetailleerde instructies, zie de gids bij [ het bijwerken stroomspecificaties ](./update-flow-specs.md).

## De verbindingsspecificatie bijwerken

U kunt uw verbindingsspecificatie bijwerken door een PUT-aanvraag in te dienen bij de [!DNL Flow Service] API. Zie de gids bij [ het bijwerken van uw verbindingsspecificaties ](./update-connection-specs.md) voor meer informatie.

## Uw bron verzenden

Als u uw bron voor integratie naar Experience Platform wilt verzenden, moet u eerst de volledige API-workflow voor bronnen van [!DNL Flow Service] voltooien om ervoor te zorgen dat uw bron goed werkt. Als je bron goed werkt, kun je doorgaan en contact opnemen met je Adobe-vertegenwoordiger voor verificatie en promotie. Zie de gids bij [ het testen en het voorleggen van uw bron ](./submit.md) voor meer informatie

## Volgende stappen

Om te beginnen gebruikend [!DNL Flow Service] API en een nieuwe bron door Zelfbediening Bronnen (Partij SDK) tot stand te brengen, lees [ begonnen gids ](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
