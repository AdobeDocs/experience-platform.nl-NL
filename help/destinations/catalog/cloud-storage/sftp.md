---
keywords: SFTP;sftp
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 99bb5d1b76b926622ca21fa1df7c3cb9fabc4856
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# SFTP-verbinding

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Adobe gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen opslaglocaties voor de cloud voor het exporteren van gegevens: [!DNL Amazon S3] en [!DNL Azure Blob].

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als Base64 gecodeerde koord worden geschreven."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="SSH-toets"
>abstract="De sleutel SSH vereist een koord Base64."

Wanneer [verbinden](../../ui/connect-destination.md) aan deze bestemming, moet u de volgende informatie verstrekken:

#### Verificatiegegevens {#authentication-information}

Als u **[!UICONTROL Basic authentication]** type voor verbinding met uw SFTP-locatie:

![Basisverificatie van SFTP-bestemming](../..//assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Het adres van uw opslagplaats SFTP;
* **[!UICONTROL Username]**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie;
* **[!UICONTROL Password]**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
   * Voorbeeld: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![PGP-toets](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


Als u **[!UICONTROL SFTP with SSH key]** verificatietype voor verbinding met uw SFTP-locatie:

![SSH-sleutelverificatie voor SFTP-bestemming](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Vul het IP-adres of de domeinnaam van uw SFTP-account in
* **[!UICONTROL Port]**: De poort die wordt gebruikt door uw SFTP-opslaglocatie;
* **[!UICONTROL Username]**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie;
* **[!UICONTROL SSH Key]**: De SSH-sleutel om u aan te melden bij uw SFTP-opslaglocatie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
   * Voorbeeld: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![PGP-toets](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Doelgegevens {#destination-details}

Na het vestigen van de authentificatieverbinding aan de plaats SFTP, verstrek de volgende informatie voor de bestemming:

![Beschikbare bestemmingsdetails voor bestemming SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Voer een naam in die u zal helpen deze bestemming in het gebruikersinterface van het Experience Platform identificeren;
* **[!UICONTROL Description]**: een beschrijving voor deze bestemming invoeren;
* **[!UICONTROL Folder path]**: Voer het pad in naar de map op de SFTP-locatie waar de bestanden worden geëxporteerd.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL SFTP] doelen, Platform maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) in de zelfstudie voor segmentactivering.

## IP adres lijst van gewenste personen

Zie [IP adres lijst van gewenste personen voor wolkenopslagbestemmingen](ip-address-allow-list.md) als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.
