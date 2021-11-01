---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;salesforce bestemming
title: Verbinding met Salesforce-Marketing Cloud
seo-description: Salesforce Marketing Cloud is a digital marketing suite formerly known as ExactTarget that allows you to build and customize journeys for visitors and customers to personalize their experience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: b0d6e02c67f2a62971332acb224c7422ea467e6c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Segmentgegevens verzenden naar [!DNL Salesforce Marketing Cloud]moet u eerst [verbinden de bestemming](#connect-destination) in Platform en vervolgens [een gegevensimport instellen](#import-data-into-salesforce) vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud].

## Exporttype {#export-type}

**Op basis van profiel** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met selectiekenmerken van het dialoogvenster [activeringsworkflow voor publiek](../../ui/activate-batch-profile-destinations.md#select-attributes).

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

Voor [!DNL Salesforce Marketing Cloud] doelen, Platform maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [segmentactivering controleren](../../ui/activate-batch-profile-destinations.md#verify) in de zelfstudie voor segmentactivering.

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Na verbinding [!DNL Platform] aan uw [!DNL SFTP] -opslag, moet u de gegevens die u importeert vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud]. Ga voor meer informatie over het uitvoeren van deze taak naar [Abonnees importeren in Marketing Cloud vanuit een bestand](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in de [!DNL Salesforce Help Center].
