---
title: Overeenkomsten en doelstellingen op het niveau van de dienstverlening
description: Leer hoe u verificatie voor de Edge Network Server-API configureert
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: gegevensverzameling;verzameling;edge network;api;sla;slt;service levels
hide: true
hidefromtoc: true
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Guardrails

## Overzicht {#overview}

Adobe zal commercieel redelijke inspanningen leveren om de [!DNL Server API] beschikbaar binnen een maandelijks uptime percentage van minstens 99.9% voor elke regio, tijdens om het even welke maandelijkse factureringscyclus.

## Definities

* **Beschikbaarheid** wordt berekend voor elk vijf-minieme interval als percentage van verzoeken die door het Netwerk van de Rand van de Ervaring worden verwerkt Adobe Experience Platform die niet met fouten ontbreken en slechts op de provisioned het Netwerk van Adobe Experience Platform Edge APIs betrekking hebben. Als een huurder geen verzoeken in een bepaald vijf-minieme interval maakte, wordt dat interval beschouwd als beschikbaar 100%.
* **Maandelijks uptime percentage** voor een bepaald gebied wordt berekend als het gemiddelde van de beschikbaarheid voor alle intervallen van vijf minuten in een maand.
* An **upstream** is de dienst achter het Netwerk van Adobe Edge, die voor een specifieke gegevensstroom, zoals de Zijde Door:sturen van de Server van Adobe, Adobe Edge Segmentation, of Adobe Target wordt toegelaten.
* A **verzoek** die naar de server-API worden verzonden, wordt gedefinieerd als een of meer aanvraageenheden.
* A **aanvraageenheid** komt overeen met een fragment van 8 kB van een verzoek en één upstream geconfigureerd voor een gegevensstroom.
* An **fout** is om het even welke verzoek die wegens een Netwerk van Adobe Experience Platform Edge ontbreekt [interne servicefout](error-handling.md).

## Interne doelstellingen

De ingenieursteams van Adobe stellen dicht bij telemetrie in real time, controle, en schaal uit procedures op om de volgende doelstellingen te verzekeren:

* Minder dan 1% van HTTP-aanvragen retourneren `5xx` fouten in de laatste vijf minuten
* Minder dan 1% van de upstreamverbindingen retourneert een fout in de laatste vijf minuten
* Elke huurderscapaciteit wordt binnen 10 minuten verdubbeld vanaf het moment waarop een limiet wordt bereikt.

## Uitsluiting van overeenkomsten op serviceniveau

De hierboven beschreven verbintenis op het niveau van de dienst is niet van toepassing op om het even welke onbeschikbaarheid of prestatieskwesties die door de volgende gebeurtenissen worden veroorzaakt:

* Factoren die buiten onze redelijke controle vallen, zoals internettoegang of aanverwante problemen buiten de infrastructuur van Adobe.
* Elk misbruik van de [!DNL Server API], zoals gedefinieerd door de hieronder aangegeven limieten.

## Servicelimieten

Alle gegevensstromen dwingen bepaalde gebruiksgrenzen af, die hoofdzakelijk controleren hoeveel gebeurtenissen gelijktijdig kunnen worden verzonden, hun grootte, en het aantal upstream diensten die die verzoeken worden verpletterd aan.

### Aanvraageenheden

Alle limieten worden toegepast en genormaliseerd over een **aanvraageenheid (RU)**, gedefinieerd als een **8 kB-fragment** van een verzoek die naar één upstream dienst gaat die in een datastream wordt gevormd.

#### Voorbeelden

| Upstreams geconfigureerd per datastream | Gemiddelde aanvraaggrootte | Aanvraageenheden |
| --- | --- | --- |
| 1 (Adobe-Platform) | 8 kB (1 fragment) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 kB (1 fragment) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 kB (2 fragmenten) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 kB (8 fragmenten) | 16 |

### Limieten voor aanvraageenheden

In de onderstaande tabel staan de standaardgrenswaarden. Neem contact op met uw accountvertegenwoordiger als u hogere aanvragen voor eenheidlimieten nodig hebt.

| Endpoint | Verzoeken om eenheden per seconde |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Maximale grootte HTTP-aanvraag

| Payload-indeling | Maximale grootte voor een aanvraag | Max. 8 kB aanvraagfragmenten |
| --- | --- | --- |
| JSON onbewerkte tekst | 64 kB | 8 |


>[!NOTE]
>
>Afhankelijk van de nuttige lading zelf, zijn de binaire formaten over het algemeen 20-40% compacter, toestaand u om meer gegevens te duwen dan u in duidelijk-tekst JSON zou doen. Neem contact op met uw medewerker van de klantenservice als u een hogere capaciteit voor uw gegevensstreams nodig hebt.

