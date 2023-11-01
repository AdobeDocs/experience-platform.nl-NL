---
title: Datasets exporteren naar cloudopslagdoelen
type: Tutorial
description: Leer hoe u gegevenssets van Adobe Experience Platform naar de gewenste locatie voor cloudopslag exporteert.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# Gegevenssets exporteren naar cloudopslagbestemmingen

>[!AVAILABILITY]
>
>* Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP Premiere of Ultimate-pakket, Adobe Journey Optimizer of Customer Journey Analytics hebben aangeschaft. Neem contact op met uw Adobe voor meer informatie.

In dit artikel wordt uitgelegd welke workflow nodig is om te exporteren [gegevenssets](/help/catalog/datasets/overview.md) van Adobe Experience Platform naar uw voorkeurslocatie voor cloudopslag, zoals [!DNL Amazon S3], SFTP-locaties, of [!DNL Google Cloud Storage] door het Experience Platform UI te gebruiken.

U kunt de Experience Platform APIs ook gebruiken om datasets uit te voeren. Lees de [API-zelfstudie voor exporteren](/help/destinations/api/export-datasets.md) voor meer informatie .

## Beschikbare gegevensbestanden voor exporteren {#datasets-to-export}

De gegevenssets die u kunt exporteren, variëren op basis van de toepassing van het Experience Platform (Real-Time CDP, Adobe Journey Optimizer), de laag (Premier of Ultimate) en alle invoegtoepassingen die u hebt aangeschaft (bijvoorbeeld Data Distiller).

Begrijp van de lijst hieronder welke datasettypes u afhankelijk van uw toepassing, productrij, en om het even welke gekochte toe:voegen-ons kunt uitvoeren:

<table>
<thead>
  <tr>
    <th>Toepassing/invoegtoepassing</th>
    <th>Tier</th>
    <th>Beschikbare gegevens voor exporteren</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Eerste</td>
    <td>De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de Experience Platform UI na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Schakelaar van Gegevens van de Analyse, en Audience Manager worden gecreeerd.</td>
  </tr>
  <tr>
    <td>Ultieme</td>
    <td><ul><li>De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de Experience Platform UI na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Schakelaar van Gegevens van de Analyse, en Audience Manager worden gecreeerd.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Gegevensset voor door het systeem gegenereerde profielmomentopname</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Eerste</td>
    <td>Zie de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentatie.</td>
  </tr>
  <tr>
    <td>Ultieme</td>
    <td>Zie de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentatie.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Distiller-gegevens (invoegtoepassing)</td>
    <td>Voortgekomen datasets die door de Dienst van de Vraag worden gecreeerd.</td>
  </tr>
</tbody>
</table>

## Ondersteunde doelen {#supported-destinations}

Momenteel, kunt u datasets naar de bestemmingen van de wolkenopslag uitvoeren die in het schermafbeelding worden benadrukt en hieronder worden vermeld.

![Doelen die de uitvoer van gegevenssets ondersteunen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Wanneer moet u het publiek activeren of gegevenssets exporteren {#when-to-activate-audiences-or-activate-datasets}

Sommige op dossier-gebaseerde bestemmingen in de catalogus van het Experience Platform steunen zowel publieksactivering als dataset de uitvoer.

* U kunt doelgroepen activeren als u uw gegevens wilt indelen in profielen die zijn gegroepeerd op belangen of kwalificaties van het publiek.
* U kunt ook gegevenssets exporteren overwegen wanneer u onbewerkte gegevenssets wilt exporteren. Deze zijn niet gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. U kunt deze gegevens gebruiken voor rapportage, workflows voor gegevenswetenschap en vele andere gebruiksgevallen. Bijvoorbeeld, als beheerder, gegevensingenieur, of analist, kunt u gegevens van Experience Platform uitvoeren om met uw gegevenspakhuis te synchroniseren, gebruik in de analysehulpmiddelen van BI, externe wolkenhulpmiddelen van XML, of opslag in uw systeem voor de opslagbehoeften op lange termijn.

Dit document bevat alle informatie die nodig is om gegevenssets te exporteren. Als u *publiek* naar cloudopslag- of e-mailmarketingbestemmingen, lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md).

## Vereisten {#prerequisites}

Om datasets naar de bestemmingen van de cloudopslag uit te voeren, moet u met succes hebben [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

### Vereiste machtigingen {#permissions}

Om datasets uit te voeren, hebt u nodig **[!UICONTROL View Destinations]**, **[!UICONTROL View Datasets]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

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

3. Gebruik de **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. U kunt momenteel geen einddatum instellen voor het exporteren. Voor meer informatie bekijkt u de [bekende beperkingen](#known-limitations) sectie.

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


## Uitvoerrechten gegevensset {#licensing-entitlement}

Raadpleeg de productbeschrijvingsdocumenten om te begrijpen hoeveel gegevens u per jaar voor elke Experience Platform-toepassing mag exporteren. U kunt bijvoorbeeld de Real-Time CDP-productbeschrijving bekijken [hier](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

De gegevensuitvoerrechten voor verschillende aanvragen zijn niet additief. Dit betekent bijvoorbeeld dat als u Real-Time CDP Ultimate en Adobe Journey Optimizer Ultimate koopt, de uitvoerrechten voor profielen de hoogste van de twee rechten zijn, zoals beschreven in de productbeschrijvingen. Uw volumeregelingen worden berekend door het totale aantal gelicentieerde profielen te nemen en te vermenigvuldigen met 500 kB voor Real-Time CDP Premium of 700 kB voor Real-Time CDP Ultimate om te bepalen hoeveel gegevensvolume u hebt.

Anderzijds, als u toe:voegen-ons zoals Gegevens Distiller koopt, vertegenwoordigt de grens van de gegevensuitvoer die u gerechtigd bent om de som van de productrij en de toe:voegen-op te stellen.

U kunt uw profielexport bekijken en volgen op basis van uw contractuele limieten in het licentiedashboard.

## Bekende beperkingen {#known-limitations}

Houd in mening de volgende beperkingen voor de algemene beschikbaarheidsversie van de uitvoer van datasets:

* Momenteel, kunt u stijgende dossiers slechts uitvoeren en een einddatum kan niet voor uw datasetuitvoer worden geselecteerd.
* Geëxporteerde bestandsnamen kunnen momenteel niet worden aangepast.
* Datasets die via API zijn gemaakt, zijn momenteel niet beschikbaar voor export.
* UI blokkeert momenteel niet u van het schrappen van een dataset die naar een bestemming wordt uitgevoerd. Verwijder geen datasets die naar bestemmingen worden geëxporteerd. [De gegevensset verwijderen](#remove-dataset) van een doelgegevensstroom alvorens het te schrappen.
* De metriek van de controle voor de uitvoer van datasets wordt momenteel gemengd met aantallen voor profieluitvoer zodat weerspiegelen zij niet de ware uitvoeraantallen.
