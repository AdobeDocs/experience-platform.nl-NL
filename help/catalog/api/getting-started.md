---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;Catalogus
solution: Experience Platform
title: API-handleiding voor Catalogusservice
topic: developer guide
description: Met de API voor catalogusservice kunnen ontwikkelaars metagegevens voor gegevenssets beheren in Adobe Experience Platform. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# [!DNL Catalog Service] API-handleiding

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. [!DNL Catalog] fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden  [!DNL Experience Platform], zonder dat u toegang hoeft te krijgen tot de gegevens zelf. Zie [[!DNL Catalog] overzicht](../home.md) voor meer informatie.

Deze ontwikkelaarsgids verstrekt stappen helpen u beginnen gebruikend [!DNL Catalog] API. De gids verstrekt dan steekproefAPI vraag voor het uitvoeren van zeer belangrijke verrichtingen gebruikend [!DNL Catalog].

## Vereisten

[!DNL Catalog] controleert meta-gegevens voor verscheidene soorten middelen en verrichtingen binnen  [!DNL Experience Platform]. Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het creëren van en het beheren van deze middelen:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.
* [Inname](../../ingestion/batch-ingestion/overview.md) in batch: Hoe  [!DNL Experience Platform] neemt en slaat gegevens van gegevensdossiers, zoals CSV en Parquet op.
* [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe  [!DNL Experience Platform] neemt en slaat gegevens van cliënt-en server-zijapparaten in real time op.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan hand om met succes vraag aan [!DNL Catalog Service] API te maken.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Aanbevolen procedures voor API-aanroepen [!DNL Catalog]

Wanneer het uitvoeren van GET- verzoeken aan [!DNL Catalog] API, is de beste praktijk om vraagparameters in uw verzoeken te omvatten om slechts de voorwerpen en de eigenschappen terug te keren die u nodig hebt. Door ongefilterde verzoeken kunnen antwoordladingen groter zijn dan 3 GB, wat de algehele prestaties kan vertragen.

U kunt specifieke voorwerpen bekijken door hun identiteitskaart in de verzoekweg te omvatten of vraagparameters zoals `properties` en `limit` te gebruiken om reacties te filtreren. Filters kunnen als kopballen en als vraagparameters worden overgegaan, met die overgegaan als vraagparameters die belangrijkheid nemen. Zie het document over [het filtreren gegevens van de Catalogus](filter-data.md) voor meer informatie.

Aangezien sommige vragen een zware lading op API kunnen zetten, zijn de globale grenzen uitgevoerd op [!DNL Catalog] vragen om beste praktijken verder te steunen.

## Volgende stappen

In dit document wordt de vereiste kennis behandeld die nodig is om aanroepen te kunnen uitvoeren naar de [!DNL Catalog] API. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen.

De meeste voorbeelden in deze handleiding gebruiken het `/dataSets` eindpunt, maar de principes kunnen op andere eindpunten binnen [!DNL Catalog] (zoals `/batches` en `/accounts`) worden toegepast. Zie [Referentie van de Dienst API van de Catalogus ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) voor een volledige lijst van alle vraag en verrichtingen beschikbaar voor elk eindpunt.

Voor een geleidelijke werkschema dat aantoont hoe [!DNL Catalog] API met gegevensopname geïmpliceerd is, zie de zelfstudie op [het creëren van een dataset](../datasets/create.md).
