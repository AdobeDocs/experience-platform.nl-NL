---
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# SFTP-verbinding

## Doelwijziging {#changelog}

Met de versie van het Experience Platform van juli 2023, verstrekt de bestemming SFTP nieuwe functionaliteit, zoals hieronder vermeld:

* [Ondersteuning voor gegevensexport](/help/destinations/ui/export-datasets.md).
* Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Mogelijkheid om de opmaak van geëxporteerde CSV-gegevensbestanden aan te passen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Experience Platform gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens: [!DNL Amazon S3] en [!DNL Azure Blob].

## Verbinding maken met SFTP via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw SFTP-opslaglocatie via de gebruikersinterface van het platform, leest u de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u via programmacode verbinding wilt maken met uw SFTP-opslaglocatie, leest u de [Activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Op SFTP-profiel gebaseerd exporttype dat is gemarkeerd in de catalogus met doelen.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Procedure [de uitvoer datasets gebruikend het gebruikersinterface van het Platform](/help/destinations/ui/export-datasets.md).
* Procedure [de uitvoer datasets programmatically gebruikend de Dienst API van de Stroom](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Bij exporteren *publieksgegevens*, Platform maakt een `.csv`, `parquet`, of `.json` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden de [ondersteunde bestandsindelingen voor export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) in de zelfstudie voor publieksactivering.

Bij exporteren *gegevenssets*, Platform maakt een `.parquet` of `.json` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden de [succesvolle uitvoer van gegevenssets controleren](../../ui/export-datasets.md#verify) in de zelfstudie over exportgegevensbestanden.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verificatiegegevens {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Persoonlijke SSH-sleutel"
>abstract="De persoonlijke sleutel van SSH moet een RSA-Geformatteerd, Base64-Gecodeerde koord zijn, en moet niet wachtwoord-beschermd zijn."

Als u **[!UICONTROL SFTP with password]** verificatietype voor verbinding met uw SFTP-locatie:

![De bestemming SFTP basisauthentificatie met wachtwoord.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: Het adres van uw opslagplaats SFTP;
* **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
* **[!UICONTROL Port]**: De poort die wordt gebruikt door uw SFTP-opslaglocatie;
* **[!UICONTROL Password]**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Als u **[!UICONTROL SFTP with SSH key]** verificatietype voor verbinding met uw SFTP-locatie:

![SSH-sleutelverificatie voor SFTP-doel.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Vul het IP-adres of de domeinnaam van uw SFTP-account in
* **[!UICONTROL Port]**: De poort die wordt gebruikt door uw SFTP-opslaglocatie;
* **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
* **[!UICONTROL SSH Key]**: De persoonlijke SSH-sleutel die wordt gebruikt om u aan te melden bij uw SFTP-opslaglocatie. De persoonlijke sleutel moet een RSA-Geformatteerd, Base64-Gecodeerde koord zijn, en moet niet wachtwoord-beschermd zijn.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens {#destination-details}

Na het vestigen van de authentificatieverbinding aan de plaats SFTP, verstrek de volgende informatie voor de bestemming:

![De gebieden van de details van de bestemming voor de bestemming SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ga een naam in die u helpt deze bestemming in het gebruikersinterface van het Experience Platform identificeren;
* **[!UICONTROL Description]**: Voer een beschrijving in voor deze bestemming;
* **[!UICONTROL Folder path]**: Voer het pad in naar de map op de SFTP-locatie waar de bestanden worden geëxporteerd.
* **[!UICONTROL File type]**: Selecteer het Experience Platform voor de indeling die u voor de geëxporteerde bestanden wilt gebruiken. Wanneer u de [!UICONTROL CSV] kunt u [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Een [voorbeeldmanifestbestand](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) waarmee het geëxporteerde bestand is gegenereerd.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in de opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u de SFTP-opslag en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## IP adres lijst van gewenste personen {#ip-address-allow-list}

Zie de [IP adres lijst van gewenste personen](ip-address-allow-list.md) artikel als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.
