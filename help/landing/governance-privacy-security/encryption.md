---
title: Gegevensversleuteling in Adobe Experience Platform
topic-legacy: data protection
description: Leer hoe gegevens worden gecodeerd tijdens de doorvoer en in rust in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Gegevenscodering in Adobe Experience Platform

Adobe Experience Platform is een krachtig en uitbreidbaar systeem dat gegevens over de klantervaring centraliseert en standaardisert voor alle bedrijfsoplossingen. Alle gegevens die door Platform worden gebruikt, worden tijdens de doorvoer en in rust gecodeerd om uw gegevens veilig te houden. In dit document worden de versleutelingsprocessen van Platform op een hoog niveau beschreven.

In het volgende stroomdiagram wordt getoond hoe gegevens worden opgenomen, gecodeerd en door [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Gegevens in doorvoer {#in-transit}

Alle gegevens die tussen Platform en om het even welke externe component worden doorgevoerd over veilige, gecodeerde verbindingen die HTTPS gebruiken [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

In het algemeen worden gegevens op drie manieren in Platform gebracht:

* [Gegevensverzameling](../../collection/home.md) met de mogelijkheden kunnen websites en mobiele toepassingen gegevens naar het Edge Network van het Platform verzenden voor ophaling en voorbereiding voor opname.
* [Bronaansluitingen](../../sources/home.md) stroomgegevens rechtstreeks naar Platform vanuit Adobe Experience Cloud-toepassingen en andere bedrijfsgegevensbronnen.
* Met niet-Adobe ETL-gereedschappen (extractie, transformatie, laden) worden gegevens verzonden naar de [batch-invoer-API](../../ingestion/batch-ingestion/overview.md) voor consumptie.

Nadat gegevens in het systeem zijn ingevoerd en [gecodeerd in rust](#at-rest), kan het vervolgens door de diensten van de Platform worden verrijkt en op de volgende manieren uit het systeem worden gehaald:

* [Doelen](../../destinations/home.md) staat u toe om gegevens aan Adobe toepassingen en partnertoepassingen te activeren.
* Native Platform-toepassingen zoals [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) en [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) kan ook gebruikmaken van de gegevens.

## Gegevens in rust {#at-rest}

Gegevens die door Platform worden opgenomen en gebruikt, worden opgeslagen in het datumpeer, een hoogst korrelige gegevensopslag die alle gegevens bevat die door het systeem, ongeacht oorsprong of dossierformaat worden beheerd. Alle gegevens die in het gegevensmeer worden voortgeduurd, worden gecodeerd, opgeslagen en in geïsoleerd [[!DNL Microsoft Azure Data Lake] Opslag](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) -instantie die uniek is voor uw organisatie.

Voor meer informatie over hoe gegevens in rust worden gecodeerd in Azure Data Lake Storage en Cosmos DB raadpleegt u de [officiële Azure-documentatie](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

## Volgende stappen

Dit document biedt een uitgebreid overzicht van de manier waarop gegevens in Platform worden gecodeerd. Voor meer informatie over veiligheidsprocedures in Platform, zie het overzicht over [bestuur, privacy en veiligheid](./overview.md) op Experience League, of neem een blik bij [whitepaper over beveiliging van Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
