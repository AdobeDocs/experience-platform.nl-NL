---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;Catalogus
solution: Experience Platform
title: API-handleiding voor Catalogusservice
description: Met de API voor catalogusservice kunnen ontwikkelaars metagegevens voor gegevenssets beheren in Adobe Experience Platform. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# [!DNL Catalog Service] API-handleiding

[!DNL Catalog Service] is het recordsysteem voor de gegevenslocatie en -lijn in Adobe Experience Platform. [!DNL Catalog] fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden in [!DNL Experience Platform] , zonder dat u toegang hoeft te krijgen tot de gegevens zelf. Zie het [[!DNL Catalog]  overzicht ](../home.md) voor meer informatie.

Deze handleiding voor ontwikkelaars bevat stappen waarmee u de API van [!DNL Catalog] kunt gaan gebruiken. De handleiding bevat vervolgens voorbeeld-API-aanroepen voor het uitvoeren van toetsbewerkingen met [!DNL Catalog] .

## Vereisten

[!DNL Catalog] houdt metagegevens bij voor verschillende soorten bronnen en bewerkingen binnen [!DNL Experience Platform] . Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Experience Platform] -services die betrokken zijn bij het maken en beheren van deze bronnen:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.
* [ Inname van de Partij ](../../ingestion/batch-ingestion/overview.md): Hoe [!DNL Experience Platform] gegevens van gegevensdossiers, zoals CSV en Parquet opneemt en opslaat.
* [ Streaming opname ](../../ingestion/streaming-ingestion/overview.md): Hoe [!DNL Experience Platform] gegevens van cliënt en server-zijapparaten in echt - tijd opneemt en opslaat.

De volgende secties bevatten aanvullende informatie die u moet weten of die u zelf moet hebben om aanroepen naar de [!DNL Catalog Service] API te kunnen uitvoeren.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Aanbevolen procedures voor API-aanroepen van [!DNL Catalog]

Wanneer u GET-aanvragen naar de [!DNL Catalog] API uitvoert, kunt u het beste queryparameters opnemen in uw aanvragen om alleen de objecten en eigenschappen te retourneren die u nodig hebt. Door ongefilterde verzoeken kunnen antwoordladingen groter zijn dan 3 GB, wat de algehele prestaties kan vertragen.

U kunt specifieke objecten weergeven door hun id op te nemen in het aanvraagpad of met queryparameters zoals `properties` en `limit` om reacties te filteren. Filters kunnen als kopballen en als vraagparameters worden overgegaan, met die overgegaan als vraagparameters die belangrijkheid nemen. Zie het document over [ het filtreren gegevens van de Catalogus ](filter-data.md) voor meer informatie.

Aangezien sommige query&#39;s een zware belasting voor de API kunnen betekenen, zijn algemene limieten geïmplementeerd voor [!DNL Catalog] query&#39;s voor verdere ondersteuning van best practices.

## Volgende stappen

Dit document bevatte de vereiste kennis die nodig was om aanroepen uit te voeren naar de [!DNL Catalog] API. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen.

De meeste voorbeelden in deze handleiding gebruiken het eindpunt `/dataSets` , maar de principes kunnen worden toegepast op andere eindpunten binnen [!DNL Catalog] (zoals `/batches` ). Zie de [ Verwijzing van de Dienst API van de Catalogus ](https://www.adobe.io/experience-platform-apis/references/catalog/) voor een volledige lijst van alle vraag en verrichtingen beschikbaar voor elk eindpunt.

Voor een geleidelijke werkschema dat aantoont hoe [!DNL Catalog] API met gegevensopname geïmpliceerd is, zie het leerprogramma op [ het creëren van een dataset ](../datasets/create.md).
