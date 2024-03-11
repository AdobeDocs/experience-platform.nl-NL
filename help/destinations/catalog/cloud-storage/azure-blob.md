---
title: Azure Blob-verbinding
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om regelmatig CSV-gegevensbestanden uit Adobe Experience Platform te exporteren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# [!DNL Azure Blob] verbinding

## Doelwijziging {#changelog}

Met de release van het Experience Platform van juli 2023 [!DNL Azure Blob] doel biedt nieuwe functionaliteit, zoals hieronder wordt weergegeven:

* [Ondersteuning voor gegevensexport](/help/destinations/ui/export-datasets.md).
* Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Mogelijkheid om de opmaak van geëxporteerde CSV-gegevensbestanden aan te passen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Overzicht {#overview}

[!DNL Azure Blob] (hierna [!DNL Blob]) is Microsoft-oplossing voor objectopslag voor de cloud. Deze zelfstudie bevat stappen voor het maken van een [!DNL Blob] doel met behulp van [!DNL Platform] gebruikersinterface.

## Verbinding maken met uw [!UICONTROL Azure Blob] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!UICONTROL Azure Blob] opslaglocatie via de gebruikersinterface van het platform, lees de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!UICONTROL Azure Blob] opslagplaats programmatically, lees de [Activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL Blob] doel, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [publiek activeren op uw bestemming](../../ui/activate-batch-profile-destinations.md).

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

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Connection string]**: de verbindingstekenreeks is vereist voor toegang tot gegevens in de blob-opslag. De [!DNL Blob] patroon verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Voor meer informatie over het configureren van uw [!DNL Blob] verbindingstekenreeks, zie [Een verbindingstekenreeks configureren voor een Azure-opslagaccount](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in de documentatie van Microsoft.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van dit doel in.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Container]**: Voer de naam in van de [!DNL Azure Blob Storage] container die door deze bestemming moet worden gebruikt.
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
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Azure Blob] opslaan en ervoor zorgen dat de geëxporteerde bestanden de verwachte profielpopulaties bevatten.