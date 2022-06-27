---
title: Prestatiehandleidingen voor Edge Network Server API
description: Leer hoe u de server-API kunt gebruiken binnen optimale prestatievereisten.
keywords: gegevensverzameling;verzameling;edge network;api;sla;slt;service levels
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Prestatiehandleidingen voor Edge Network Server API

## Overzicht {#overview}

Met prestatiehandleidingen worden gebruiksgrenzen gedefinieerd voor de serverAPI-gebruiksgevallen. Als u de prestatiegaranties die in dit artikel worden beschreven, overschrijdt, kunnen de prestaties achteruitgaan.

Adobe is niet verantwoordelijk voor prestatievermindering die wordt veroorzaakt door te hoge gebruikslimieten. Klanten die de prestatiegaranties consequent overschrijden, kunnen om extra verwerkingscapaciteit vragen om prestatievermindering te voorkomen.

## Definities

* **Beschikbaarheid** wordt berekend voor elk vijf-minieme interval als percentage van verzoeken die door het Netwerk van de Rand van het Experience Platform worden verwerkt die niet met fouten ontbreken en slechts op de provisioned het Netwerk APIs van de Rand betrekking hebben. Als een huurder geen verzoeken in een bepaald vijf-minieme interval maakte, wordt dat interval beschouwd als beschikbaar 100%.
* **Maandelijks uptime percentage** voor een bepaald gebied wordt berekend als het gemiddelde van de beschikbaarheid voor alle intervallen van vijf minuten in een maand.
* An **upstream** is de dienst achter het Netwerk van de Rand, dat voor een specifieke gegevensstroom, zoals de Zijde Door:sturen van de Server van Adobe, de Segmentatie van Adobe Edge, of Adobe Target wordt toegelaten.
* A **aanvraageenheid** komt overeen met een fragment van 8 kB van een verzoek en één upstream geconfigureerd voor een gegevensstroom.
* A **verzoek** is één bericht dat door een toepassing in eigendom van een klant naar de [!DNL Server API]. Een aanvraag kan een of meer aanvraageenheden bevatten.
* An **fout** is om het even welke verzoek die wegens een Netwerk van de Rand ontbreekt [interne servicefout](error-handling.md).

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
