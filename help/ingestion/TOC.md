---
audience: user
user-guide-title: Hulp bij Adobe Experience Platform-gegevensopname
breadcrumb-title: Gids voor gegevensopname
user-guide-description: Breng uw gegevens naar Experience Platform via batch- of streamingopname.
feature: Data Ingestion
role: Developer
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 20%

---


# Adobe Experience Platform-gegevensinscriptie {#ingestion}

- [Overzicht van gegevensinname](home.md)
- Streaming opname {#streaming}
   - [Overzicht](streaming-ingestion/overview.md)
   - [Kafka-connector](streaming-ingestion/kafka.md)
   - [Problemen oplossen](streaming-ingestion/troubleshooting.md)
   - [IP Adres Voegende op lijst van gewenste personen &#x200B;](streaming-ingestion/allowlisting.md)
- Inname in batch{#batch}
   - [Aan de slag met batch-opname-API&#39;s](batch-ingestion/getting-started.md)
   - [API-overzicht](batch-ingestion/overview.md)
   - [API-ontwikkelaarsgids](batch-ingestion/api-overview.md)
   - [Gedeeltelijke batch ingestie](batch-ingestion/partial.md)
   - [Problemen oplossen](batch-ingestion/troubleshooting.md)
- Tutorials {#tutorials}
   - Een CSV-bestand toewijzen aan XDM {#map-csv}
      - [Overzicht](./tutorials/map-csv/overview.md)
      - [Een CSV-bestand toewijzen aan een bestaand schema](./tutorials/map-csv/existing-schema.md)
      - [Een CSV-bestand toewijzen aan de hand van door AI gegenereerde aanbevelingen](./tutorials/map-csv/recommendations.md)
   - [Batchgegevens invoeren met de gebruikersinterface](tutorials/ingest-batch-data.md)
   - [Een geverifieerde streamingverbinding maken](tutorials/create-authenticated-streaming-connection.md)
   - [Een streamingverbinding (API) maken](tutorials/create-streaming-connection.md)
   - [Een streamingverbinding (UI) maken](tutorials/create-streaming-connection-ui.md)
   - [Opnamegegevens streamen](tutorials/streaming-record-data.md)
   - [Streaming tijdreeksgegevens](tutorials/streaming-time-series-data.md)
   - [Meerdere berichten streamen](tutorials/streaming-multiple-messages.md)
- Gegevenskwaliteit en toezicht{#quality}
   - [Overzicht](quality/overview.md)
   - [Gegevens bijhouden](quality/monitor-data-ingestion.md)
   - [Foutendiagnostiek ophalen](quality/error-diagnostics.md)
   - [Ontbroken batches ophalen](quality/retrieve-failed-batches.md)
   - [Validatie van gestreamde invoer](quality/streaming-validation.md)
- [Guardrails voor gegevensinvoer](guardrails.md)
- [Source-connectors](source-connectors.md)
- [&#x200B; Verwijzing van de Opname API van de Partij &#x200B;](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [&#x200B; Streaming Ingestie API verwijzing &#x200B;](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Releaseopmerkingen bij Experience Platform](https://experienceleague.adobe.com/nl/docs/experience-platform/release-notes/latest)
