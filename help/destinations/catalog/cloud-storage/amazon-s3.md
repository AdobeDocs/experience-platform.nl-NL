---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3-bestemming
seo-title: Amazon S3-bestemming
description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
seo-description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] doel

## Overzicht

Creeer een levende uitgaande verbinding aan uw opslag [!DNL Amazon Web Services] (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Exporttype op basis van Amazon S3-profielen](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](./workflow.md) voor instructies over het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Amazon S3].

Voor [!DNL Amazon S3] bestemmingen, ga de volgende informatie in creeer bestemmingswerkschema in:

* **[!DNL Amazon S3]toegangstoets en [!DNL Amazon S3] geheime sleutel**: In [!DNL Amazon S3], produceer een `access key - secret access key` paar om toegang in real time CDP tot uw [!DNL Amazon S3] rekening te verlenen. Meer informatie vindt u in de documentatie [van](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.

>[!IMPORTANT]
>
>CDP in real time vereist `write` toestemmingen op het emmervoorwerp waar de de uitvoerdossiers zullen worden geleverd.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Amazon S3] bestemmingen, leidt in real time CDP tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie de bestemmingen van de Marketing van de [E-mail en de opslagbestemmingen](../../ui/activate-destinations.md#esp-and-cloud-storage) van de Wolk in de zelfstudie van de segmentactivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
