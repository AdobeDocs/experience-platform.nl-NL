---
keywords: Amazon S3;S3 doel;s3;amazon s3
title: Amazon S3-verbinding
description: Creeer een levende uitgaande verbinding aan uw opslag van Amazon Web Services (AWS) S3 om CSV- gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: bf46f4e6549fcbd975a9f0a6034040ed2e9b34e6
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# [!DNL Amazon S3] verbinding {#s3-connection}

## Overzicht {#overview}

Een live uitgaande verbinding maken met uw [!DNL Amazon Web Services] (AWS) S3-opslag om CSV-gegevensbestanden periodiek van Adobe Experience Platform naar uw eigen S3-emmers te exporteren.

## Exporttype {#export-type}

**Op basis van profiel** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met selectiekenmerken van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-segment-streaming-destinations.md#mapping).

![Exporttype op basis van Amazon S3-profielen](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als Base64 gecodeerde koord worden geschreven."
>text="Learn more in documentation"

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!DNL Amazon S3]toegangstoets** en **[!DNL Amazon S3]geheime sleutel**: In [!DNL Amazon S3], een `access key - secret access key` paar om Platform toegang tot uw te verlenen [!DNL Amazon S3] account. Meer informatie in het dialoogvenster [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.

>[!TIP]
>
>In de Connect-doelworkflow kunt u per geëxporteerd segmentbestand een aangepaste map in uw Amazon S3-opslagruimte maken. Lezen [Macro&#39;s gebruiken om een map te maken op uw opslaglocatie](overview.md#use-macros) voor instructies.

### Vereist [!DNL Amazon S3] machtigingen {#required-s3-permission}

Om gegevens met succes te verbinden en uit te voeren aan uw [!DNL Amazon S3] opslaglocatie, een gebruiker voor Identiteit en Toegangsbeheer (IAM) maken voor [!DNL Platform] in [!DNL Amazon S3] en wijs toestemmingen voor de volgende acties toe:

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

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Amazon S3] bestemmingen, [!DNL Platform] maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) in de zelfstudie voor segmentactivering.
