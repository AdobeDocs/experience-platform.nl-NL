---
description: De op dossier-gebaseerde bestemmings het testen API is een inzameling van eindpunten die u kunt gebruiken om de configuratie van uw op dossier-gebaseerde bestemmingen te bevestigen die door de Destination SDK worden gebouwd.
title: API voor doeltesten op basis van bestanden
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# API voor doeltesten op basis van bestanden

## Overzicht {#overview}

De op een bestand gebaseerde API voor het testen van doelen is een reeks eindpunten die u kunt gebruiken om de configuratie van uw op een bestand gebaseerde doelen te valideren die via de Destination SDK zijn gemaakt.

Wij adviseren gebruikend deze hulpmiddelen om uw configuratie vóór te bevestigen [indienen](submit-destination.md) uw doel voor revisie naar Adobe.

Voor de beste testresultaten raden we u aan deze API te gebruiken op basis van het onderstaande stroomdiagram.

![Diagram met de aanbevolen teststroom voor de bestemming](assets/file-based-testing-flow.png)

Zie de secties hieronder voor een kort overzicht van wat elk eindpunt kan doen.

## Eindpunt van voorbeeldgeneratie {#sample-generation-endpoint}

Dit eindpunt helpt u steekproefprofielen produceren die op uw bestaand bronschema worden gebaseerd.

Voorbeeldprofielen zijn bedoeld om u te helpen de JSON-structuur van een profiel te begrijpen. Bovendien geven ze u een backbone die u kunt aanpassen met uw eigen profielgegevens voor verdere doeltests.

Zie de [speciale documentatie](file-based-sample-profile-generation-api.md) voor meer informatie over het genereren van voorbeeldprofielen.

## Testeindpunt voor doelconfiguratie {#destination-configuration-testing-endpoint}

Dit eindpunt helpt u testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en verifieert de integriteit van gegevensstromen aan uw gevormde bestemming.

U kunt verzoeken aan het testende eindpunt met of zonder het toevoegen van [voorbeeldprofielen](file-based-sample-profile-generation-api.md) aan de vraag. Als u geen profielen verzendt op de aanvraag, genereert de API automatisch een voorbeeldprofiel en voegt deze toe aan de aanvraag.

Zie de [speciale documentatie](file-based-destination-testing-api.md) om te leren hoe te om uw bestemmingsconfiguratie met steekproefprofielen te testen.

## Het eindpunt van de activeringsresultaten {#activation-results}

Dit eindpunt helpt u de volledige details van uw op dossier-gebaseerde bestemmingstestresultaten bekijken.

Dit API eindpunt keert het zelfde resultaat terug zoals u zou verkrijgen wanneer het gebruiken van [Flow Service-API](../api/update-destination-dataflows.md) om de gegevensstromen te controleren.

Zie de [speciale documentatie](file-based-destination-results-api.md) voor meer informatie over gedetailleerde activeringsresultaten.

## Rendereindpunt van klantvelden {#customer-fields-rendering-endpoint}

Dit eindpunt helpt u visualiseren hoe templatized [klantgegevensvelden](file-based-destination-configuration.md#customer-data-fields) bepaald in uw bestemmingsconfiguratie zou als kijken.

Het eindpunt produceert willekeurige waarden voor uw gebieden van klantengegevens, en keert hen in de reactie terug. Hierdoor kunt u de semantische structuur van gegevensvelden van klanten, zoals emmernamen of mappaden, valideren.

Zie de [speciale documentatie](file-based-render-template-api.md) voor meer informatie over gedetailleerde activeringsresultaten.