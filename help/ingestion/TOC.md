---
product: experience-platform
audience: user
user-guide-title: Help bij Adobe Experience Platform-gegevensverwerking
breadcrumb-title: Data Ingestion Guide
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: 2a5d6a9462950007d00f321ca9f3a3c457a3243e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Overzicht van gegevensinname](home.md)
- Streaming opname {#streaming}
   - [Overzicht](streaming-ingestion/overview.md)
   - [Kafka-connector](streaming-ingestion/kafka.md)
   - [Problemen oplossen](streaming-ingestion/troubleshooting.md)
- Inname in batch{#batch}
   - [Overzicht](batch-ingestion/overview.md)
   - [Batchopname-API](batch-ingestion/api-overview.md)
   - [Gedeeltelijke batch ingestie](batch-ingestion/partial.md)
   - [Problemen oplossen](batch-ingestion/troubleshooting.md)
- Tutorials {#tutorials}
   - [Een CSV-bestand toewijzen aan XDM](tutorials/map-a-csv-file.md)
   - [Batchgegevens invoeren met de gebruikersinterface](tutorials/ingest-batch-data.md)
   - [Een geverifieerde streamingverbinding maken](tutorials/create-authenticated-streaming-connection.md)
   - [Een streamingverbinding (API) maken](tutorials/create-streaming-connection.md)
   - [Een streamingverbinding (UI) maken](tutorials/create-streaming-connection-ui.md)
   - [Opnamegegevens streamen](tutorials/streaming-record-data.md)
   - [Streaming tijdreeksgegevens](tutorials/streaming-time-series-data.md)
   - [Meerdere berichten streamen](tutorials/streaming-multiple-messages.md)
- Kwaliteit van gegevensinvoer en controle{#quality}
   - [Overzicht](quality/overview.md)
   - [Gegevensstromen bewaken](quality/monitor-data-flows.md)
   - [Foutendiagnostiek ophalen](quality/error-diagnostics.md)
   - [Ontbroken batches ophalen](quality/retrieve-failed-batches.md)
   - [Validatie van gestreamde invoer](quality/streaming-validation.md)
   - [Abonneren op gebeurtenissen voor gegevensinvoer](quality/subscribe-events.md)
- [Bronaansluitingen](source-connectors.md)
- [API-referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Opmerkingen bij de release Platform](https://www.adobe.com/go/platform-release-notes-en)