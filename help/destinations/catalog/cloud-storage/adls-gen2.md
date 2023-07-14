---
title: (Beta) Azure Data Lake Storage Gen2-verbinding
description: Leer hoe u verbinding maakt met Azure Data Lake Storage Gen2 om het publiek te activeren en gegevenssets te exporteren.
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# (bèta) [!DNL Azure Data Lake Storage Gen2] verbinding

>[!IMPORTANT]
>
>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Azure Data Lake Storage Gen2] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL Organization ID].

## Overzicht {#overview}

Lees deze pagina om te leren een live uitgaande verbinding met uw [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) gegevens uit het meer om periodiek gegevensbestanden uit Experience Platform te exporteren.

## Verbinding maken met uw [!DNL ADLS Gen2] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!DNL ADLS Gen2] opslaglocatie via de gebruikersinterface van het Platform, lees de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!DNL ADLS Gen2] opslagplaats programmatically, lees de [Activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Alle bestemmingen ondersteunen de activering van publiek dat door het Experience Platform wordt geproduceerd [Segmenteringsservice](../../../segmentation/home.md).

Bovendien ondersteunt deze bestemming ook de activering van het publiek dat in de onderstaande tabel wordt beschreven.

| Type publiek | Beschrijving |
---------|----------|
| Aangepaste uploads | Soorten publiek dat via CSV-bestanden in het Experience Platform wordt opgenomen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de toepasselijke schemavelden (bijvoorbeeld uw PPID), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](/help/destinations/ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL URL]**: Het eindpunt voor [!DNL Azure Data Lake Storage Gen2]. Het eindpuntpatroon is: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]**: De huurdersinformatie die uw toepassing bevat.
* **[!UICONTROL Service principal ID]**: De client-id van de toepassing.
* **[!UICONTROL Service principal key]**: De sleutel van de toepassing.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: Selecteer de indeling die het Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer u de [!UICONTROL CSV] kunt u ook [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Planning {#scheduling}

In de **[!UICONTROL Scheduling]** stap, u kunt [het exportschema instellen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Azure Data Lake Storage Gen2] doel en u kunt ook [de naam van uw geëxporteerde bestanden configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## (bètaversie) Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt datasetuitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Procedure [de uitvoer datasets gebruikend het gebruikersinterface van de Platform](/help/destinations/ui/export-datasets.md).
* Procedure [de uitvoer datasets programmatically gebruikend de Dienst API van de Stroom](/help/destinations/api/export-datasets.md).

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Azure Data Lake Storage Gen2] opslaan en ervoor zorgen dat de geëxporteerde bestanden de verwachte profielpopulaties bevatten.
