---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;Catalogus
solution: Experience Platform
title: API-handleiding voor Catalogusservice
topic-legacy: developer guide
description: Met de API voor catalogusservice kunnen ontwikkelaars metagegevens voor gegevenssets beheren in Adobe Experience Platform. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# [!DNL Catalog Service] API-handleiding

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. [!DNL Catalog] fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden binnen [!DNL Experience Platform], zonder toegang tot de gegevens zelf. Zie de [[!DNL Catalog] overzicht](../home.md) voor meer informatie .

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de functie [!DNL Catalog] API. De gids verstrekt dan steekproefAPI vraag om zeer belangrijke verrichtingen uit te voeren gebruikend [!DNL Catalog].

## Vereisten

[!DNL Catalog] controleert meta-gegevens voor verscheidene soorten middelen en verrichtingen binnen [!DNL Experience Platform]. Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Experience Platform] diensten die betrokken zijn bij het creëren en beheren van deze middelen:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.
* [Inname in batch](../../ingestion/batch-ingestion/overview.md): Hoe [!DNL Experience Platform] Hiermee worden gegevens uit gegevensbestanden, zoals CSV en Parquet, ingepakt en opgeslagen.
* [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe [!DNL Experience Platform] Voert gegevens van client- en server-side apparaten in real-time in en slaat deze op.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan met succes vraag aan [!DNL Catalog Service] API.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

## Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Aanbevolen procedures voor [!DNL Catalog] API-aanroepen

Bij het uitvoeren van GET-aanvragen bij de [!DNL Catalog] API, de beste praktijken moeten vraagparameters in uw verzoeken omvatten om slechts de voorwerpen en de eigenschappen terug te keren die u nodig hebt. Door ongefilterde verzoeken kunnen antwoordladingen groter zijn dan 3 GB, wat de algehele prestaties kan vertragen.

U kunt specifieke objecten bekijken door hun id op te nemen in het aanvraagpad of met queryparameters zoals `properties` en `limit` om reacties te filteren. Filters kunnen als kopballen en als vraagparameters worden overgegaan, met die overgegaan als vraagparameters die belangrijkheid nemen. Document weergeven op [catalogusgegevens filteren](filter-data.md) voor meer informatie .

Aangezien sommige query&#39;s een zware belasting voor de API kunnen betekenen, zijn globale limieten geïmplementeerd op [!DNL Catalog] vragen om de beste praktijken verder te ondersteunen.

## Volgende stappen

Dit document bevatte de vereiste kennis die nodig was om oproepen te doen aan de [!DNL Catalog] API. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen.

In de meeste voorbeelden in deze handleiding wordt gebruikgemaakt van de `/dataSets` , maar de beginselen kunnen worden toegepast op andere eindpunten binnen [!DNL Catalog] (zoals `/batches` en `/accounts`). Zie de [Referentie voor Catalog Service API](https://www.adobe.io/experience-platform-apis/references/catalog/) voor een volledige lijst van alle vraag en verrichtingen beschikbaar voor elk eindpunt.

Voor een stapsgewijze workflow die aantoont hoe de [!DNL Catalog] API is betrokken bij gegevensinvoer, raadpleeg de zelfstudie over [een gegevensset maken](../datasets/create.md).
