---
keywords: Experience Platform;problemen oplossen;instructies;richtlijnen;
title: Guardrails voor gegevensinname
description: Dit document biedt richtlijnen voor het opnemen van gegevens in Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 008537dffff4cc428de9070964446f4e7ebf039f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Guardrails voor gegevensinname

De begeleiding is drempels die begeleiding voor gegevens en systeemgebruik, prestatiesoptimalisering, en vermijding van fouten of onverwachte resultaten in Adobe Experience Platform verstrekken. De begeleiding kan naar uw gebruik of gebruik van gegevens en verwerking met betrekking tot uw vergunningsrechten verwijzen.

Dit document bevat richtlijnen voor het opnemen van gegevens in Adobe Experience Platform.

## Guardrails voor batchgewijs innemen

In de volgende tabel worden de hulplijnen weergegeven die u moet gebruiken bij het gebruik van de [batch-invoer-API](./batch-ingestion/overview.md) of bronnen:

| Type opname | Richtsnoeren | Notities |
| --- | --- | --- |
| Inname van gegevens in een meer met behulp van de batch-opname-API | <ul><li>Met de batch-opname-API kunt u maximaal 20 GB aan gegevens per uur opnemen in het datumpomeer.</li><li>Het maximumaantal bestanden per batch is 1500.</li><li>De maximale batchgrootte is 100 GB.</li><li>Het maximumaantal eigenschappen of velden per rij is 10000.</li><li>Het maximumaantal batches per minuut per gebruiker is 138.</li></ul> |
| Inname van gegevenslagen met behulp van batchbronnen | <ul><li>U kunt maximaal 200 GB gegevens per uur aan datumpeer opnemen gebruikend batch-ingestigenbronnen zoals [!DNL Azure Blob], [!DNL Amazon S3], en [!DNL SFTP].</li><li>Een batch moet tussen 256 MB en 100 GB groot zijn.</li><li>Het maximumaantal bestanden per batch is 1500.</li></ul> | Zie de [overzicht van bronnen](../sources/home.md) voor een catalogus met bronnen die u kunt gebruiken voor gegevensinvoer. |
| Inname in batch naar profiel | <ul><li>De maximale grootte van een recordklasse is 100 kB (zacht).</li><li>De maximale grootte van een klasse ExperienceEvent is 10 KB (soft).</li><li>De maximale grootte van één record is 1 MB.</li></ul> |
| Aantal per dag ingenomen Profile- of ExperienceEvent-batches | **Het maximumaantal per dag ingenomen Profile of ExperienceEvent-batches is 90.** Dit houdt in dat het gecombineerde totaal van de elke dag ingeslikte Profile en ExperienceEvent batches niet meer dan 90 mag bedragen. Door extra batches in te voeren worden de systeemprestaties beïnvloed. | Dit is een zachte limiet. Het is mogelijk om verder te gaan dan een zachte limiet, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties. |

## Guardrails voor streaming opname

Lees de [overzicht van het opnemen van streaming](./streaming-ingestion/overview.md) voor meer informatie over trails voor streaming opname.

## Guardrails voor streamingbronnen

In de volgende tabel worden de instructies beschreven waarmee u rekening moet houden bij het gebruik van de streamingbronnen:

| Type opname | Richtsnoeren | Notities |
| --- | --- | --- |
| Streaming bronnen | <ul><li>De maximale recordgrootte is 1 MB, waarbij de aanbevolen grootte 10 kB is.</li><li>Streaming bronnen ondersteunen tussen 4000 en 5000 aanvragen per seconde wanneer een nieuwe bronverbinding wordt gemaakt. **Opmerking**: Het kan tot 30 minuten duren voor streaming gegevens volledig zijn verwerkt tot data Lake.</li><li>U kunt tussen 4000 en 5000 verzoeken per seconde aan gegevens verwerken meer. **Opmerking**: Het kan tot 30 minuten duren voor streaming gegevens volledig zijn verwerkt tot data Lake.</li></ul> | Streaming bronnen zoals [!DNL Kafka], [!DNL Azure Event Hubs], en [!DNL Amazon Kinesis] niet de [!DNL Data Collection Core Service] (DCCS) route en kan verschillende productiegrenzen hebben. Zie de [overzicht van bronnen](../sources/home.md) voor een catalogus met bronnen die u kunt gebruiken voor gegevensinvoer. |

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over gegevens en verwerkingsinstructies in Experience Platform:

* [Gardrails voor gegevens in realtime klantprofiel](../profile/guardrails.md)
* [Guardrails voor identiteitsservicegegevens](../identity-service/guardrails.md)
