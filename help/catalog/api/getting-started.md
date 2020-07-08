---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van Catalog Service

Catalogusservice is het systeem voor het opnemen van gegevens voor de locatie en de verbinding binnen het Adobe Experience Platform. Catalogus fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden binnen het Experience Platform, zonder dat u toegang hoeft te krijgen tot de gegevens zelf. Zie het [Catalogusoverzicht](../home.md) voor meer informatie.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de API voor Catalog kunt gaan gebruiken. De handleiding bevat vervolgens voorbeeld-API-aanroepen voor het uitvoeren van toetsbewerkingen met behulp van Catalog.

## Vereisten

De catalogus volgt meta-gegevens voor verscheidene soorten middelen en verrichtingen binnen Experience Platform. Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van de Experience Platform betrokken bij het creëren van en het beheren van deze middelen:

* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [Inname](../../ingestion/batch-ingestion/overview.md)in batch: Hoe Experience Platform gegevens uit gegevensbestanden, zoals CSV en Parquet, opneemt en opslaat.
* [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe het Experience Platform gegevens van cliënt en server-zijapparaten in real time opneemt en opslaat.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben om met succes vraag aan de Dienst API van de Catalogus te maken.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Aanbevolen procedures voor API-aanroepen van catalogus

Wanneer het uitvoeren van GET verzoeken aan Catalog API, is de beste praktijk om vraagparameters in uw verzoeken te omvatten om slechts de voorwerpen en de eigenschappen terug te keren die u nodig hebt. Door ongefilterde verzoeken kunnen antwoordladingen groter zijn dan 3 GB, wat de algehele prestaties kan vertragen.

U kunt specifieke objecten weergeven door hun id op te nemen in het aanvraagpad of met queryparameters, zoals `properties` en `limit` voor het filteren van reacties. Filters kunnen als kopballen en als vraagparameters worden overgegaan, met die overgegaan als vraagparameters die belangrijkheid nemen. Zie het document over het [filtreren van de gegevens](filter-data.md) van de Catalogus voor meer informatie.

Aangezien sommige vragen een zware lading op API kunnen zetten, zijn de globale grenzen uitgevoerd op de vragen van de Catalogus om beste praktijken verder te steunen.

## Volgende stappen

Dit document bevatte de vereiste kennis die nodig was om oproepen te kunnen uitvoeren naar de API voor catalogi. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen.

De meeste voorbeelden in deze gids gebruiken het `/dataSets` eindpunt, maar de principes kunnen op andere eindpunten binnen Catalogus (zoals `/batches` en `/accounts`) worden toegepast. Zie de [dienst API van de Catalogus verwijzing](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) voor een volledige lijst van alle vraag en verrichtingen beschikbaar voor elk eindpunt.

Voor een geleidelijke werkschema dat aantoont hoe Catalog API met gegevensopname geïmpliceerd is, zie het leerprogramma bij het [creëren van een dataset](../datasets/create.md).
