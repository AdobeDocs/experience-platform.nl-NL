---
title: Prestatieinstructies voor Edge Network Server API
description: Leer hoe u de server-API kunt gebruiken binnen optimale prestatiegaranties.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---


# Prestatieinstructies voor Edge Network Server API

## Overzicht {#overview}

Met prestatiehandleidingen worden gebruiksgrenzen gedefinieerd voor de serverAPI-gebruiksgevallen. Als u de prestatiegaranties die in dit artikel worden beschreven, overschrijdt, kunnen de prestaties achteruitgaan.

Adobe is niet verantwoordelijk voor prestatievermindering die wordt veroorzaakt door overschrijding van de gebruikslimieten. Klanten die de prestatiegaranties consequent overschrijden, kunnen om extra verwerkingscapaciteit vragen om prestatievermindering te voorkomen.

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

Alle prestatieinstructies die in deze pagina worden beschreven, zijn van toepassing op IMS-organisatieniveau. Voor gebruikers met meerdere IMS-organisaties geconfigureerd, is elke organisatie afzonderlijk onderworpen aan de onderstaande prestatieinstructies. Zie de [ verklarende woordenlijst van Experience Platform ](../landing/glossary.md) voor meer details over [!DNL IMS Organizations].

## Definities

* **Beschikbaarheid** wordt berekend voor elk vijf-minieme interval als percentage van verzoeken die door Experience Platform Edge Network worden verwerkt die niet met fouten ontbreken en slechts op provisioned Edge Network APIs betrekking hebben. Als een huurder geen verzoeken in een bepaald vijf-minieme interval maakte, wordt dat interval beschouwd als beschikbaar 100%.
* **maandelijks uptime percentage** voor een bepaald gebied wordt berekend als gemiddelde van de beschikbaarheid voor alle vijf-minieme intervallen in een maand.
* Een **stroomopwaarts** is de dienst achter Edge Network, die voor een specifieke gegevensstroom, zoals de Server van Adobe door:sturen, de Segmentatie van de Rand van Adobe, of Adobe Target wordt toegelaten.
* A **verzoekeenheid** beantwoordt aan een fragment 8 KB van een verzoek en één upstream die voor een gegevensstroom wordt gevormd.
* A **verzoek** is één enkel bericht dat door een klant-bezeten toepassing aan [!DNL Server API] wordt verzonden. Een aanvraag kan een of meer aanvraageenheden bevatten.
* Een **fout** is om het even welk verzoek dat wegens een interne de dienstfout van Edge Network [ ](error-handling.md) ontbreekt.

## Servicelimieten

Alle gegevensstromen dwingen bepaalde gebruiksgrenzen af, die hoofdzakelijk controleren hoeveel gebeurtenissen gelijktijdig kunnen worden verzonden, hun grootte, en het aantal upstream diensten die die verzoeken worden verpletterd aan.

### Aanvraageenheden

Alle grenzen worden toegepast en genormaliseerd over a **verzoekeenheid (RU)**, die als fragment van a **8 KB** wordt bepaald van een verzoek dat naar één upstream dienst gaat die in een datastream wordt gevormd.

#### Voorbeelden

| Upstreams geconfigureerd per datastream | Gemiddelde aanvraaggrootte | Aanvraageenheden |
| --- | --- | --- |
| 1 (Adobe Experience Platform) | 8 kB (1 fragment) | 1 |
| 2 (Adobe Experience Platform, Adobe Target) | 8 kB (1 fragment) | 2 |
| 2 (Adobe Experience Platform, Adobe Target) | 16 kB (2 fragmenten) | 4 |
| 2 (Adobe Experience Platform, Adobe Target) | 64 kB (8 fragmenten) | 16 |

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

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platform Services-instructies, informatie over end-to-end latentie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [ de diagrammen van de de latentie van begin tot eind ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) voor diverse diensten van Experience Platform.
* [ Real-Time Customer Data Platform (B2C Uitgave - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2P - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2B - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
