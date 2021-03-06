---
keywords: cloudopslag;cloudopslag
title: Overzicht van Cloud Storage-bestemmingen
description: Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw Amazon S3-, AWS Kinesis-, Azure Event Hubs- of SFTP-cloudopslaglocaties.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 818c9a6f5cd39db1405827b657872b99254ad1e5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Overzicht van opslagdoelen voor cloud {#cloud-storage-destinations}

## Overzicht {#overview}

Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV-bestanden voor [!DNL Amazon S3], [!DNL Azure Blob] en SFTP. Voor [!DNL Amazon Kinesis] en [!DNL Azure Event Hubs] doelen, gegevens worden gestreamd uit Experience Platform in [!DNL JSON] gebruiken.

![Adobe-cloudopslagbestemmingen](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Ondersteunde cloudopslagbestemmingen {#supported-destinations}

Adobe Experience Platform ondersteunt de volgende cloudopslagdoelen:

* [Amazon Kinesis-verbinding](amazon-kinesis.md)
* [Amazon S3-verbinding](amazon-s3.md)
* [Azure Blob-verbinding](azure-blob.md)
* [Azure Event Hubs-verbinding](azure-event-hubs.md)
* [SFTP-verbinding](sftp.md)

## Verbinding maken met een nieuwe bestemming voor cloudopslag {#connect-destination}

Om segmenten naar de bestemmingen van de wolkenopslag voor uw campagnes te verzenden, moet het Platform eerst met de bestemming verbinden. Zie de [zelfstudie over het maken van doelen](../../ui/connect-destination.md) voor gedetailleerde informatie over het opzetten van een nieuwe bestemming.


## Macro&#39;s gebruiken om een map te maken op uw opslaglocatie {#use-macros}

>[!NOTE]
>
> De in deze sectie beschreven functionaliteit is momenteel beschikbaar voor [Amazon S3](amazon-s3.md) alleen bestemmingen.

Als u een aangepaste map per segmentbestand op uw opslaglocatie wilt maken, kunt u macro&#39;s gebruiken in het invoerveld voor het mappad. Voeg de macro&#39;s in aan het einde van het invoerveld, zoals hieronder wordt weergegeven.

![Macro&#39;s gebruiken om een map in uw opslagruimte te maken](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

In de onderstaande voorbeelden wordt verwezen naar een voorbeeldsegment `Luxury Audience` met id `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Invoer: `acme/campaigns/2021/%SEGMENT_NAME%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Invoer: `acme/campaigns/2021/%SEGMENT_ID%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Invoer: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Gegevensuitvoertype {#export-type}

Ondersteuning voor cloudopslagbestemmingen **Op profielen gebaseerde export**. Dit betekent dat u details exporteert over de personen in het publiek. Deze details zijn nodig voor verpersoonlijking en kunnen attributen, gebeurtenissen, segmentlidmaatschap, en meer omvatten.