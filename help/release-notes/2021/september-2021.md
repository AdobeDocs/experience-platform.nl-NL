---
title: Aanvullende informatie van september 2021 voor Adobe Experience Platform
description: Aanvullende informatie voor de versie van september 2021 voor Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 23%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 29 september 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensopname](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

## Gegevensopname {#ingestion}

De Ingestie van Gegevens van Adobe Experience Platform vertegenwoordigt de veelvoudige methodes waardoor Experience Platform gegevens uit diverse bronnen opneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van Experience Platform worden voortgeduurd.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Upsert or patch Profile records using Batch-opname | Klantprofiel in realtime staat nu updates toe naar profielkenmerken in afzonderlijke profielrecordgegevens via batch-opname. Om meer te leren, verwijs naar de [ gids van de de partijenontwikkelaar ](../../ingestion/batch-ingestion/api-overview.md). |

Meer over het opnemen van gegevens in Experience Platform leren, bezoek de [ documentatie van de Ingestie van Gegevens ](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het streamen van gegevensstromen | U kunt nu functies van het gegevensvoorvoegsel gebruiken wanneer u een streaming gegevensstroom maakt voor [!DNL Amazon Kinesis] , [!DNL Azure Event Hubs] en [!DNL Google PubSub] . Zie het leerprogramma op [ creërend een het stromen dataflow voor de bronnen van de wolkenopslag ](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) voor meer informatie. |

Meer over [!DNL Data Prep] leren zie het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Data Landing Zone] | U kunt een [!DNL Data Landing Zone] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) of het [ gebruikersinterface ](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Experience Platform is ingericht en waarmee u toegang hebt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor bestanden om bestanden naar Experience Platform te brengen. Zie het [[!DNL Data Landing Zone]  overzicht ](../../sources/connectors/cloud-storage/data-landing-zone.md) voor meer informatie. |
| [!DNL Snowflake] | U kunt een [!DNL Snowflake] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/databases/snowflake.md) of het [ gebruikersinterface ](../../sources/tutorials/ui/create/databases/snowflake.md) om gegevens van uw [!DNL Snowflake] gegevensbestand aan Experience Platform te brengen. Zie het [[!DNL Snowflake]  overzicht ](../../sources/connectors/databases/snowflake.md) voor meer informatie. |
| [!DNL SFTP] bronverbeteringen | U kunt handmatig een aangepast poortnummer instellen wanneer u een [!DNL SFTP] bronverbinding maakt. Zie het [[!DNL SFTP]  overzicht ](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
