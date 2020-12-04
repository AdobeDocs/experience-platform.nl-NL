---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Catalog Service
topic: developer guide
description: Deze handleiding voor ontwikkelaars bevat stappen waarmee u de API voor Catalog kunt gaan gebruiken. De handleiding bevat vervolgens voorbeeld-API-aanroepen voor het uitvoeren van toetsbewerkingen met behulp van Catalog.
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# [!DNL Catalog Service] ontwikkelaarsgids

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. [!DNL Catalog] fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden [!DNL Experience Platform], zonder dat u toegang hoeft te krijgen tot de gegevens zelf. Zie het [[!DNL Catalog] overzicht](../home.md) voor meer informatie.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de [!DNL Catalog] API kunt gaan gebruiken. De gids verstrekt dan steekproefAPI vraag voor het uitvoeren van zeer belangrijke verrichtingen gebruikend [!DNL Catalog].

## Vereisten

[!DNL Catalog] controleert meta-gegevens voor verscheidene soorten middelen en verrichtingen binnen [!DNL Experience Platform]. Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het creëren van en het beheren van deze middelen:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.
* [Inname](../../ingestion/batch-ingestion/overview.md)in batch: Hoe [!DNL Experience Platform] neemt en slaat gegevens van gegevensdossiers, zoals CSV en Parquet op.
* [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe [!DNL Experience Platform] neemt en slaat gegevens van cliënt-en server-zijapparaten in real time op.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben om met succes vraag aan [!DNL Catalog Service] API te maken.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Aanbevolen procedures voor [!DNL Catalog] API-aanroepen

Wanneer u GET-aanvragen naar de [!DNL Catalog] API uitvoert, kunt u het beste queryparameters opnemen in uw aanvragen om alleen de objecten en eigenschappen te retourneren die u nodig hebt. Door ongefilterde verzoeken kunnen antwoordladingen groter zijn dan 3 GB, wat de algehele prestaties kan vertragen.

U kunt specifieke objecten weergeven door hun id op te nemen in het aanvraagpad of met queryparameters, zoals `properties` en `limit` voor het filteren van reacties. Filters kunnen als kopballen en als vraagparameters worden overgegaan, met die overgegaan als vraagparameters die belangrijkheid nemen. Zie het document over het [filtreren van de gegevens](filter-data.md) van de Catalogus voor meer informatie.

Aangezien sommige vragen een zware lading op API kunnen zetten, zijn de globale grenzen uitgevoerd op [!DNL Catalog] vragen om beste praktijken verder te steunen.

## Volgende stappen

Dit document bevatte de vereiste kennis die nodig was om oproepen naar de [!DNL Catalog] API uit te voeren. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen.

De meeste voorbeelden in deze handleiding gebruiken het `/dataSets` eindpunt, maar de beginselen kunnen op andere eindpunten binnen [!DNL Catalog] (zoals `/batches` en `/accounts`) worden toegepast. Zie de [dienst API van de Catalogus verwijzing](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) voor een volledige lijst van alle vraag en verrichtingen beschikbaar voor elk eindpunt.

Voor een geleidelijke werkschema dat aantoont hoe [!DNL Catalog] API met gegevensopname geïmpliceerd is, zie het leerprogramma bij het [creëren van een dataset](../datasets/create.md).
