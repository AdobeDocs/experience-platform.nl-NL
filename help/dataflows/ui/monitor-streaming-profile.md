---
title: Streaming profielopname controleren
description: Leer hoe u het dashboard voor bewaking kunt gebruiken om de opname van streaming profielen te controleren
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# Streaming profielopname controleren

Met het dashboard voor bewaking in de gebruikersinterface van Adobe Experience Platform kunt u in realtime controle uitvoeren op de innamesnelheden van streaming profielen in uw organisatie. Gebruik deze functie voor een betere transparantie van de doorvoer, de latentie en de gegevenskwaliteit rond streaming gegevens. Bovendien kunt u deze functie gebruiken voor proactieve waarschuwingen en het opvragen van activeerbare inzichten om potentiële capaciteitsschendingen en kwesties van gegevensopname te identificeren.

Lees de volgende handleiding om te leren hoe u het dashboard voor bewaking kunt gebruiken om de frequenties en metriek van streamingtaken voor het opnemen van profielen in uw organisatie te controleren.

## Het dashboard voor het opnemen van streaming profielen

U kunt drie verschillende metrische categorieën in het controledashboard gebruiken voor het stromen van profielopname: [!UICONTROL Throughput], [!UICONTROL Ingestion], en [!UICONTROL Latency].

* **Productie**: Selecteer **[!UICONTROL Throughput]** om informatie over de hoeveelheid gegevens te bekijken die Experience Platform gegeven een gevormde periode verwerkt. Verwijs naar deze metrisch om de efficiency en de capaciteit van uw systeem te evalueren.
   * **Capaciteit**: De maximumhoeveelheid gegevens die uw zandbak onder bepaalde voorwaarden kan verwerken.
   * **productie van het Verzoek**: Het tarief waarbij de gebeurtenissen door het innamesysteem worden ontvangen, dat in gebeurtenissen per seconde wordt gemeten.
   * **Verwerkingsproductie**: Het tarief waarbij het systeem met succes binnenkomt en inkomende gebeurtenislading verwerkt, die in gebeurtenissen per seconde wordt gemeten.
* **Ingestie**: Selecteer [!UICONTROL Ingestion] om informatie over de innametaken in uw zandbak te bekijken. Deze innametaken worden in drie verschillende meeteenheden gemeten:
   * **Beelden die** worden gecreeerd: De totale hoeveelheid verslagen binnen een bepaalde tijdspanne worden gecreeerd. Deze metrische waarde vertegenwoordigt succesvolle processen voor gegevensinvoer in uw sandbox.
   * **Ontbroken verslagen**: Het totale aantal verslagen die niet wegens fouten werden opgenomen.
   * **gelaten vallen verslagen**: Het totale aantal verslagen die wegens schending van capaciteitsgrenzen werden gelaten vallen.
* **Latentie**: Selecteer [!UICONTROL Latency] om informatie over de hoeveelheid tijd te bekijken het Experience Platform neemt om op een verzoek te antwoorden of een verrichting binnen een bepaalde tijdspanne te voltooien.

