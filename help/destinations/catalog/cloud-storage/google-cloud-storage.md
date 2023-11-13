---
title: Google Cloud Storage-verbinding
description: Leer hoe u verbinding maakt met Google Cloud Storage en een publiek activeert of gegevenssets exporteert.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# [!DNL Google Cloud Storage] verbinding

## Overzicht {#overview}

Een live uitgaande verbinding maken met [!DNL Google Cloud Storage] om gegevensbestanden van Adobe Experience Platform regelmatig naar uw eigen emmers te exporteren.

## Verbinding maken met uw [!DNL Google Cloud Storage] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!DNL Google Cloud Storage] opslaglocatie via de gebruikersinterface van het platform, lees de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!DNL Google Cloud Storage] opslagplaats programmatically, lees de [Activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de toepasselijke schemavelden, zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vereiste instellingen voor verbinding met uw [!DNL Google Cloud Storage] account {#prerequisites}

Als u een verbinding wilt maken met Platform [!DNL Google Cloud Storage], moet u eerst interoperabiliteit voor uw [!DNL Google Cloud Storage] account. Voor toegang tot de interoperabiliteitsinstelling opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** van de **[!UICONTROL Cloud Storage]** in het navigatievenster.

![Google Cloud Platform-dashboard met Cloud Storage en Settings gemarkeerd.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

De **[!UICONTROL Settings]** wordt weergegeven. Hier kunt u informatie over uw [!DNL Google] project-id en details over uw [!DNL Google Cloud Storage] account. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperability]** in de bovenste koptekst.

![Het tabblad Interoperabiliteit wordt gemarkeerd op het dashboard voor het Google Cloud-platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

De **[!UICONTROL Interoperability]** De pagina bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw de dienstrekening. Als u een nieuwe toegangstoets-id en een geheime toegangssleutel voor uw serviceaccount wilt genereren, selecteert u **[!UICONTROL Create a Key for a Service Account]**.

![De sleutel voor een serviceaccountbesturingselement maken die is gemarkeerd in het dashboard voor het Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangstoets-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] account aan Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](/help/destinations/ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt voor het verifiëren van uw [!DNL Google Cloud Storage] account aan Platform. Voor informatie over het verkrijgen van deze waarde leest u de [voorwaarden](#prerequisites) hierboven.
* **[!UICONTROL Secret access key]**: Een tekenreeks van 40 tekens met de basiscode 64 die wordt gebruikt voor verificatie van uw [!DNL Google Cloud Storage] account aan Platform. Voor informatie over het verkrijgen van deze waarde leest u de [voorwaarden](#prerequisites) hierboven.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Voor meer informatie over deze waarden leest u de [HMAC-sleutels voor Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) hulplijn. Raadpleeg voor meer informatie over het genereren van uw eigen toegangstoets-id en geheime toegangstoets de [[!DNL Google Cloud Storage] bronoverzicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: Selecteer het Experience Platform voor de indeling die u voor de geëxporteerde bestanden wilt gebruiken. Wanneer u de [!UICONTROL CSV] kunt u [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Een [voorbeeldmanifestbestand](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) waarmee het geëxporteerde bestand is gegenereerd.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in de opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Planning

In de **[!UICONTROL Scheduling]** stap, u kunt [het exportschema instellen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Google Cloud Storage] doel en u kunt ook [de naam van uw geëxporteerde bestanden configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Procedure [de uitvoer datasets gebruikend het gebruikersinterface van het Platform](/help/destinations/ui/export-datasets.md).
* Procedure [de uitvoer datasets programmatically gebruikend de Dienst API van de Stroom](/help/destinations/api/export-datasets.md).

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Google Cloud Storage] emmertje en zorg ervoor dat de uitgevoerde dossiers de verwachte profielpopulaties bevatten.
