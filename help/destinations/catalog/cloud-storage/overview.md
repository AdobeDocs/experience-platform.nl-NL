---
keywords: cloudopslag;cloudopslag
title: Overzicht van Cloud Storage-bestemmingen
description: Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw Amazon S3-, AWS Kinesis-, Azure Event Hubs- of SFTP-cloudopslaglocaties.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Overzicht van cloudopslagdoelen {#cloud-storage-destinations}

Adobe Experience Platform kan uw segmenten als gegevensbestanden leveren aan uw locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV-bestanden of bestanden met tabs als scheidingsteken voor [!DNL Amazon S3] en SFTP. Voor [!DNL AWS Kinesis]- en [!DNL Azure Event Hubs]-doelen worden gegevens uit Experience Platform gestreamd in JSON-indeling.

![Adobe-cloudopslagbestemmingen](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Voor informatie over hoe te om met de bestemmingen van de wolkenopslag te verbinden, zie [Workflow om wolkenopslagbestemmingen tot stand te brengen](./workflow.md).

## Gegevensuitvoertype

**Op profiel gebaseerde export** : u exporteert details over de personen in het publiek. Deze details zijn nodig voor verpersoonlijking en kunnen attributen, gebeurtenissen, segmentlidmaatschap, enz. omvatten.

## Beschikbare cloudopslagbestemmingen

- [Amazon S3-bestemming](./amazon-s3.md)
- [Azure Blob-bestemming](./azure-blob.md)
- [SFTP-bestemming](./sftp.md)

## Beschikbare streamingdoelen voor cloudopslag

- [Amazon Kinesis-bestemming](./amazon-kinesis.md)
- [Azure Event Hubs-bestemming](./azure-event-hubs.md)