## Metrische gegevens voor het streamen van profielopname controleren {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Streaming profielopname controleren"
>abstract="Het controledashboard voor het stromen profielen toont informatie over productie, innamesnelheden, en latentie. Met dit dashboard kunt u de gegevens voor gegevensverwerking weergeven, begrijpen en analyseren. van uw streamingprofielen naar Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Productie aanvragen"
>abstract="Deze metrische waarde vertegenwoordigt het aantal gebeurtenissen dat per seconde het innamesysteem binnenkomt."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Verwerkingsdoorvoer"
>abstract="Deze metrische waarde vertegenwoordigt het aantal gebeurtenissen dat met succes door het systeem elke seconde wordt opgenomen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95-inlaatlatentie"
>abstract="Deze metrische waarde meet de latentie van het 95e percentiel vanaf het moment dat een gebeurtenis in Experience Platform aankomt tot wanneer de gebeurtenis met succes in de opslag van het Profiel wordt opgenomen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Maximale doorvoer"
>abstract="Deze metrische waarde vertegenwoordigt het maximumaantal binnenkomende verzoeken per seconde die het stromen profielopname ingaan."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Opgenomen records"
>abstract="Deze metrische waarde vertegenwoordigt het totale aantal verslagen die aan de opslag van het Profiel binnen een gevormd tijdvenster worden opgenomen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Records mislukt"
>abstract="Deze metrische waarde vertegenwoordigt het totale aantal verslagen die geen opname in de opslag van het Profiel, binnen een gevormd tijdvenster, wegens fouten ontbrak."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Records overgeslagen"
>abstract="Deze metrisch vertegenwoordigt het totale aantal verslagen die binnen een gevormd tijdvenster, wegens configuratie of capaciteitsschendingen werden gelaten vallen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Foutgegevens"
>abstract="Deze metrische waarde vertegenwoordigt het aantal mislukte gebeurtenissen als gevolg van fouten."
>text="Learn more in documentation"

| Metrisch | Beschrijving | Afmetingen | Frequentie van meting |
| --- | --- | --- | --- |
| Productie aanvragen | Deze metrische waarde vertegenwoordigt het aantal gebeurtenissen dat per seconde het innamesysteem binnenkomt. | Sandbox/DataFlow | Controle in real time met gegevens verfrist zich elke 60 seconden. |
| Verwerkingsdoorvoer | Deze metrische waarde vertegenwoordigt het aantal gebeurtenissen dat met succes door het systeem elke seconde wordt opgenomen. | Sandbox/DataFlow | Controle in real time met gegevens verfrist zich elke 60 seconden. |
| P95-inlaatlatentie | Deze metrische waarde meet de latentie van het 95e percentiel vanaf het moment dat een gebeurtenis in Experience Platform aankomt tot wanneer de gebeurtenis met succes in de opslag van het Profiel wordt opgenomen. | Sandbox/DataFlow | Controle in real time met gegevens verfrist zich elke 60 seconden. |
| Maximale doorvoer |
| Opgenomen records | Deze metrische waarde vertegenwoordigt het totale aantal verslagen die aan de opslag van het Profiel binnen een gevormd tijdvenster worden opgenomen. | <ul><li>Sandbox/DataFlow</li><li>Dataflow-uitvoering</li></ul> | <ul><li>Sandbox/Dataflow: Real-time controle met gegevens verfrist zich om de 60 seconden.</li><li>Dataflow-run: binnen 15 minuten gegroepeerd.</li></ul> |
| Records mislukt | Deze metrische waarde vertegenwoordigt het totale aantal verslagen die geen opname in de opslag van het Profiel, binnen een gevormd tijdvenster, wegens fouten ontbrak. | <ul><li>Sandbox/DataFlow</li><li>Dataflow-uitvoering</li></ul> | <ul><li>Sandbox/Dataflow: Real-time controle met gegevens verfrist zich om de 60 seconden.</li><li>Dataflow-run: binnen 15 minuten gegroepeerd.</li></ul> |
| Records overgeslagen | Deze metrisch vertegenwoordigt het totale aantal verslagen die binnen een gevormd tijdvenster, wegens configuratie of capaciteitsschendingen werden gelaten vallen. | <ul><li>Sandbox/DataFlow</li><li>Dataflow-uitvoering</li></ul> | <ul><li>Sandbox/Dataflow: Real-time controle met gegevens verfrist zich om de 60 seconden.</li><li>Dataflow-run: binnen 15 minuten gegroepeerd.</li></ul> |
| Foutgegevens | Deze metrische waarde vertegenwoordigt het aantal mislukte gebeurtenissen als gevolg van fouten. | Dataflow-uitvoering | gegroepeerd in een uurvenster. |

{style="table-layout:auto"}