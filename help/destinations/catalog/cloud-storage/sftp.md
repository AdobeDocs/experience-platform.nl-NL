---
title: SFTP-verbinding
description: Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 45f22addbff9ec81d64e9e756e4c27e8af4b477d
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 0%

---

# SFTP-verbinding

## Doelwijziging {#changelog}

Met de versie van Experience Platform van juli 2023, verstrekt de bestemming SFTP nieuwe functionaliteit, zoals hieronder vermeld:

* [ de uitvoersteun van de Dataset ](/help/destinations/ui/export-datasets.md).
* Aanvullende [ dossier noemende opties ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Mogelijkheid om de kopballen van het douanedossier in uw uitgevoerde dossiers via de [ verbeterde toewijzingsstap ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te plaatsen.
* [ Mogelijkheid om het formatteren van uitgevoerde CSV gegevensdossiers ](/help/destinations/ui/batch-destinations-file-formatting-options.md) aan te passen.

## Overzicht {#overview}

Maak een live uitgaande verbinding met uw SFTP-server om gescheiden gegevensbestanden periodiek vanuit Adobe Experience Platform te exporteren.

>[!IMPORTANT]
>
> Hoewel Experience Platform gegevensexport naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens [!DNL Amazon S3] en [!DNL Azure Blob] .

## Verbinding maken met SFTP via API of UI {#connect-api-or-ui}

* Om met uw opslagplaats van SFTP te verbinden gebruikend het gebruikersinterface van Experience Platform, lees de secties [ verbinden met de bestemming ](#connect) en [ actief publiek aan deze bestemming ](#activate) hieronder.
* Om met uw opslagplaats van SFTP programmatically te verbinden, lees [ actief publiek aan op dossier-gebaseerde bestemmingen door de dienst API van de Stroom te gebruiken leerprogramma ](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![ SFTP op profiel-gebaseerd die uitvoertype in de bestemmingscatalogus wordt benadrukt.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Hoe te [ datasets uitvoeren gebruikend het gebruikersinterface van Experience Platform ](/help/destinations/ui/export-datasets.md).
* Hoe te [ datasets programmatically uitvoeren gebruikend de Dienst API van de Stroom ](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Wanneer het uitvoeren van *publieksgegevens*, leidt Experience Platform tot een `.csv`, `parquet`, of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [ gesteunde dossierformaten voor de uitvoer ](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) sectie in het leerprogramma van de publiekactivering.

Wanneer het uitvoeren van *datasets*, leidt Experience Platform tot een `.parquet` of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [ succesvolle datasetuitvoer ](../../ui/export-datasets.md#verify) sectie in het de uitvoerdatasetleerprogramma verifiëren.

## Vereisten voor SFTP-serververbinding {#sftp-connection-requirements}

Om ervoor te zorgen dat gegevens succesvol worden geëxporteerd, moet u uw doel-SFTP-server configureren om een voldoende aantal gelijktijdige verbindingen toe te staan. Als uw server SFTP het aantal gelijktijdige verbindingen beperkt, kunt u de mislukkingen van de uitvoerbaan ervaren, vooral wanneer het uitvoeren van veelvoudige publiek of datasets tezelfdertijd.

**Aanbeveling**
Voor optimale prestaties, zou uw server SFTP minstens één gezamenlijke verbinding voor elk publiek of dataset moeten toestaan die worden uitgevoerd. De server moet minimaal 30% ondersteunen van het totale aantal soorten publiek of gegevenssets die tegelijkertijd worden geëxporteerd.

**Voorbeeld**\
Als u de uitvoer voor 100 publiek of datasets gelijktijdig plant, zou uw server SFTP minstens 30 gezamenlijke verbindingen moeten toestaan.

Als u de verbindingslimieten van uw SFTP-server correct configureert, voorkomt u mislukte exportbewerkingen en bent u zeker van betrouwbare gegevenslevering vanuit Adobe Experience Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verificatiegegevens {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Persoonlijke SSH-sleutel"
>abstract="De persoonlijke sleutel van SSH moet een RSA-Geformatteerd, Base64-Gecodeerde koord zijn, en moet niet wachtwoord-beschermd zijn."

Als u het verificatietype **[!UICONTROL SFTP with password]** selecteert om verbinding te maken met uw SFTP-locatie:

![ de bestemmingsbasisauthentificatie van SFTP met wachtwoord.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: het adres van uw opslagplaats SFTP;
* **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
* **[!UICONTROL Port]**: de poort die wordt gebruikt door de opslaglocatie van uw SFTP;
* **[!UICONTROL Password]**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![ Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Als u het verificatietype **[!UICONTROL SFTP with SSH key]** selecteert om verbinding te maken met uw SFTP-locatie:

![ de belangrijkste authentificatie van bestemmingsSSH van SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: vul het IP-adres of de domeinnaam van uw SFTP-account in
* **[!UICONTROL Port]**: de poort die wordt gebruikt door de opslaglocatie van uw SFTP;
* **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
* **[!UICONTROL SSH Key]**: De persoonlijke SSH-sleutel die wordt gebruikt om u aan te melden bij uw SFTP-opslaglocatie. De persoonlijke sleutel moet een RSA-Geformatteerd, Base64-Gecodeerde koord zijn, en moet niet wachtwoord-beschermd zijn.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![ Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens {#destination-details}

Na het vestigen van de authentificatieverbinding aan de plaats SFTP, verstrek de volgende informatie voor de bestemming:

![ de detailvelden van de Bestemming voor de bestemming SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: voer een naam in waarmee u deze bestemming in de Experience Platform-gebruikersinterface kunt identificeren.
* **[!UICONTROL Description]**: voer een beschrijving in voor dit doel;
* **[!UICONTROL Folder path]**: voer het pad in naar de map op de SFTP-locatie waar de bestanden worden geëxporteerd.
* **[!UICONTROL File type]**: selecteer de indeling die Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer het selecteren van de [!UICONTROL CSV] optie, kunt u ook [ de dossier het formatteren opties ](../../ui/batch-destinations-file-formatting-options.md) vormen.
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Bekijk a [ steekproef manifestdossier ](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [ dataflow looppas ](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die het uitgevoerde dossier produceerde.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in uw opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u de SFTP-opslag en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## IP adres lijst van gewenste personen {#ip-address-allow-list}

Verwijs naar het [&#128279;](ip-address-allow-list.md) artikel van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.
