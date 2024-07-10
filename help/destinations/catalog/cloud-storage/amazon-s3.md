---
title: Amazon S3-verbinding
description: Creeer een levende uitgaande verbinding aan uw opslag van Amazon Web Services (AWS) S3 om CSV- gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# [!DNL Amazon S3] verbinding {#s3-connection}

## Doelwijziging {#changelog}

+++ Wijzigingen weergeven


| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Januari 2024 | Bijwerken van functionaliteit en documentatie | De Amazon S3 bestemmingsschakelaar steunt nu een nieuw verondersteld rolauthentificatietype. Lees meer over het onderwerp in de [verificatiesectie](#assumed-role-authentication). |
| Juli 2023 | Bijwerken van functionaliteit en documentatie | Met de release van het Experience Platform van juli 2023 [!DNL Amazon S3] doel biedt nieuwe functionaliteit, zoals hieronder wordt weergegeven: <br><ul><li>[Ondersteuning voor gegevensexport](/help/destinations/ui/export-datasets.md)</li><li>Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Mogelijkheid om de opmaak van geëxporteerde CSV-gegevensbestanden aan te passen](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Verbinding maken met uw [!DNL Amazon S3] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!DNL Amazon S3] opslaglocatie via de gebruikersinterface van het platform, lees de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!DNL Amazon S3] opslagplaats programmatically, lees de gids over hoe te [activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Op Amazon S3-profielen gebaseerd exporttype gemarkeerd in de UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

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
>id="platform_destinations_connect_s3_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**. De Amazon S3-bestemming ondersteunt twee verificatiemethoden:

* Toegangstoets en geheime sleutelverificatie
* Veronderstelde rolauthentificatie

#### Toegangstoets en geheime sleutelverificatie

Gebruik deze verificatiemethode als u de Amazon S3-toegangstoets en de geheime sleutel wilt invoeren, zodat Experience Platform gegevens kan exporteren naar uw Amazon S3-eigenschappen.

![Afbeelding van de vereiste velden bij het selecteren van de toegangstoets en de verificatie met de geheime sleutel.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]toegangstoets** en **[!DNL Amazon S3]geheime sleutel**: In [!DNL Amazon S3], een `access key - secret access key` paar om Platform toegang tot uw te verlenen [!DNL Amazon S3] account. Meer informatie in het dialoogvenster [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Veronderstelde rol {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Veronderstelde rolauthentificatie"
>abstract="Gebruik dit verificatietype als u accountsleutels en geheime sleutels niet met Adobe wilt delen. In plaats daarvan maakt Experience Platform verbinding met uw Amazon S3-locatie via op rollen gebaseerde toegang. Plak de ARN van de rol die u in AWS voor de Adobe gebruiker hebt gemaakt. Het patroon is vergelijkbaar met `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Afbeelding van de vereiste velden bij het selecteren van aangenomen rolverificatie.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Gebruik dit verificatietype als u accountsleutels en geheime sleutels niet met Adobe wilt delen. In plaats daarvan maakt Experience Platform verbinding met uw Amazon S3-locatie via op rollen gebaseerde toegang.

Om dit te doen, moet u in de console van AWS een veronderstelde gebruiker voor Adobe met [rechten vereist](#required-s3-permission) om naar uw Amazon S3 emmers te schrijven. Een **[!UICONTROL Trusted entity]** in AWS met de Adobe account **[!UICONTROL 670664943635]**. Raadpleeg voor meer informatie de [AWS-documentatie over het maken van rollen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: Plak de ARN van de rol die u in AWS voor de Adobe gebruiker hebt gemaakt. Het patroon is vergelijkbaar met `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Naam van emmertje"
>abstract="Moet tussen 3 en 63 tekens lang zijn. Moet beginnen en eindigen met een letter of cijfer. Moet alleen kleine letters, cijfers of afbreekstreepjes ( - ) bevatten. Mag niet als IP adres (bijvoorbeeld, 192.100.1.1) worden geformatteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Mappad"
>abstract="Moet alleen de tekens A-Z, a-z, 0-9 bevatten en mag de volgende speciale tekens bevatten: `/!-_.'()"^[]+$%.*"`. Als u een map per publieksbestand wilt maken, voegt u de macro in `/%SEGMENT_NAME%` of `/%SEGMENT_ID%` of `/%SEGMENT_NAME%/%SEGMENT_ID%` in het tekstveld. Macro&#39;s kunnen alleen aan het einde van het mappad worden ingevoegd. Macrovoorbeelden weergeven in de documentatie."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Macro&#39;s gebruiken om een map te maken op uw opslaglocatie"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van dit doel in.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: Selecteer het Experience Platform voor de indeling die u voor de geëxporteerde bestanden wilt gebruiken. Wanneer u de [!UICONTROL CSV] kunt u [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Een [voorbeeldmanifestbestand](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) waarmee het geëxporteerde bestand is gegenereerd.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in de opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

>[!TIP]
>
>In de Connect-doelworkflow kunt u per geëxporteerd publieksbestand een aangepaste map in uw Amazon S3-opslag maken. Lezen [Macro&#39;s gebruiken om een map te maken op uw opslaglocatie](overview.md#use-macros) voor instructies.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

### Vereist [!DNL Amazon S3] machtigingen {#required-s3-permission}

Om gegevens met succes te verbinden en uit te voeren aan uw [!DNL Amazon S3] opslaglocatie, een gebruiker voor Identiteit en Toegangsbeheer (IAM) maken [!DNL Platform] in [!DNL Amazon S3] en wijs toestemmingen voor de volgende acties toe:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Amazon S3] opslaan en ervoor zorgen dat de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## IP adres lijst van gewenste personen {#ip-address-allow-list}

Zie de [IP adres lijst van gewenste personen](ip-address-allow-list.md) artikel als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.