---
title: (bèta) Datasets exporteren naar Cloud Storage-doelen
type: Tutorial
description: Leer hoe u gegevenssets van Adobe Experience Platform naar de gewenste locatie voor cloudopslag exporteert.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 6627953aba4f1cd665c3d5c4bc8711c48064374f
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 0%

---

# (bèta) Gegevenssets exporteren naar cloudopslagbestemmingen

>[!IMPORTANT]
>
>* De functionaliteit om datasets uit te voeren is momenteel in Bèta en niet beschikbaar aan alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.
>* Deze bètafunctionaliteit ondersteunt de export van gegevens van de eerste generatie, zoals gedefinieerd in de Real-time Customer Data Platform [productbeschrijving](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP-pakket Premier en Ultimate hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

In dit artikel wordt uitgelegd welke workflow nodig is om te exporteren [gegevenssets](/help/catalog/datasets/overview.md) van Adobe Experience Platform naar uw voorkeurslocatie voor cloudopslag, zoals [!DNL Amazon S3], SFTP-locaties, of [!DNL Google Cloud Storage] door het Experience Platform UI te gebruiken.

U kunt de Experience Platform APIs ook gebruiken om datasets uit te voeren. Lees de [API-zelfstudie voor exporteren](/help/destinations/api/export-datasets.md) voor meer informatie .

## Ondersteunde doelen {#supported-destinations}

Momenteel, kunt u datasets naar de bestemmingen van de wolkenopslag uitvoeren die in het schermafbeelding worden benadrukt en hieronder worden vermeld.

![Doelen die de uitvoer van gegevenssets ondersteunen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Wanneer moet u het publiek activeren of gegevenssets exporteren {#when-to-activate-audiences-or-activate-datasets}

Sommige op dossier-gebaseerde bestemmingen in de catalogus van het Experience Platform steunen zowel publieksactivering als dataset de uitvoer.

* U kunt doelgroepen activeren als u uw gegevens wilt indelen in profielen die zijn gegroepeerd op belangen of kwalificaties van het publiek.
* U kunt ook gegevenssets exporteren overwegen wanneer u onbewerkte gegevenssets wilt exporteren. Deze zijn niet gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. U kunt deze gegevens gebruiken voor rapportage, workflows voor gegevenswetenschap, om te voldoen aan de compatibiliteitseisen en vele andere gebruiksgevallen.

Dit document bevat alle informatie die nodig is om gegevenssets te exporteren. Als u het publiek wilt activeren naar cloudopslag of marketingdoelen via e-mail, leest u [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md).

## Vereisten {#prerequisites}

Om datasets naar de bestemmingen van de cloudopslag uit te voeren, moet u met succes hebben [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

### Vereiste machtigingen {#permissions}

Om datasets uit te voeren, hebt u nodig **[!UICONTROL Manage Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om datasets uit te voeren en dat de bestemming het uitvoeren van datasets steunt, doorblader de bestemmingscatalogus. Als een doel een **[!UICONTROL Activate]** of een **[!UICONTROL Export datasets]** controle, dan hebt u de aangewezen toestemmingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus met besturingselement Catalogus gemarkeerd.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate]** of **[!UICONTROL Export datasets]** op de kaart die aan de bestemming beantwoordt dat u datasets naar wilt uitvoeren.

   ![Tabblad Doelcatalogus met besturingselement Activeren gemarkeerd.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Selecteren **[!UICONTROL Data type Datasets]** en selecteer de bestemmingsverbinding u datasets naar wilt uitvoeren, dan selecteren **[!UICONTROL Next]**.

>[!TIP]
> 
>Als u een nieuwe bestemming wilt instellen om gegevenssets te exporteren, selecteert u **[!UICONTROL Configure new destination]** om de [Verbinden met doel](/help/destinations/ui/connect-destination.md) workflow.

![Workflow voor doelactivering met Datasets-besturingselement gemarkeerd.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. De **[!UICONTROL Select datasets]** wordt weergegeven. Ga naar de volgende sectie tot [uw gegevenssets selecteren](#select-datasets) voor uitvoer.

## Uw gegevenssets selecteren {#select-datasets}

Gebruik de controlevakjes links van de datasetnamen om de datasets te selecteren die u naar de bestemming wilt uitvoeren, dan selecteren **[!UICONTROL Next]**.

![De de uitvoerwerkschema van de gegevensset die de Uitgezochte datasetstap tonen waar u kunt selecteren welke datasets aan uitvoer.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Gegevensexport voor schema {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Exportopties voor bestanden voor gegevenssets"
>abstract="Selecteren **Incrementele bestanden exporteren** alleen de gegevens exporteren die sinds de laatste export aan de gegevensset zijn toegevoegd. <br> De eerste incrementele bestandsuitvoer bevat alle gegevens in de gegevensset, die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de gegevens die sinds de eerste export aan de gegevensset zijn toegevoegd."

In de **[!UICONTROL Scheduling]** stap, kunt u een begindatum en een uitvoerkadentie voor uw datasetuitvoer plaatsen.

De **[!UICONTROL Export incremental files]** wordt automatisch geselecteerd. Dit leidt tot de uitvoer waar het eerste dossier een volledige momentopname van de dataset is en de verdere dossiers zijn stijgende toevoegingen aan de dataset sinds de vorige uitvoer.

>[!IMPORTANT]
>
>Het eerste geëxporteerde incrementele bestand bevat alle bestaande gegevens in de gegevensset, die als backfill werken.

![Workflow voor het exporteren van gegevenssets met de planningsstap.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Gebruik de **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: Plan het incrementele bestand eenmaal per dag, elke dag, op het opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: Plan het incrementele bestand om de 3, 6, 8 of 12 uur.

2. Gebruik de **[!UICONTROL Time]** om de tijd van de dag te kiezen, in [!DNL UTC] formaat, wanneer het exporteren moet plaatsvinden.

3. Gebruik de **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. In de bètaversie van de functie is het niet mogelijk een einddatum voor de exportbewerking in te stellen. Voor meer informatie bekijkt u de [bekende beperkingen](#known-limitations) sectie.

4. Selecteren **[!UICONTROL Next]** om het programma op te slaan en door te gaan naar de **[!UICONTROL Review]** stap.

>[!NOTE]
> 
>Voor het exporteren van gegevenssets hebben de bestandsnamen een vooraf ingestelde standaardindeling, die niet kan worden gewijzigd. Zie de sectie [Controleren of gegevensset is geëxporteerd](#verify) voor meer informatie en voorbeelden van geëxporteerde bestanden.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en begonnen datasets aan de bestemming te exporteren.

![Workflow voor het exporteren van gegevenssets met de revisiestap.](/help/destinations/assets/ui/export-datasets/review.png)

## Controleren of gegevensset is geëxporteerd {#verify}

Bij het exporteren van gegevenssets maakt Experience Platform een `.json` of `.parquet` in de opslaglocatie die u hebt opgegeven. Verwacht dat een nieuw bestand op uw opslaglocatie wordt gedeponeerd volgens het exportschema dat u hebt opgegeven.

Experience Platform leidt tot een omslagstructuur in de opslagplaats u specificeerde, waar het de uitgevoerde datasetdossiers bewaart. Voor elke exporttijd wordt een nieuwe map gemaakt volgens het onderstaande patroon:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

De standaardbestandsnaam wordt willekeurig gegenereerd en zorgt ervoor dat geëxporteerde bestandsnamen uniek zijn.

### Voorbeeldgegevenssetbestanden {#sample-files}

De aanwezigheid van deze bestanden op uw opslaglocatie is een bevestiging van een geslaagde export. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u een voorbeeld downloaden [.parquet-bestand](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) of [.json-bestand](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Gecomprimeerde gegevensbestanden {#compressed-dataset-files}

In de [verbinding maken met doelworkflow](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), kunt u de geëxporteerde gegevenssetbestanden selecteren die u wilt comprimeren, zoals hieronder wordt weergegeven:

![Het type van dossier en compressieselectie wanneer het verbinden met een bestemming om datasets uit te voeren.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Houd rekening met het verschil in bestandsindeling tussen de twee bestandstypen bij het comprimeren:

* Bij het exporteren van gecomprimeerde JSON-bestanden is de geëxporteerde bestandsindeling `json.gz`
* Bij het exporteren van gecomprimeerde parketbestanden is de geëxporteerde bestandsindeling `gz.parquet`

## Gegevensset verwijderen van bestemming {#remove-dataset}

Om een dataset uit een bestaande gegevensstroom te verwijderen, volg de stappen hieronder:

1. Aanmelden bij de [UI EXPERIENCE PLATFORM](https://experience.adobe.com/platform/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteren **[!UICONTROL Browse]** van de hoogste kopbal om uw bestaande bestemmingsgegevens te bekijken.

   ![De bestemming bladert mening met een getoonde bestemmingsverbinding en de rest vaag uit.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Filterpictogram selecteren ![Filter-pictogram](../assets/ui/edit-activation/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

1. Van de **[!UICONTROL Activation data]** kolom, selecteer de datasetcontrole om alle datasets te bekijken die aan dit de uitvoerdataflow in kaart worden gebracht.

   ![De beschikbare gegevenssetnavigatieoptie die in de kolom van de Gegevens van de Activering wordt benadrukt.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. De **[!UICONTROL Activation data]** wordt de pagina voor het doel weergegeven. Selecteren **[!UICONTROL Remove dataset]** in het rechterspoor om het dialoogvenster voor het bevestigen van gegevenssets te openen.

   ![Verwijder de dialoog van de dataset die de Remove datasetcontrole in de juiste spoorlijn toont.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Selecteer in het bevestigingsdialoogvenster de optie **[!UICONTROL Remove]** om de dataset van uitvoer aan de bestemming onmiddellijk te verwijderen.

   ![Dialoogvenster dat de bevestigingsoptie van de datasetverwijdering van dataflow toont.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Bekende beperkingen {#known-limitations}

Houd rekening met de volgende beperkingen voor de bètaversie van het exporteren van gegevenssets:

* Er is momenteel één machtiging (**[!UICONTROL Manage and Activate Dataset Destinations]**) die het beheren en activeren van toestemmingen op datasetbestemmingen omvat. Deze controles zullen in de toekomst in meer korrelige toestemmingen worden verdeeld. Controleer de [vereiste machtigingen](#permissions) sectie voor een volledige lijst van toestemmingen die u datasets moet uitvoeren.
* Momenteel, kunt u stijgende dossiers slechts uitvoeren en een einddatum kan niet voor uw datasetuitvoer worden geselecteerd.
* Geëxporteerde bestandsnamen kunnen momenteel niet worden aangepast.
* UI blokkeert momenteel niet u van het schrappen van een dataset die naar een bestemming wordt uitgevoerd. Verwijder geen datasets die naar bestemmingen worden geëxporteerd. [De gegevensset verwijderen](#remove-dataset) van een doelgegevensstroom alvorens het te schrappen.
* De metriek van de controle voor de uitvoer van datasets wordt momenteel gemengd met aantallen voor profieluitvoer zodat weerspiegelen zij niet de ware uitvoeraantallen.
