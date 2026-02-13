---
keywords: Experience Platform;problemen oplossen;instructies;richtlijnen;
title: Guardrails voor gegevensinname
description: Meer informatie over instructies voor gegevensinvoer in Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: b5b975308d28ae82ea4d811652681215bc2cfbdb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Guardrails voor gegevensinname

>[!IMPORTANT]
>
>De begeleiding voor partij en het stromen wordt ingestie over het algemeen berekend op het organisatieniveau en niet op het zandbakniveau. Dit betekent dat uw gegevensgebruik per sandbox is gebonden aan de totale gebruiksrechten voor licenties die overeenkomen met uw volledige organisatie. Daarnaast is het gebruik van gegevens in ontwikkelingssandboxen beperkt tot 10% van uw totale profielen. Voor meer informatie over de gebruiksrechten van de vergunning, lees de [ gids van de beste praktijken van het gegevensbeheer ](../landing/license-usage-and-guardrails/data-management-best-practices.md).

De begeleiding is drempels die begeleiding voor gegevens en systeemgebruik, prestatiesoptimalisering, en vermijding van fouten of onverwachte resultaten in Adobe Experience Platform verstrekken. De begeleiding kan naar uw gebruik of gebruik van gegevens en verwerking met betrekking tot uw vergunningsrechten verwijzen.

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

Dit document bevat richtlijnen voor het opnemen van gegevens in Adobe Experience Platform.

## Guardrails voor batchgewijs innemen

De volgende lijst schetst te overwegen gidsen wanneer het gebruiken van [ partij ingestie API ](./batch-ingestion/overview.md) of bronnen:

| Type opname | Richtsnoeren | Notities |
| --- | --- | --- |
| Inname van gegevens in een meer met behulp van de batch-opname-API | <ul><li>Met de batch-opname-API kunt u maximaal 20 GB aan gegevens per uur opnemen in het datumpomeer.</li><li>Het maximumaantal bestanden per batch is 1500.</li><li>De maximale batchgrootte is 100 GB.</li><li>Het maximumaantal eigenschappen of velden per rij is 10000.</li><li>Het maximumaantal batches per minuut per gebruiker is 2000.</li></ul> | |
| Inname van gegevenslagen met behulp van batchbronnen | <ul><li>U kunt maximaal 200 GB aan gegevens per uur invoeren aan datumpeer gebruikend batch-ingestigenbronnen zoals [!DNL Azure Blob], [!DNL Amazon S3], en [!DNL SFTP].</li><li>Een batch moet tussen 256 MB en 100 GB groot zijn. Dit geldt zowel voor ongecomprimeerde als gecomprimeerde gegevens. Wanneer gecomprimeerde gegevens niet in het datumpeer worden gecomprimeerd, zijn deze beperkingen van toepassing.</li><li>Het maximumaantal bestanden per batch is 1500.</li><li>Een bestand of map heeft minimaal 1 byte. U kunt geen bestanden of mappen met 0-byte-grootte invoeren.</li></ul> | Lees het [ overzicht van bronnen ](../sources/home.md) voor een catalogus van bronnen u voor gegevensopname kunt gebruiken. |
| Inname in batch naar profiel | <ul><li>De maximale grootte van een recordklasse is 100 KB (hard).</li><li>De maximale grootte van een klasse ExperienceEvent is 10 KB (hard).</li></ul> | |
| Aantal per dag ingenomen Profile- of ExperienceEvent-batches | **het maximumaantal per dag ingeslikte partijen van het Profiel of van de ExperienceEvent is 90 per zandbak.** Dit betekent dat het gecombineerde totaal van de elke dag ingeslikte profielen Profile en ExperienceEvent niet meer dan 90 mag zijn. Door extra batches in te voeren worden de systeemprestaties beïnvloed. | Dit is een zachte limiet. Het is mogelijk om verder te gaan dan een zachte limiet, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties. Bovendien, is deze guardrail op a **per zandbak** basis, niet per organisatiebasis. |
| Versleutelde gegevensinvoer | De maximale ondersteunde grootte van één gecodeerd bestand is 1 GB. Terwijl u bijvoorbeeld 2 of meer GB&#39;s aan gegevens kunt invoeren in één dataflow-run, kan geen enkel afzonderlijk bestand in de dataflow-run meer dan 1 GB bedragen. | Het inslikken van gecodeerde gegevens kan langer duren dan het innemen van gewone gegevens. Lees de [ gecodeerde gids van de gegevensopname API ](../sources/tutorials/api/encrypt-data.md) voor meer informatie. |
| Batchopname bijwerken | De inname van upsert de partijen kan tot 10x langzamer zijn dan regelmatige partijen, daarom zou u uw upsert partijen onder twee miljoen verslagen **moeten houden om efficiënte runtime te verzekeren en het blokkeren van andere partijen te vermijden die in de zandbak worden verwerkt.** | Hoewel u ongetwijfeld batches met meer dan twee miljoen records kunt innemen, is de tijd van inname aanzienlijk langer vanwege de beperkingen van kleine sandboxen. |

{style="table-layout:auto"}

## Guardrails voor streaming opname

Lees het [ stromen ingeslikt overzicht ](./streaming-ingestion/overview.md) voor informatie over gidsen voor het stromen ingestie.

## Guardrails voor streamingbronnen

In de volgende tabel worden de instructies beschreven waarmee u rekening moet houden bij het gebruik van de streamingbronnen:

| Type opname | Richtsnoeren | Notities |
| --- | --- | --- |
| Streaming bronnen | <ul><li>De maximale recordgrootte is 1 MB, waarbij de aanbevolen grootte 10 kB is.</li><li>Streaming bronnen ondersteunen tussen de 4000 en 5000 aanvragen per seconde bij het opnemen naar het data-meer. Dit geldt voor zowel nieuw gemaakte bronverbindingen als bestaande bronverbindingen. **Nota**: Het kan tot 60 minuten voor het stromen gegevens vergen om volledig te worden verwerkt tot gegevens meer.</li><li>Streaming bronnen ondersteunen maximaal 1500 aanvragen per seconde bij het opnemen van gegevens naar profiel of streaming segmentatie.</li></ul> | Streaming bronnen zoals [!DNL Kafka] , [!DNL Azure Event Hubs] en [!DNL Amazon Kinesis] maken geen gebruik van de [!DNL Data Collection Core Service] (DCCS)-route en kunnen verschillende doorvoergrenzen hebben. Zie het [ overzicht van bronnen ](../sources/home.md) voor een catalogus van bronnen u voor gegevensopname kunt gebruiken. |

{style="table-layout:auto"}

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platform Services-instructies, informatie over end-to-end latentie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [ de diagrammen van de de latentie van begin tot eind ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) voor diverse diensten van Experience Platform.
* [ Real-Time Customer Data Platform (B2C Edition - Prime en de Pakketten van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2P - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2B - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
