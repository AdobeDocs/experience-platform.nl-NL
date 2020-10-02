---
keywords: SFTP;sftp
title: SFTP-bestemming
seo-title: SFTP-bestemming
description: Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.
seo-description: Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# SFTP-bestemming

## Overzicht

Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.

## Exporttype {#export-type}

**Profielexport** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](/help/rtcdp/destinations/activate-destinations.md#select-attributes).

![Op SFTP-profiel gebaseerd exporttype](/help/rtcdp/destinations/assets/sftp-export-type.png)

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloudopslagdoelen ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)voor instructies over hoe u verbinding kunt maken met uw cloudopslagdoelen, inclusief SFTP.

Voor bestemmingen SFTP, ga de volgende informatie in creeer bestemmingswerkschema, in de stap van de **Authentificatie** in:

* **Host**: het adres van uw opslagplaats SFTP
* **Gebruikersnaam**: de gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie
* **Wachtwoord**: het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie

## Geëxporteerde gegevens {#exported-data}

Voor bestemmingen SFTP, leidt Adobe in real time CDP tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie de bestemmingen van de Marketing van de [E-mail en de opslagbestemmingen](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) van de Wolk in de zelfstudie van de segmentactivering.