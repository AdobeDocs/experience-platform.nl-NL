---
keywords: SFTP;sftp
title: SFTP-bestemming
seo-title: SFTP-bestemming
description: Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.
seo-description: Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# SFTP-bestemming

## Overzicht

Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloudopslagdoelen ](./workflow.md)voor instructies over hoe u verbinding kunt maken met uw cloudopslagdoelen, inclusief SFTP.

Voor bestemmingen SFTP, ga de volgende informatie in creeer bestemmingswerkschema, in de stap van de **Authentificatie** in:

* **Host**: Het adres van uw opslagplaats SFTP
* **Gebruikersnaam**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie
* **Wachtwoord**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie

## Geëxporteerde gegevens {#exported-data}

Voor bestemmingen SFTP, in real time CDP leidt tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie de bestemmingen van de Marketing van de [E-mail en de opslagbestemmingen](../../ui/activate-destinations.md#esp-and-cloud-storage) van de Wolk in de zelfstudie van de segmentactivering.