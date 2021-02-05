---
keywords: SFTP;sftp
title: Bestemming SFTP-verbinding
description: Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# SFTP-verbinding

Creeer een levende uitgaande verbinding aan uw server SFTP om gescheiden gegevensdossiers van Experience Platform periodiek uit te voeren.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Doel {#connect-destination} verbinden

Zie [Workflow voor cloudopslagdoelen ](./workflow.md)voor instructies over hoe u verbinding kunt maken met uw cloudopslagdoelen, inclusief SFTP.

Voor bestemmingen SFTP, ga de volgende informatie in creeer bestemmingswerkschema, in **Authentificatie** stap in:

* **Host**: Het adres van uw opslagplaats SFTP
* **Gebruikersnaam**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie
* **Wachtwoord**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie

## Geëxporteerde gegevens {#exported-data}

Voor SFTP-doelen maakt Platform een door tabs gescheiden `.txt` of `.csv` bestand op de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.