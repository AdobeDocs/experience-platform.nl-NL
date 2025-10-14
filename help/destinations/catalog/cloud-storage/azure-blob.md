---
title: Azure Blob-verbinding
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om regelmatig CSV-gegevensbestanden uit Adobe Experience Platform te exporteren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# [!DNL Azure Blob] verbinding

## Doelwijziging {#changelog}

Met de Experience Platform-release van juli 2023 biedt de [!DNL Azure Blob] -bestemming nieuwe functionaliteit, zoals hieronder wordt weergegeven:

* [&#x200B; de uitvoersteun van de Dataset &#x200B;](/help/destinations/ui/export-datasets.md).
* Aanvullende [&#x200B; dossier noemende opties &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Mogelijkheid om de kopballen van het douanedossier in uw uitgevoerde dossiers via de [&#x200B; verbeterde toewijzingsstap &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te plaatsen.
* [&#x200B; Mogelijkheid om het formatteren van uitgevoerde CSV gegevensdossiers &#x200B;](/help/destinations/ui/batch-destinations-file-formatting-options.md) aan te passen.

## Overzicht {#overview}

[!DNL Azure Blob] (hierna [!DNL Blob] genoemd) is een Microsoft-oplossing voor objectopslag voor de cloud. Deze zelfstudie bevat stappen voor het maken van een [!DNL Blob] -doel met behulp van de gebruikersinterface van [!DNL Experience Platform] .

## Verbinding maken met uw [!UICONTROL Azure Blob] -opslag via API of UI {#connect-api-or-ui}

* Om met uw [!UICONTROL Azure Blob] opslagplaats te verbinden gebruikend het gebruikersinterface van Experience Platform, lees de secties [&#x200B; verbinden met de bestemming &#x200B;](#connect) en [&#x200B; actief publiek aan deze bestemming &#x200B;](#activate) hieronder.
* Om met uw [!UICONTROL Azure Blob] opslagplaats programmatically te verbinden, lees [&#x200B; actief publiek aan op dossier-gebaseerde bestemmingen door de dienst API van de Stroom te gebruiken leerprogramma &#x200B;](../../api/activate-segments-file-based-destinations.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Blob] bestemming hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; activerend publiek aan uw bestemming &#x200B;](../../ui/activate-batch-profile-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Hoe te [&#x200B; datasets uitvoeren gebruikend het gebruikersinterface van Experience Platform &#x200B;](/help/destinations/ui/export-datasets.md).
* Hoe te [&#x200B; datasets programmatically uitvoeren gebruikend de Dienst API van de Stroom &#x200B;](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Wanneer het uitvoeren van *publieksgegevens*, leidt Experience Platform tot een `.csv`, `parquet`, of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [&#x200B; gesteunde dossierformaten voor de uitvoer &#x200B;](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) sectie in het leerprogramma van de publiekactivering.

Wanneer het uitvoeren van *datasets*, leidt Experience Platform tot een `.parquet` of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [&#x200B; succesvolle datasetuitvoer &#x200B;](../../ui/export-datasets.md#verify) sectie in het de uitvoerdatasetleerprogramma verifiëren.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Connection string]**: de verbindingstekenreeks is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de [!DNL Blob] verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` .
   * Voor meer informatie over het vormen van uw [!DNL Blob] verbindingskoord, zie [&#x200B; een verbindingskoord voor een Azure opslagrekening &#x200B;](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in de documentatie van Microsoft vormen.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![&#x200B; Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont &#x200B;](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt bij het identificeren van dit doel.
* **[!UICONTROL Description]**: voer een beschrijving van dit doel in.
* **[!UICONTROL Folder path]**: voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Container]**: voer de naam in van de [!DNL Azure Blob Storage] -container die door dit doel moet worden gebruikt.
* **[!UICONTROL File type]**: selecteer de indeling die Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer het selecteren van de [!UICONTROL CSV] optie, kunt u ook [&#x200B; de dossier het formatteren opties &#x200B;](../../ui/batch-destinations-file-formatting-options.md) vormen.
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Bekijk a [&#x200B; steekproef manifestdossier &#x200B;](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [&#x200B; dataflow looppas &#x200B;](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die het uitgevoerde dossier produceerde.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in uw opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u de [!DNL Azure Blob] -opslag en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.