---
title: Google Cloud Storage-verbinding
description: Leer hoe u verbinding maakt met Google Cloud Storage en een publiek activeert of gegevenssets exporteert.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# [!DNL Google Cloud Storage] verbinding

## Overzicht {#overview}

Maak een live uitgaande verbinding met [!DNL Google Cloud Storage] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen emmers te exporteren.

## Verbinding maken met uw [!DNL Google Cloud Storage] -opslag via API of UI {#connect-api-or-ui}

* Om met uw [!DNL Google Cloud Storage] opslagplaats te verbinden gebruikend het gebruikersinterface van Experience Platform, lees de secties [&#x200B; verbinden met de bestemming &#x200B;](#connect) en [&#x200B; actief publiek aan deze bestemming &#x200B;](#activate) hieronder.
* Om met uw [!DNL Google Cloud Storage] opslagplaats programmatically te verbinden, lees [&#x200B; actief publiek aan op dossier-gebaseerde bestemmingen door de dienst API van de Stroom te gebruiken leerprogramma &#x200B;](../../api/activate-segments-file-based-destinations.md).

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
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de toepasselijke schemagebieden, zoals gekozen in het uitgezochte scherm van profielattributen van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Hoe te [&#x200B; datasets uitvoeren gebruikend het gebruikersinterface van Experience Platform &#x200B;](/help/destinations/ui/export-datasets.md).
* Hoe te [&#x200B; datasets programmatically uitvoeren gebruikend de Dienst API van de Stroom &#x200B;](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Wanneer het uitvoeren van *publieksgegevens*, leidt Experience Platform tot een `.csv`, `parquet`, of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [&#x200B; gesteunde dossierformaten voor de uitvoer &#x200B;](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) sectie in het leerprogramma van de publiekactivering.

Wanneer het uitvoeren van *datasets*, leidt Experience Platform tot een `.parquet` of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [&#x200B; succesvolle datasetuitvoer &#x200B;](../../ui/export-datasets.md#verify) sectie in het de uitvoerdatasetleerprogramma verifiëren.

## Vereiste instellingen voor verbinding met uw [!DNL Google Cloud Storage] -account {#prerequisites}

Als u Experience Platform wilt verbinden met [!DNL Google Cloud Storage] , moet u eerst interoperabiliteit inschakelen voor uw [!DNL Google Cloud Storage] -account. Als u de instelling voor interoperabiliteit wilt openen, opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** in de optie **[!UICONTROL Cloud Storage]** in het navigatievenster.

![&#x200B; het dashboard van het Platform van Google Cloud met de benadrukte Opslag en Montages van de Wolk.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

De pagina **[!UICONTROL Settings]** wordt weergegeven. Hier vindt u informatie over uw [!DNL Google] project-id en informatie over uw [!DNL Google Cloud Storage] -account. Selecteer **[!UICONTROL Interoperability]** in de bovenste koptekst voor toegang tot de instellingen voor interoperabiliteit.

![&#x200B; het lusje van Interoperabiliteit dat in het dashboard van het Platform van de Wolk van Google wordt benadrukt.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

De pagina **[!UICONTROL Interoperability]** bevat informatie over verificatie, toegangstoetsen en het standaardproject dat aan uw serviceaccount is gekoppeld. Selecteer **[!UICONTROL Create a Key for a Service Account]** om een nieuwe toegangs sleutel-id en een geheime toegangssleutel voor uw serviceaccount te genereren.

![&#x200B; creeer een sleutel voor een controle van de de dienstrekening die in het dashboard van het Platform van de Wolk van Google wordt benadrukt.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangs sleutel-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] -account aan te sluiten op Experience Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](/help/destinations/ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Access key ID]**: Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. Voor informatie over hoe te om deze waarde te verkrijgen, lees de [&#x200B; eerste vereisten &#x200B;](#prerequisites) hierboven sectie.
* **[!UICONTROL Secret access key]**: Een tekenreeks met een basiscode van 40 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. Voor informatie over hoe te om deze waarde te verkrijgen, lees de [&#x200B; eerste vereisten &#x200B;](#prerequisites) hierboven sectie.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![&#x200B; Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont &#x200B;](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Voor meer informatie over deze waarden, lees de [&#x200B; de sleutels van HMAC van de Opslag van de Wolk van Google HMAC &#x200B;](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) gids. Voor stappen op hoe te om uw eigen toegangs zeer belangrijke identiteitskaart en geheime toegangssleutel te produceren, verwijs naar het [[!DNL Google Cloud Storage]  bronoverzicht &#x200B;](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Bucket name]**: voer de naam in van het [!DNL Google Cloud Storage] emmertje dat door dit doel moet worden gebruikt.
* **[!UICONTROL Folder path]**: voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
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

### Vereiste [!DNL Google Cloud Storage] machtigingen {#required-google-cloud-storage-permission}

Als u gegevens met succes wilt verbinden en exporteren naar de opslaglocatie van [!DNL Google Cloud Storage] , hebt u de volgende [!DNL Google Cloud Storage] -machtigingen voor uw emmers nodig:

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

Lees meer over [&#x200B; toegangsbeheer en toestemmingen &#x200B;](https://cloud.google.com/storage/docs/access-control/iam-permissions) in [!DNL Google Cloud Storage].

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Planning

In de **[!UICONTROL Scheduling]** stap, kunt u [&#x200B; opstelling het uitvoerprogramma &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Google Cloud Storage] bestemming en u kunt ook [&#x200B; de naam van uw uitgevoerde dossiers &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) vormen.

### Kenmerken en identiteiten toewijzen {#map}

In de stap **[!UICONTROL Mapping]** kunt u selecteren welke kenmerk- en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie, bekijk de [&#x200B; toewijzingsstap &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in de activerende partijbestemmingen UI leerprogramma.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u het emmertje van [!DNL Google Cloud Storage] en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## IP adres lijst van gewenste personen {#ip-address-allow-list}

Verwijs naar het [&#128279;](ip-address-allow-list.md) artikel van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.