---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 4959b5227f777a2c8cab1317d67795678d1a6eea
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 29 september 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensinname](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

## Gegevensinname {#ingestion}

De Ingestie van Gegevens van Adobe Experience Platform vertegenwoordigt de veelvoudige methodes waardoor Platform gegevens uit diverse bronnen inneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van het Platform worden voortgeduurd.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Upsert or patch Profile records using Batch-opname | Klantprofiel in realtime staat nu updates toe naar profielkenmerken in afzonderlijke profielrecordgegevens via batch-opname. Voor meer informatie raadpleegt u de handleiding [voor het ontwikkelen van batches](../../ingestion/batch-ingestion/api-overview.md). |

Meer over het opnemen van gegevens in Platform, bezoek [de documentatie van de Ingestie van Gegevens](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het streamen van gegevensstromen | U kunt de functies van het gegevensvoorvoegsel nu gebruiken wanneer het creëren van een het stromen gegevensstroom voor [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], en [!DNL Google PubSub]. Zie de zelfstudie over het maken van een streaminggegevensstroom voor bronnen voor cloudopslag](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) voor meer informatie.[ |

Voor meer informatie over [!DNL Data Prep] zie [[!DNL Data Prep] overview](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Data Landing Zone] | U kunt nu een [!DNL Data Landing Zone] bronverbinding maken met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] is een  [!DNL Azure Blob] opslaginterface die door Platform wordt ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden binnen en buiten het Platform in te voeren en te egress. Zie [[!DNL Data Landing Zone] overzicht](../../sources/connectors/cloud-storage/data-landing-zone.md) voor meer informatie. |
| [!DNL Snowflake] | U kunt nu een [!DNL Snowflake] bronverbinding tot stand brengen gebruikend [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) of [gebruikersinterface](../../sources/tutorials/ui/create/databases/snowflake.md) om gegevens van uw [!DNL Snowflake] gegevensbestand aan Platform te brengen. Zie [[!DNL Snowflake] overzicht](../../sources/connectors/databases/snowflake.md) voor meer informatie. |
| [!DNL SFTP] bronverbeteringen | U kunt handmatig een aangepast poortnummer instellen wanneer u een [!DNL SFTP]-bronverbinding maakt. Zie [[!DNL SFTP] overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
