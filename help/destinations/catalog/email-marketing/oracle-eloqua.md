---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle eloqua;oracle
title: Oracle Eloqua-verbinding
description: Oracle Eloqua is een softwareplatform als service (SaaS) voor marketingautomatisering dat door Oracle wordt aangeboden en dat bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkooplood te beheren.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) is software als serviceplatform voor marketingautomatisering die wordt aangeboden door [!DNL Oracle] die bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en productie van verkooplood te beheren.

Segmentgegevens verzenden naar [!DNL Oracle Eloqua]moet u eerst [verbinden de bestemming](#connect-destination) in Adobe Experience Platform, en vervolgens [een gegevensimport instellen](#import-data-into-eloqua) vanaf uw opslaglocatie naar [!DNL Oracle Eloqua].

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP adres lijst van gewenste personen {#allow-list}

Bij het vestigen van e-mail marketing bestemmingen met opslag SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Zie [IP adres lijst van gewenste personen voor wolkenopslagbestemmingen](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u verstrekken:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u verstrekken:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan geëxporteerde bestanden onder de **[!UICONTROL Key]** sectie. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
* **[!UICONTROL Folder Path]**: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV-bestanden indient.
* **[!UICONTROL File Format]**: Selecteren **CSV** om CSV-bestanden naar uw opslaglocatie te exporteren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Segmenten naar dit doel activeren {#activate}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Doelkenmerken {#destination-attributes}

Bij het activeren van segmenten op dit doel raadt Adobe u aan een unieke id te selecteren in uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Raadpleeg voor meer informatie [best practices bij het activeren van doelgroepen naar marketingdoelen per e-mail](overview.md#best-practices).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Eloqua] doelen, Platform maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [segmentactivering controleren](../../ui/activate-batch-profile-destinations.md#verify) in de zelfstudie voor segmentactivering.

## Gegevensimport instellen in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Na verbinding [!DNL Platform] aan uw [!DNL SFTP] -opslag, moet u de gegevens die u importeert vanaf uw opslaglocatie naar [!DNL Oracle Eloqua]. Ga voor meer informatie over het uitvoeren van deze taak naar [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in de [!DNL Oracle Eloqua Help Center].
