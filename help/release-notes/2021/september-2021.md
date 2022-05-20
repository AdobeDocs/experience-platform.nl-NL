---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2021
description: In de release van september 2021 staat een opmerking voor Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '377'
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
| Upsert or patch Profile records using Batch-opname | Klantprofiel in realtime staat nu updates toe naar profielkenmerken in afzonderlijke profielrecordgegevens via batch-opname. Raadpleeg voor meer informatie de [handleiding voor het ontwikkelen van batch-inhoud](../../ingestion/batch-ingestion/api-overview.md). |

Ga voor meer informatie over het opnemen van gegevens in het Platform naar de [Documentatie over gegevensinname](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het streamen van gegevensstromen | U kunt nu functies van het gegevensvoorvoegsel gebruiken wanneer u een streaming gegevensstroom maakt voor [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], en [!DNL Google PubSub]. Zie de zelfstudie aan [streaming-gegevensstroom maken voor bronnen voor cloudopslag](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) voor meer informatie . |

Meer informatie over [!DNL Data Prep] zie [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Data Landing Zone] | U kunt nu een [!DNL Data Landing Zone] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] is een [!DNL Azure Blob] opslaginterface die door Platform wordt geleverd, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden in Platform te brengen. Zie de [[!DNL Data Landing Zone] overzicht](../../sources/connectors/cloud-storage/data-landing-zone.md) voor meer informatie . |
| [!DNL Snowflake] | U kunt nu een [!DNL Snowflake] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/databases/snowflake.md) om gegevens van uw [!DNL Snowflake] database naar Platform. Zie de [[!DNL Snowflake] overzicht](../../sources/connectors/databases/snowflake.md) voor meer informatie . |
| [!DNL SFTP] bronverbeteringen | U kunt handmatig een aangepast poortnummer instellen wanneer u een [!DNL SFTP] bronverbinding. Zie de [[!DNL SFTP] overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie . |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
