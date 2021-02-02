---
keywords: Amazon S3;S3 doel;s3;amazon s3
title: Amazon S3-bestemming
seo-title: Amazon S3-bestemming
description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
seo-description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Amazon S3] doel

## Overzicht

Creeer een levende uitgaande verbinding aan uw [!DNL Amazon Web Services] (AWS) S3 opslag om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Exporttype op basis van Amazon S3-profielen](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Doel {#connect-destination} verbinden

Zie [Workflow ](./workflow.md) voor cloudopslagdoelen voor instructies voor het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Amazon S3].

Voor [!DNL Amazon S3] bestemmingen, ga de volgende informatie in tot bestemmingswerkschema:

* **[!DNL Amazon S3]toegangstoets en  [!DNL Amazon S3] geheime sleutel**: In  [!DNL Amazon S3], produceer een  `access key - secret access key` paar om Platform toegang tot uw  [!DNL Amazon S3] rekening te verlenen. Meer informatie vindt u in de [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>Platform heeft `write` machtigingen nodig voor het emmerobject waar de exportbestanden worden geleverd.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Amazon S3] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.
