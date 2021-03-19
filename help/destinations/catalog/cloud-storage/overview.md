---
keywords: cloudopslag;cloudopslag
title: Overzicht van Cloud Storage-bestemmingen
description: Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw Amazon S3-, AWS Kinesis-, Azure Event Hubs- of SFTP-cloudopslaglocaties.
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Overzicht van cloudopslagdoelen {#cloud-storage-destinations}

Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV of bestanden met tabs als scheidingsteken voor [!DNL Amazon S3], [!DNL Azure Blob] en SFTP. Voor [!DNL Amazon Kinesis]- en [!DNL Azure Event Hubs]-doelen worden gegevens uit Experience Platform gestreamd in JSON-indeling.

![Adobe-cloudopslagbestemmingen](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Voor informatie over hoe te om met de bestemmingen van de wolkenopslag te verbinden, zie [Workflow om wolkenopslagbestemmingen tot stand te brengen](./workflow.md).

## Gegevensuitvoertype

**Op profiel gebaseerde export** : u exporteert details over de personen in het publiek. Deze details zijn nodig voor verpersoonlijking en kunnen attributen, gebeurtenissen, segmentlidmaatschap, en meer omvatten.

## Beschikbare cloudopslagbestemmingen

- [Amazon S3-verbinding](./amazon-s3.md)
- [Azure Blob-verbinding](./azure-blob.md)
- [SFTP-verbinding](./sftp.md)

## Beschikbare streamingdoelen voor cloudopslag

- [Amazon Kinesis-verbinding](./amazon-kinesis.md)
- [Azure Event Hubs-verbinding](./azure-event-hubs.md)