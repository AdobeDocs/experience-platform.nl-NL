---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Segmentatieservice
topic: developer guide
translation-type: tm+mt
source-git-commit: e25ce403034a94d7024e8c244cb438bd9dfe0c5f
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van Segmentatieservice

Met segmentatie kunt u segmenten samenstellen en een publiek genereren in het Adobe Experience Platform op basis van uw gegevens in het realtime profiel van de klant.

## Aan de slag

Deze handleiding vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het gebruik van Segmentatie.

- [Segmentatie](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om Segmentatie met succes te gebruiken gebruikend API.

### API-voorbeeldaanroepen lezen

De documentatie van de Dienst API van de Segmentatie verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan de eindpunten van het Platform met succes te maken. Het voltooien van de authentificatiezelfstudie verstrekt de waarden voor elk van de vereiste kopballen in de vraag van API van het Platform van de Ervaring, zoals hieronder getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van [sandboxen voor meer informatie over het werken met sandboxen in Experience Platform](../../sandboxes/home.md).

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Segmenttaken

De banen van het segment verwerken eerder vastgestelde segmentdefinities om een publiekssegment te produceren. U kunt het `/segment/jobs` eindpunt gebruiken om een lijst van segmentbanen terug te winnen, een nieuwe segmentbaan tot stand te brengen, details van een specifieke segmentbaan terug te winnen, of een specifieke segmentbaan te schrappen.

Voor meer informatie bij het gebruiken van dit eindpunt, te lezen gelieve de gids [van de](./segment-jobs.md)segmentbaanontwikkelaar.

## Segmentzoekopdracht

Het onderzoek van het segment wordt gebruikt aan onderzoek en index configureerbare gebieden die over diverse gegevensbronnen worden bevat en hen in bijna real time terugkeren. Zie de handleiding voor [zoekprogramma&#39;s voor meer informatie over het werken met segmentzoekopdrachten](segment-search.md)

## Volgende stappen

Beginnen het maken vraag gebruikend de Segmentatie API, selecteer één van sub-gidsen om te leren hoe te om specifieke op segmentatie betrekking hebbende eindpunten te gebruiken. Meer over het werken met segmenten gebruikend het Platform UI, zie de de gebruikersgids [van de](../ui/overview.md)Segmentatie.