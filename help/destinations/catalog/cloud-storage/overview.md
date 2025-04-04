---
keywords: cloudopslag;cloudopslag
title: Overzicht van Cloud Storage-bestemmingen
description: Adobe Experience Platform kan uw publiek als gegevensbestanden leveren aan uw Amazon S3-, AWS Kinesis-, Azure Event Hubs- of SFTP-cloudopslaglocaties.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Overzicht van opslagdoelen voor cloud {#cloud-storage-destinations}

## Overzicht {#overview}

Adobe Experience Platform kan uw publiek als gegevensbestanden leveren aan uw opslaglocaties in de cloud. Hierdoor kunt u soorten publiek en hun profielkenmerken naar uw interne systemen verzenden via CSV-bestanden voor [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] en SFTP. Voor [!DNL Amazon Kinesis] - en [!DNL Azure Event Hubs] -doelen worden gegevens in [!DNL JSON] -indeling uit Experience Platform gestreamd.

![ de bestemmingen van de wolkenopslag van Adobe ](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Ondersteunde cloudopslagbestemmingen {#supported-destinations}

Adobe Experience Platform ondersteunt gegevensexport naar de volgende cloudopslagdoelen:

* [Amazon Kinesis-verbinding](amazon-kinesis.md)
* [Amazon S3-verbinding](amazon-s3.md)
* [Azure Blob-verbinding](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure Event Hubs-verbinding](azure-event-hubs.md)
* [Gegevenslandingszone](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [SFTP-verbinding](sftp.md)

## Verbinding maken met een nieuwe bestemming voor cloudopslag {#connect-destination}

Experience Platform moet eerst verbinding maken met het doel om het publiek voor uw campagnes naar cloudopslagbestemmingen te sturen. Zie het [ leerprogramma van de bestemmingsverwezenlijking ](../../ui/connect-destination.md) voor gedetailleerde informatie bij vestiging een nieuwe bestemming.


## Macro&#39;s gebruiken om een map te maken op uw opslaglocatie {#use-macros}

>[!NOTE]
>
> De functionaliteit die in dit gedeelte wordt beschreven, is beschikbaar voor alle cloudopslagdoelen. Nochtans, steunt de [ bestemming van Amazon S3 ](amazon-s3.md) momenteel slechts de `%SEGMENT_ID%` en `%SEGMENT_NAME%` macro&#39;s.

Als u een aangepaste map per doelbestand op uw opslaglocatie wilt maken, kunt u macro&#39;s gebruiken in het invoerveld voor het mappad. Voeg de macro&#39;s in aan het einde van het invoerveld, zoals hieronder wordt weergegeven.

![ hoe te om macro&#39;s te gebruiken om een omslag in uw opslag tot stand te brengen ](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

In de onderstaande voorbeelden wordt verwezen naar een voorbeeldpubliek `Luxury Audience` met ID `25768be6-ebd5-45cc-8913-12fb3f348615` .

**Macro 1:`%SEGMENT_NAME%`**

Invoer: `acme/campaigns/2021/%SEGMENT_NAME%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Invoer: `acme/campaigns/2021/%SEGMENT_ID%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Invoer: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Mappad op uw opslaglocatie: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Verdere macro&#39;s**

Net als in de bovenstaande voorbeelden kunt u aanvullende macro&#39;s gebruiken om een aangepaste mapstructuur te maken op de maplocatie:

* `%DATETIME%` of `%TIMESTAMP%` om een aangepaste mapnaam toe te voegen op basis van de exporttijd van de bestanden. De indeling voor de eerste macro is `MMDDYYYY_HHMMSS` en een UNIX-indeling van 10 cijfers voor de tweede macro.
* `%DESTINATION_NAME%` om een aangepaste map toe te voegen op basis van de naam van de doelgegevensstroom.

## Gegevensuitvoertype {#export-type}

De opslagbestemmingen van de wolk steunen de volgende uitvoertypes:
* **op profiel-gebaseerde uitvoer**. Dit betekent dat u details exporteert over de personen in het publiek. Deze details zijn nodig voor verpersoonlijking en kunnen attributen, gebeurtenissen, publiekslidmaatschappen, en meer omvatten.
* **de uitvoer van de Dataset**. Deze functionaliteit staat u toe om volledige datasets naar de bestemmingen van de wolkenopslag uit te voeren. [Lees meer](/help/destinations/ui/export-datasets.md) over de nieuwe functionaliteit.

## Volgende stappen {#next-steps}

Na het selecteren van welke één van [ gesteunde wolkenbestemmingen ](#supported-destinations) u zou willen gebruiken, [ verbind met bestemmingsleerprogramma ](/help/destinations/ui/connect-destination.md) leren hoe te om een verbinding aan de bestemming te vestigen. Dan, lees het activeringsleerprogramma aan op dossier-gebaseerde bestemmingen om te leren hoe te [ het uitvoeren ](/help/destinations/ui/activate-batch-profile-destinations.md) gegevens aan uw bestemming van de wolkenopslag beginnen.
