---
keywords: Amazon S3;S3 doel;s3;amazon s3
title: Amazon S3-verbinding
description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
translation-type: tm+mt
source-git-commit: d77cd063e61118631b757d9821267b2fd6ab0148
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!DNL Amazon S3] verbinding  {#s3-connection}

## Overzicht {#overview}

Creeer een levende uitgaande verbinding aan uw [!DNL Amazon Web Services] (AWS) S3 opslag om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Exporttype op basis van Amazon S3-profielen](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Doel {#connect-destination} verbinden

Zie [Workflow ](./workflow.md) voor cloudopslagdoelen voor instructies voor het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Amazon S3].

Voor [!DNL Amazon S3] bestemmingen, ga de volgende informatie in tot bestemmingswerkschema:

* **[!DNL Amazon S3]toegangstoets en  [!DNL Amazon S3] geheime sleutel**: In  [!DNL Amazon S3], produceer een  `access key - secret access key` paar om Platform toegang tot uw  [!DNL Amazon S3] rekening te verlenen. Meer informatie vindt u in de [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

## Vereiste [!DNL Amazon S3] machtigingen {#required-s3-permission}

Als u gegevens met succes wilt verbinden en exporteren naar uw [!DNL Amazon S3]-opslaglocatie, maakt u een IAM-gebruiker voor [!DNL Platform] in [!DNL Amazon S3] en wijst u machtigingen toe voor de volgende handelingen:

* `s3:DeleteObject`
* `s3:DeleteObjectVersion`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:GetObjectVersion`
* `s3:ListBucket`
* `s3:ListBuckets`
* `s3:PutBucketVersioning`
* `s3:PutObject`
* `s3:ReplicateObject`
* `s3:RestoreObject`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Amazon S3] bestemmingen, [!DNL Platform] leidt tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.
