---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: 'Bronnen: SDK API Guide (bèta)'
topic-legacy: overview
description: Dit document biedt een overzicht van het proces voor het maken van een nieuwe bron, inclusief stappen voor het ophalen, schrijven en verzenden van een nieuwe verbindingsspecificatie met behulp van de Flow Service API.
hide: true
hidefromtoc: true
source-git-commit: b8793a4346e3f6017bdac07a1dd8df75a7341066
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Bronnen: SDK API Guide (bèta)

>[!IMPORTANT]
>
>Bronnen-SDK bevindt zich momenteel in bètaversie en uw organisatie heeft mogelijk nog geen toegang tot deze SDK. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Dit document biedt een overzicht van het proces voor het maken van een nieuwe bron, inclusief stappen voor het schrijven en verzenden van een nieuwe verbindingsspecificatie met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

De [!DNL Flow Service] API verstrekt verscheidene eindpunten die u toestaan om de verbinding en stroomspecificaties voor een nieuwe bron programmatically te beheren die u door Bronnen SDK integreert.

## Een nieuwe verbindingsspecificatie maken

De eerste stap in het vormen van een nieuwe bron is een nieuwe verbindingsspecificatie tot stand te brengen.

Verbindingsspecificaties retourneren de verbindingseigenschappen van een bron. Zij omvatten authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen en een vaste identiteitskaart van de verbindingsspecificatie die aan een bepaalde bron wordt toegewezen. De specificaties van de verbinding zijn huurder en organisatie IMS agnostic. Een typische verbindingsspecificatie bevat basisinformatie over een bepaalde bron, evenals drie verschillende secties: `authSpec`, `sourceSpec`, en `exploreSpec`.

Voor gedetailleerde instructies raadpleegt u de handleiding op [een nieuwe verbindingsspecificatie maken](./create.md). Voor informatie over de eigenschappen en waarden die voor een verbindingsspecificatie worden gebruikt, met inbegrip van details bij het vormen van authentificatie, bron, en onderzoek specificaties, zie [document met configuratieopties](../config/config.md).

## Stroomspecificaties bijwerken

Als u een verbindingsspecificatie hebt gemaakt, moet u de opdracht `RestStorageToAEP` de stroomspecificatie om uw bron toe te laten om een gegevensstroom tot stand te brengen.

De specificaties van de stroom bevatten informatie die een stroom bepaalt, met inbegrip van bron en doel verbindings IDs die het steunt, transformatiespecificaties die nodig zijn om op de gegevens worden toegepast, en het plannen van parameters die worden vereist om een stroom te produceren.

Voor gedetailleerde instructies raadpleegt u de handleiding op [bijwerken, stroomspecificaties](./update-flow-specs.md).

## De verbindingsspecificatie bijwerken

U kunt uw verbindingsspecificatie bijwerken door een PUT aan te vragen bij de [!DNL Flow Service] API. Zie de handleiding op [bijwerken, verbindingsspecificaties](./update-connection-specs.md) voor meer informatie .

## Uw bron verzenden

Als u uw bron voor integratie naar het Experience Platform wilt verzenden, moet u eerst het volledige [!DNL Flow Service] API-workflow voor bronnen om te controleren of uw bron goed werkt. Als de bron goed wordt uitgevoerd, kun je doorgaan en contact opnemen met je Adobe-vertegenwoordiger voor verificatie en promotie. Zie de handleiding op [bron testen en verzenden](./submit.md) voor meer informatie

## Volgende stappen

Als u het gereedschap [!DNL Flow Service] API en creeer een nieuwe bron door Bronnen SDK, lees [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.