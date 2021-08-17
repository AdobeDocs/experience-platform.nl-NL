---
keywords: SFTP;sftp
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# SFTP-verbinding

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Adobe gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens [!DNL Amazon S3] en [!DNL Azure Blob].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-batch-profile-destinations.md).

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **Host**: Het adres van uw opslagplaats SFTP
* **Gebruikersnaam**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie
* **Wachtwoord**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL SFTP] bestemmingen, leidt het Platform tot een lusje-afgebakend `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [Activate publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../../ui/activate-batch-profile-destinations.md) in de zelfstudie van de segmentactivering.

## IP adres lijst van gewenste personen

Verwijs naar [IP adreslijst van gewenste personen voor wolkenopslagbestemmingen ](ip-address-allow-list.md) als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.
