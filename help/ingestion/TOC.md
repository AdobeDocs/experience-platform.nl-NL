---
audience: user
user-guide-title: Hulp bij Adobe Experience Platform-gegevensopname
breadcrumb-title: Gids voor gegevensopname
user-guide-description: Breng uw gegevens naar Experience Platform via batch- of streamingopname.
feature: Data Ingestion
role: Developer
source-git-commit: e828485ad5b0904c9dc66b43d1cdb3c4707885b1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 17%

---


# Adobe Experience Platform-gegevensinscriptie {#ingestion}

- [Overzicht van gegevensinname](home.md)
- Streaming opname {#streaming}
   - [Overzicht](streaming-ingestion/overview.md)
   - [Kafka-connector](streaming-ingestion/kafka.md)
   - [Problemen oplossen](streaming-ingestion/troubleshooting.md)
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
   - [Meldingen voor gegevensinvoer](quality/subscribe-events.md)
- [Guardrails voor gegevensinvoer](guardrails.md)
- [Bronaansluitingen](source-connectors.md)
- [Referentie voor API voor batchverwerking](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Referentie voor API voor streaming](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Opmerkingen bij de release van Platform](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)
