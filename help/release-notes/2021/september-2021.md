---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2021
description: In de release van september 2021 staat een opmerking voor Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 29 september 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensopname](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

## Gegevensopname {#ingestion}

De Ingestie van Gegevens van Adobe Experience Platform vertegenwoordigt de veelvoudige methodes waardoor Platform gegevens uit diverse bronnen opneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van het Platform worden voortgeduurd.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
|------- | -----------|
| Upsert or patch Profile records using Batch-opname | Klantprofiel in realtime staat nu updates toe naar profielkenmerken in afzonderlijke profielrecordgegevens via batch-opname. Om meer te leren, verwijs naar de [ gids van de de partijenontwikkelaar ](../../ingestion/batch-ingestion/api-overview.md). |

Meer leren over het opnemen van gegevens in Platform, bezoek de [ documentatie van de Ingestie van Gegevens ](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het streamen van gegevensstromen | U kunt nu functies van het gegevensvoorvoegsel gebruiken wanneer u een streaming gegevensstroom maakt voor [!DNL Amazon Kinesis] , [!DNL Azure Event Hubs] en [!DNL Google PubSub] . Zie het leerprogramma op [ creërend een het stromen dataflow voor de bronnen van de wolkenopslag ](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) voor meer informatie. |

Meer over [!DNL Data Prep] leren zie het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Data Landing Zone] | U kunt een [!DNL Data Landing Zone] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) of het [ gebruikersinterface ](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die is ingericht door Platform en u toegang biedt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor bestanden om bestanden over te brengen naar Platform. Zie het [[!DNL Data Landing Zone]  overzicht ](../../sources/connectors/cloud-storage/data-landing-zone.md) voor meer informatie. |
| [!DNL Snowflake] | U kunt een [!DNL Snowflake] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/databases/snowflake.md) of het [ gebruikersinterface ](../../sources/tutorials/ui/create/databases/snowflake.md) om gegevens van uw [!DNL Snowflake] gegevensbestand aan Platform te brengen. Zie het [[!DNL Snowflake]  overzicht ](../../sources/connectors/databases/snowflake.md) voor meer informatie. |
| [!DNL SFTP] bronverbeteringen | U kunt handmatig een aangepast poortnummer instellen wanneer u een [!DNL SFTP] bronverbinding maakt. Zie het [[!DNL SFTP]  overzicht ](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
