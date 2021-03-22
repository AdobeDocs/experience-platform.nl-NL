---
keywords: SFTP;sftp
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# SFTP-verbinding

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Adobe gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens [!DNL Amazon S3] en [!DNL Azure Blob].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Doel {#connect-destination} verbinden

Raadpleeg de [workflow voor cloudopslagdoelen ](./workflow.md) voor instructies over hoe u verbinding kunt maken met uw cloudopslagdoelen, inclusief SFTP.

Voor bestemmingen SFTP, ga de volgende informatie in creeer bestemmingswerkschema, in **Authentificatie** stap in:

* **Host**: Het adres van uw opslagplaats SFTP
* **Gebruikersnaam**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie
* **Wachtwoord**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie

## Geëxporteerde gegevens {#exported-data}

Voor SFTP-doelen maakt Platform een door tabs gescheiden `.txt` of `.csv` bestand op de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## IP adres lijst van gewenste personen

Verwijs naar [IP adreslijst van gewenste personen voor wolkenopslagbestemmingen ](./ip-address-allow-list.md) als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.