---
title: Amazon S3-verbinding
description: Creeer een levende uitgaande verbinding aan uw opslag van Amazon Web Services (AWS) S3 om CSV- gegevensdossiers van Adobe Experience Platform in uw eigen S3 emmers periodiek uit te voeren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# [!DNL Amazon S3]-verbinding {#s3-connection}

## Doelwijziging {#changelog}

+++ Wijzigingen weergeven


| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Januari 2024 | Bijwerken van functionaliteit en documentatie | De Amazon S3 bestemmingsschakelaar steunt nu een nieuw verondersteld rolauthentificatietype. Lees meer over het in de [&#x200B; authentificatiesectie &#x200B;](#assumed-role-authentication). |
| Juli 2023 | Bijwerken van functionaliteit en documentatie | Met de Experience Platform-release van juli 2023 biedt de [!DNL Amazon S3] -bestemming nieuwe functionaliteit, zoals hieronder wordt weergegeven: <br><ul><li>[&#x200B; de uitvoersteun van de Dataset &#x200B;](/help/destinations/ui/export-datasets.md)</li><li>Aanvullende [&#x200B; dossier noemende opties &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Mogelijkheid om de kopballen van het douanedossier in uw uitgevoerde dossiers via de [&#x200B; verbeterde toewijzingsstap &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te plaatsen.</li><li>[&#x200B; Mogelijkheid om het formatteren van uitgevoerde CSV gegevensdossiers &#x200B;](/help/destinations/ui/batch-destinations-file-formatting-options.md) aan te passen.</li></ul> |

{style="table-layout:auto"}

+++

## Verbinding maken met uw [!DNL Amazon S3] -opslag via API of UI {#connect-api-or-ui}

* Om met uw [!DNL Amazon S3] opslagplaats te verbinden gebruikend het gebruikersinterface van Experience Platform, lees de secties [&#x200B; verbinden met de bestemming &#x200B;](#connect) en [&#x200B; actief publiek aan deze bestemming &#x200B;](#activate) hieronder.
* Om met uw [!DNL Amazon S3] opslagplaats programmatically te verbinden, lees de gids op hoe te [&#x200B; publiek aan op dossier-gebaseerde bestemmingen activeren door de Dienst API van de Stroom te gebruiken leerprogramma &#x200B;](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![&#x200B; Amazon S3 op profiel-gebaseerd die uitvoertype in UU wordt benadrukt.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

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
>id="platform_destinations_connect_s3_rsa"
>title="Openbare RSA-sleutel"
>abstract="U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte sleutel in de documentatiekoppeling hieronder."

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** . De Amazon S3-bestemming ondersteunt twee verificatiemethoden:

* Toegangstoets en geheime sleutelverificatie
* Veronderstelde rolauthentificatie

#### Verificatie met S3 toegangstoets en geheime sleutel

Gebruik deze verificatiemethode als u de Amazon S3-toegangstoets en de geheime sleutel wilt invoeren, zodat Experience Platform gegevens kan exporteren naar uw Amazon S3-eigenschappen.

![&#x200B; Beeld van de vereiste gebieden wanneer het selecteren van toegangstoets en geheime zeer belangrijke authentificatie.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]access key** en **[!DNL Amazon S3]geheime sleutel**: in [!DNL Amazon S3] genereert u een `access key - secret access key` paar om Experience Platform toegang te verlenen tot uw [!DNL Amazon S3] account. Leer meer in de [&#x200B; documentatie van Amazon Web Services &#x200B;](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

  ![&#x200B; Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Authentificatie met S3 veronderstelde rol {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Veronderstelde rolauthentificatie"
>abstract="Gebruik dit verificatietype als u accountsleutels en geheime sleutels niet wilt delen met Adobe. Experience Platform maakt in plaats daarvan verbinding met uw Amazon S3-locatie via op rollen gebaseerde toegang. Plak de ARN van de rol die u in AWS voor de Adobe-gebruiker hebt gemaakt. Het patroon is vergelijkbaar met `arn:aws:iam::800873819705:role/destinations-role-customer` "

Gebruik dit verificatietype als u accountsleutels en geheime sleutels niet wilt delen met Adobe. Experience Platform maakt in plaats daarvan verbinding met uw Amazon S3-locatie via op rollen gebaseerde toegang.

![&#x200B; Beeld van de vereiste gebieden wanneer het selecteren van veronderstelde rolauthentificatie.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**: plak de ARN van de rol die u in AWS voor de Adobe-gebruiker hebt gemaakt. Het patroon is vergelijkbaar met `arn:aws:iam::800873819705:role/destinations-role-customer` . Zie de stappen hieronder voor gedetailleerde begeleiding op hoe te om S3 toegang correct te vormen.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.

Om dit te doen, moet u in de console van AWS een veronderstelde rol voor Adobe met het [&#x200B; recht vereiste toestemmingen &#x200B;](#minimum-permissions-iam-user) tot stand brengen om aan uw emmers van Amazon S3 te schrijven.

**creeer een beleid met de vereiste toestemmingen**

1. Open de AWS-console en ga naar IAM > Beleid > Beleid maken
2. Selecteer Beleidseditor > JSON en voeg de onderstaande machtigingen toe.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. Voer op de volgende pagina een naam in voor uw beleid en sla dit op ter referentie. In de volgende stap hebt u deze beleidsnaam nodig wanneer u de rol maakt.

**creeer gebruikersrol in uw S3 klantenrekening**

1. Open de AWS-console en ga naar IAM > Rollen > Nieuwe rol maken
2. Selecteer **Vertrouwd entiteitstype** > **AWS rekening**
3. Selecteer **een rekening van AWS** > **Een andere rekening van AWS** en ga Adobe rekeningidentiteitskaart in: `670664943635`
4. Machtigingen toevoegen met behulp van het eerder gemaakte beleid
5. Voer een rolnaam in (bijvoorbeeld `destinations-role-customer` ). De rolnaam moet vertrouwelijk worden behandeld, gelijkend op een wachtwoord. De tag kan maximaal 64 tekens lang zijn en kan alfanumerieke tekens en de volgende speciale tekens bevatten: `+=,.@-_` . Controleer vervolgens of:
   * De Adobe-account-id `670664943635` staat in de **[!UICONTROL Select trusted entities]** -sectie
   * Het eerder gemaakte beleid is aanwezig in **[!UICONTROL Permissions policy summary]**

**verstrek de rol voor Adobe om** te veronderstellen

Nadat u de rol in AWS hebt gemaakt, moet u de rol ARN aan Adobe geven. De ARN volgt dit patroon: `arn:aws:iam::800873819705:role/destinations-role-customer`

U kunt de ARN op de hoofdpagina vinden nadat u de rol in de AWS-console hebt gemaakt. U zult dit ARN gebruiken wanneer het creëren van de bestemming.

**verifieer roltoestemmingen en vertrouwensverhoudingen**

Zorg ervoor dat uw rol de volgende configuratie heeft:

* **Toestemmingen**: De rol zou toestemmingen moeten hebben om tot S3 toegang te hebben (of volledige toegang of de minimale toestemmingen die in **worden verstrekt leiden tot een beleid met de vereiste toestemmingen** stap hierboven)
* **Vertrouwensverhoudingen**: De rol zou de rekening van wortelAdobe (`670664943635`) in zijn vertrouwensverhoudingen moeten hebben

**Alternatief: Beperk tot specifieke gebruiker van Adobe (Facultatief)**

Als u liever niet het volledige Adobe-account toestaat, kunt u de toegang beperken tot alleen de specifieke Adobe-gebruiker. Om dit te doen, geef het vertrouwensbeleid met de volgende configuratie uit:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

Voor meer informatie, verwijs naar de [&#x200B; documentatie van AWS bij het creëren van rollen &#x200B;](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).



### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Naam van emmertje"
>abstract="Moet tussen 3 en 63 tekens lang zijn. Moet beginnen en eindigen met een letter of cijfer. Moet alleen kleine letters, cijfers of afbreekstreepjes ( - ) bevatten. Mag niet als IP adres (bijvoorbeeld, 192.100.1.1) worden geformatteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Mappad"
>abstract="Moet alleen de tekens A-Z, a-z, 0-9 bevatten en mag de volgende speciale tekens bevatten: `/!-_.'()"^[]+$%.*"` . Als u een map per publieksbestand wilt maken, voegt u de macro `/%SEGMENT_NAME%` of `/%SEGMENT_ID%` of `/%SEGMENT_NAME%/%SEGMENT_ID%` in het tekstveld in. Macro&#39;s kunnen alleen aan het einde van het mappad worden ingevoegd. Macrovoorbeelden weergeven in de documentatie."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=nl-NL#use-macros" text="Macro&#39;s gebruiken om een map te maken op uw opslaglocatie"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt bij het identificeren van dit doel.
* **[!UICONTROL Description]**: voer een beschrijving van dit doel in.
* **[!UICONTROL Bucket name]**: voer de naam in van het [!DNL Amazon S3] emmertje dat door dit doel moet worden gebruikt.
* **[!UICONTROL Folder path]**: voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: selecteer de indeling die Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer het selecteren van de [!UICONTROL CSV] optie, kunt u ook [&#x200B; de dossier het formatteren opties &#x200B;](../../ui/batch-destinations-file-formatting-options.md) vormen.
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Bekijk a [&#x200B; steekproef manifestdossier &#x200B;](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [&#x200B; dataflow looppas &#x200B;](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die het uitgevoerde dossier produceerde.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in uw opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

>[!TIP]
>
>In de Connect-doelworkflow kunt u per geëxporteerd publieksbestand een aangepaste map in uw Amazon S3-opslag maken. Lees [&#x200B; de macro&#39;s van het Gebruik om een omslag in uw opslagplaats &#x200B;](overview.md#use-macros) voor instructies tot stand te brengen.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Vereiste [!DNL Amazon S3] machtigingen {#required-s3-permission}

Als u gegevens wilt verbinden en exporteren naar uw [!DNL Amazon S3] -opslaglocatie, maakt u een gebruiker voor Identiteit en Toegangsbeheer (IAM) voor [!DNL Experience Platform] in [!DNL Amazon S3] en wijst u machtigingen toe voor de volgende handelingen:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Minimale vereiste toestemmingen voor IAM veronderstelde rolauthentificatie {#minimum-permissions-iam-user}

Wanneer het vormen van de rol IAM als klant, zorg ervoor dat het toestemmingsbeleid verbonden aan de rol de vereiste acties aan de doelomslag in het emmertje en de `s3:ListBucket` actie voor de wortel van het emmertje omvat. De mening onder een voorbeeld van het minimumtoestemmingenbeleid voor dit authentificatietype:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u de [!DNL Amazon S3] -opslag en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## IP adres lijst van gewenste personen {#ip-address-allow-list}

Verwijs naar het [&#x200B; artikel van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;als u Adobe IPs aan een lijst van gewenste personen moet toevoegen.](ip-address-allow-list.md)