---
keywords: Amazon S3;S3 doel;s3;amazon s3
title: Amazon S3-verbinding
description: Creeer een levende uitgaande verbinding aan uw opslag van het Web van Amazon van de Diensten (AWS) S3 om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# [!DNL Amazon S3] verbinding {#s3-connection}

## Overzicht {#overview}

Creeer een levende uitgaande verbinding aan uw [!DNL Amazon Web Services] (AWS) S3 opslag om lusje-afgebakende of CSV gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-segment-streaming-destinations.md#mapping).

![Exporttype op basis van Amazon S3-profielen](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!DNL Amazon S3]toegangstoets** en  **[!DNL Amazon S3]geheime sleutel**: In  [!DNL Amazon S3], produceer een  `access key - secret access key` paar om Platform toegang tot uw  [!DNL Amazon S3] rekening te verlenen. Meer informatie vindt u in de [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Bucket name]**: Voer de naam in van het  [!DNL Amazon S3] emmertje dat door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

>[!TIP]
>
>In de Connect-doelworkflow kunt u per geëxporteerd segmentbestand een aangepaste map in uw Amazon S3-opslag maken. Lees [Gebruik macro&#39;s om een map op uw opslaglocatie te maken](overview.md#use-macros) voor instructies.

### Vereiste [!DNL Amazon S3]-machtigingen {#required-s3-permission}

Als u gegevens wilt verbinden en exporteren naar uw [!DNL Amazon S3]-opslaglocatie, maakt u een gebruikers voor Identiteit en Toegangsbeheer (IAM) voor [!DNL Platform] in [!DNL Amazon S3] en wijst u machtigingen toe voor de volgende handelingen:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van de activering om profieluitvoer bestemmingen ](../../ui/activate-batch-profile-destinations.md) voor instructies te plaatsen bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Amazon S3] bestemmingen, [!DNL Platform] leidt tot een lusje-afgebakend `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [Activate publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../../ui/activate-batch-profile-destinations.md) in de zelfstudie van de segmentactivering.
