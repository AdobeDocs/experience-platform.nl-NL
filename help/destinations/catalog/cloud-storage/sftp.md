---
keywords: SFTP;sftp
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# SFTP-verbinding

## Doelwijziging {#changelog}

>[!IMPORTANT]
>
>Met de bètaversie van de functionaliteit van de uitvoerdatasets en de verbeterde functionaliteit van de dossieruitvoer, kunt u twee nu zien [!DNL SFTP] kaarten in de lijst met bestemmingen.
>* Als u al bestanden exporteert naar de **[!UICONTROL SFTP]** bestemming: Maak nieuwe gegevensstromen naar de nieuwe **[!UICONTROL SFTP beta]** bestemming.
>* Als u nog geen gegevens hebt gemaakt voor de **[!UICONTROL SFTP]** bestemming, gelieve te gebruiken nieuwe **[!UICONTROL SFTP beta]** kaart om bestanden te exporteren naar **[!UICONTROL SFTP]**.


![Afbeelding van de twee SFTP-doelkaarten in een weergave Naast elkaar.](/help/destinations/assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Verbeteringen in de nieuwe [!DNL SFTP] bestemmingskaart omvat:

* [Ondersteuning voor gegevensexport](/help/destinations/ui/export-datasets.md).
* Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Mogelijkheid om de opmaak van geëxporteerde CSV-gegevensbestanden aan te passen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Experience Platform gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens: [!DNL Amazon S3] en [!DNL SFTP].

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Op SFTP-profiel gebaseerd exporttype](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verificatiegegevens {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als Base64 gecodeerde koord worden geschreven."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Persoonlijke SSH-sleutel"
>abstract="De persoonlijke sleutel van SSH moet als Base64-Gecodeerde koord worden geformatteerd en moet niet wachtwoord-beschermd zijn."

Als u **[!UICONTROL Basic authentication]** type voor verbinding met uw SFTP-locatie:

![Basisverificatie van SFTP-bestemming](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Het adres van uw opslagplaats SFTP;
* **[!UICONTROL Username]**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie;
* **[!UICONTROL Password]**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64-encoded] tekenreeks. Bekijk een voorbeeld van een correct geformatteerde, base64-gecodeerde sleutel in de documentatieverbinding hieronder. Het middelste deel wordt verkort om kort te zijn.

![Afbeelding die een voorbeeld toont van een PGP-sleutel met de juiste indeling en basis64-codering in de gebruikersinterface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Als u **[!UICONTROL SFTP with SSH key]** verificatietype voor verbinding met uw SFTP-locatie:

![SSH-sleutelverificatie voor SFTP-bestemming](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Vul het IP-adres of de domeinnaam van uw SFTP-account in
* **[!UICONTROL Port]**: De poort die wordt gebruikt door uw SFTP-opslaglocatie;
* **[!UICONTROL Username]**: De gebruikersnaam die moet worden gebruikt om u aan te melden bij uw SFTP-opslaglocatie;
* **[!UICONTROL SSH Key]**: De persoonlijke SSH-sleutel die wordt gebruikt om u aan te melden bij uw SFTP-opslaglocatie. De persoonlijke sleutel moet zijn opgemaakt als een Base64-gecodeerde tekenreeks en mag niet met een wachtwoord zijn beveiligd.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
   * Voorbeeld: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Zie onder een voorbeeld van een correct geformatteerde sleutel PGP, met het middelste deel verkort voor beknoptheid.

      ![PGP-toets](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens {#destination-details}

Na het vestigen van de authentificatieverbinding aan de plaats SFTP, verstrek de volgende informatie voor de bestemming:

![Beschikbare bestemmingsdetails voor bestemming SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Voer een naam in die u zal helpen deze bestemming in het gebruikersinterface van het Experience Platform identificeren;
* **[!UICONTROL Description]**: een beschrijving voor deze bestemming invoeren;
* **[!UICONTROL Folder path]**: Voer het pad in naar de map op de SFTP-locatie waar de bestanden worden geëxporteerd.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## (bètaversie) Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt datasetuitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees [zelfstudie over exportgegevensbestanden](/help/destinations/ui/export-datasets.md).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL SFTP] doelen, Platform maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) in de zelfstudie voor segmentactivering.

## IP adres lijst van gewenste personen

Zie [IP adres lijst van gewenste personen voor wolkenopslagbestemmingen](ip-address-allow-list.md) als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.
