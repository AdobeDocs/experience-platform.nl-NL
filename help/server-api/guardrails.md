---
title: Prestatieinstructies voor Edge Network Server API
description: Leer hoe u de server-API kunt gebruiken binnen optimale prestatiegaranties.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---


# Prestatieinstructies voor Edge Network Server API

## Overzicht {#overview}

Met prestatiehandleidingen worden gebruiksgrenzen gedefinieerd voor de serverAPI-gebruiksgevallen. Als u de prestatiegaranties die in dit artikel worden beschreven, overschrijdt, kunnen de prestaties achteruitgaan.

Adobe is niet verantwoordelijk voor prestatievermindering die wordt veroorzaakt door te hoge gebruikslimieten. Klanten die de prestatiegaranties consequent overschrijden, kunnen om extra verwerkingscapaciteit vragen om prestatievermindering te voorkomen.

>[!IMPORTANT]
>
>Controleer uw licentierechten in uw verkooporder en de bijbehorende rechten [Productbeschrijving](https://helpx.adobe.com/legal/product-descriptions.html) op de werkelijke gebruikslimieten naast deze pagina met instructies.

## Definities

* **Beschikbaarheid** wordt berekend voor elk vijf-minieme interval als percentage van verzoeken die door de Edge Network van het Experience Platform worden verwerkt die niet met fouten ontbreken en slechts op provisioned Edge Network APIs betrekking hebben. Als een huurder geen verzoeken in een bepaald vijf-minieme interval maakte, wordt dat interval beschouwd als beschikbaar 100%.
* **Maandelijks uptime percentage** voor een bepaald gebied wordt berekend als het gemiddelde van de beschikbaarheid voor alle intervallen van vijf minuten in een maand.
* An **upstream** is de dienst achter de Edge Network, die voor een specifieke gegevensstroom, zoals de Zijde Door:sturen van de Server van de Adobe, de Segmentatie van Adobe Edge, of Adobe Target wordt toegelaten.
* A **aanvraageenheid** komt overeen met een fragment van 8 kB van een verzoek en één upstream geconfigureerd voor een gegevensstroom.
* A **verzoek** is één bericht dat door een toepassing in eigendom van een klant naar de [!DNL Server API]. Een aanvraag kan een of meer aanvraageenheden bevatten.
* An **fout** is om het even welk verzoek dat wegens een Edge Network ontbreekt [interne servicefout](error-handling.md).

## Servicelimieten

Alle gegevensstromen dwingen bepaalde gebruiksgrenzen af, die hoofdzakelijk controleren hoeveel gebeurtenissen gelijktijdig kunnen worden verzonden, hun grootte, en het aantal upstream diensten die die verzoeken worden verpletterd aan.

### Aanvraageenheden

Alle limieten worden toegepast en genormaliseerd over een **aanvraageenheid (RU)**, gedefinieerd als een **8 kB-fragment** van een verzoek die naar één upstream dienst gaat die in een datastream wordt gevormd.

#### Voorbeelden

| Upstreams geconfigureerd per datastream | Gemiddelde aanvraaggrootte | Aanvraageenheden |
| --- | --- | --- |
| 1 (Adobe Platform) | 8 kB (1 fragment) | 1 |
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

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platforms services guardrails, over end-to-end latentie-informatie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [Diagrammen met latentie van begin tot eind](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) voor verschillende diensten van de Experience Platform.
* [Real-time Customer Data Platform (B2C Edition - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
