---
title: Datasets exporteren naar cloudopslagdoelen
type: Tutorial
description: Leer hoe u gegevenssets van Adobe Experience Platform naar de gewenste locatie voor cloudopslag exporteert.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 938e4875318f07b296fc884487ca1c664be659ef
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 0%

---

# Gegevenssets exporteren naar cloudopslagbestemmingen

>[!AVAILABILITY]
>
>* Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP Premiere of Ultimate-pakket, Adobe Journey Optimizer of Customer Journey Analytics hebben aangeschaft. Neem contact op met uw Adobe voor meer informatie.

Dit artikel verklaart het werkschema dat wordt vereist om [ datasets ](/help/catalog/datasets/overview.md) van Adobe Experience Platform naar uw aangewezen plaats van de wolkenopslag, zoals [!DNL Amazon S3], plaatsen SFTP, of [!DNL Google Cloud Storage] uit te voeren door het Experience Platform UI te gebruiken.

U kunt de Experience Platform APIs ook gebruiken om datasets uit te voeren. Lees de [ leerprogramma&#39;s van de uitvoerdatasets API ](/help/destinations/api/export-datasets.md) voor meer informatie.

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
    <td><ul><li>De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de Experience Platform UI na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Schakelaar van Gegevens van de Analyse, en Audience Manager worden gecreeerd.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets"> systeem-geproduceerde dataset van de Momentopname van het Profiel </a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Eerste</td>
    <td>Raadpleeg de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> documentatie van Adobe Journey Optimizer </a> .</td>
  </tr>
  <tr>
    <td>Ultieme</td>
    <td>Raadpleeg de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> documentatie van Adobe Journey Optimizer </a> .</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Alles</td>
    <td> De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de Experience Platform UI na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Schakelaar van Gegevens van de Analyse, en Audience Manager worden gecreeerd.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Distiller-gegevens (invoegtoepassing)</td>
    <td>Voortgekomen datasets die door de Dienst van de Vraag worden gecreeerd.</td>
  </tr>
</tbody>
</table>

## Videotutorial {#video-tutorial}

Bekijk de onderstaande video voor een end-to-end uitleg van de workflow die op deze pagina wordt beschreven, de voordelen van het gebruik van de functie voor het exporteren van gegevenssets en enkele gebruiksscenario&#39;s.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Ondersteunde doelen {#supported-destinations}

Momenteel, kunt u datasets naar de bestemmingen van de wolkenopslag uitvoeren die in het schermafbeelding worden benadrukt en hieronder worden vermeld.

![ de cataloguspagina die van Doelen toont welke bestemmingen dataset uitvoeren steunen.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

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

Dit document bevat alle informatie die nodig is om gegevenssets te exporteren. Als u *publiek* aan cloudopslag of e-mail marketing bestemmingen wilt activeren, lees [ publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) activeren.

## Vereisten {#prerequisites}

Om datasets naar de bestemmingen van de wolkenopslag uit te voeren, moet u met succes [ verbonden aan een bestemming ](./connect-destination.md) hebben. Als u dit niet reeds hebt gedaan, ga naar de [ bestemmingscatalogus ](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

### Vereiste machtigingen {#permissions}

Om datasets uit te voeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL View Datasets]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om datasets uit te voeren en dat de bestemming het uitvoeren van datasets steunt, doorblader de bestemmingscatalogus. Als een doel een **[!UICONTROL Activate]** - of **[!UICONTROL Export datasets]** -besturingselement heeft, hebt u de juiste machtigingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![ de cataloguslusje van de Bestemming met benadrukte controle van de Catalogus.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate]** of **[!UICONTROL Export datasets]** op de kaart die overeenkomt met het doel waarnaar u gegevenssets wilt exporteren.

   ![ de cataloguslusje van de Bestemming met Activate benadrukte controle.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Selecteer **[!UICONTROL Data type Datasets]** en selecteer de doelverbinding waarnaar u gegevenssets wilt exporteren, en selecteer vervolgens **[!UICONTROL Next]** .

>[!TIP]
> 
>Als u opstelling een nieuwe bestemming wilt om datasets uit te voeren, uitgezocht **[!UICONTROL Configure new destination]** om [ te teweegbrengen verbind met bestemmings ](/help/destinations/ui/connect-destination.md) werkschema.

![ benadrukt de activeringswerkschema van de Bestemming met de controle van Datasets.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. De weergave **[!UICONTROL Select datasets]** wordt weergegeven. Ga aan de volgende sectie te werk aan [ selecteer uw datasets ](#select-datasets) voor de uitvoer.

## Uw gegevenssets selecteren {#select-datasets}

Gebruik de controlevakjes links van de datasetnamen om de datasets te selecteren die u naar de bestemming wilt uitvoeren, dan uitgezocht **[!UICONTROL Next]**.

![ de uitvoerwerkschema die van de Dataset de Uitgezochte datasetstap tonen waar u kunt selecteren welke datasets om uit te voeren.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Gegevensexport voor schema {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Exportopties voor bestanden voor gegevenssets"
>abstract="Selecteer **de stijgende dossiers van de Uitvoer** om slechts de gegevens uit te voeren die aan de dataset sinds de laatste uitvoer werden toegevoegd. <br> De eerste incrementele bestandsuitvoer bevat alle gegevens in de gegevensset, die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de gegevens die sinds de eerste export aan de gegevensset zijn toegevoegd."

In de stap **[!UICONTROL Scheduling]** kunt u een begindatum en een exportinterface instellen voor het exporteren van uw gegevensset.

De optie **[!UICONTROL Export incremental files]** wordt automatisch geselecteerd. Dit brengt de uitvoer van één of veelvoudige dossiers teweeg die een volledige momentopname van de dataset vertegenwoordigen. De volgende dossiers zijn stijgende toevoegingen aan de dataset sinds de vorige uitvoer.

>[!IMPORTANT]
>
>De eerste incrementele bestandsuitvoer bevat alle bestaande gegevens in de dataset, die als backfill werken. Het exporteren kan een of meerdere bestanden bevatten.

![ de uitvoerwerkschema die van de Dataset de het plannen stap tonen.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Gebruik de kiezer **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: Plan de incrementele bestandsexport eenmaal per dag, elke dag, op het opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: Plan het incrementele bestand om de 3, 6, 8 of 12 uur.

2. Gebruik de kiezer van **[!UICONTROL Time]** om in [!DNL UTC] -indeling de tijd van de dag te kiezen waarop het exporteren moet plaatsvinden.

3. Gebruik de kiezer van **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. U kunt momenteel geen einddatum instellen voor het exporteren. Voor meer informatie, bekijk de [ bekende beperkingen ](#known-limitations) sectie.

4. Selecteer **[!UICONTROL Next]** om het schema op te slaan en door te gaan naar de stap **[!UICONTROL Review]** .

>[!NOTE]
> 
>Voor het exporteren van gegevenssets hebben de bestandsnamen een vooraf ingestelde standaardindeling, die niet kan worden gewijzigd. Zie de sectie [ de succesvolle uitvoer van de dataset ](#verify) voor meer informatie en voorbeelden van uitgevoerde dossiers verifiëren.

## Controleren {#review}

Op de pagina **[!UICONTROL Review]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en datasets aan de bestemming te beginnen uitvoeren.

![ de uitvoerworkflow die van de Dataset de overzichtsstap toont.](/help/destinations/assets/ui/export-datasets/review.png)

## Controleren of gegevensset is geëxporteerd {#verify}

Bij het exporteren van gegevenssets maakt Experience Platform een of meerdere `.json` - of `.parquet` -bestanden op de opslaglocatie die u hebt opgegeven. Nieuwe bestanden worden naar verwachting op uw opslaglocatie gedeponeerd volgens het exportschema dat u hebt opgegeven.

Experience Platform leidt tot een omslagstructuur in de opslagplaats u specificeerde, waar het de uitgevoerde datasetdossiers bewaart. Voor elke exporttijd wordt een nieuwe map gemaakt volgens het onderstaande patroon:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

De standaardbestandsnaam wordt willekeurig gegenereerd en zorgt ervoor dat geëxporteerde bestandsnamen uniek zijn.

### Voorbeeldgegevenssetbestanden {#sample-files}

De aanwezigheid van deze bestanden op uw opslaglocatie is een bevestiging van een geslaagde export. Om te begrijpen hoe de uitgevoerde dossiers gestructureerd zijn, kunt u een steekproef [.parquet dossier ](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) of [ .json dossier ](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json) downloaden.

#### Gecomprimeerde gegevensbestanden {#compressed-dataset-files}

In [ verbind met bestemmingswerkschema ](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), kunt u de uitgevoerde datasetdossiers selecteren om worden samengeperst, zoals hieronder getoond:

![ het type van Dossier en compressieselectie wanneer het verbinden met een bestemming om datasets uit te voeren.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Houd rekening met het verschil in bestandsindeling tussen de twee bestandstypen bij het comprimeren:

* Bij het exporteren van gecomprimeerde JSON-bestanden is de geëxporteerde bestandsindeling `json.gz`
* Bij het exporteren van gecomprimeerde parketbestanden is de geëxporteerde bestandsindeling `gz.parquet`

## Gegevenssets verwijderen uit doelen {#remove-dataset}

Om datasets uit een bestaande gegevensstroom te verwijderen, volg de stappen hieronder:

1. Login aan het [ Experience Platform UI ](https://experience.adobe.com/platform/) en selecteert **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Browse]** in de bovenste koptekst om de bestaande doelgegevens weer te geven.

   ![ doorbladert de Bestemming mening met een getoonde bestemmingsverbinding en de rest vervaagd uit.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Selecteer het filterpictogram ![ filter-pictogram ](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

2. Van de **[!UICONTROL Activation data]** kolom, selecteer de datasetcontrole om alle datasets te bekijken die aan dit de uitvoerdataflow in kaart worden gebracht.

   ![ de beschikbare optie van de datasetnavigatie die in de kolom van de Gegevens van de Activering wordt benadrukt.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. [!BADGE  Beta ] de **[!UICONTROL Activation data]** pagina voor de bestemming verschijnt. Gebruik de selectievakjes aan de linkerkant van de lijst met gegevenssets om de gegevenssets te selecteren die u wilt verwijderen en selecteer vervolgens **[!UICONTROL Remove datasets]** in de rechterrail om het dialoogvenster voor het bevestigen van gegevenssets te openen.

   >[!NOTE]
   >Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen.

   ![ verwijder datasetdialoog die de Remove datasetcontrole in het juiste spoor toont.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. Selecteer in het bevestigingsdialoogvenster **[!UICONTROL Remove]** om de gegevensset direct te verwijderen uit het exporteren naar het doel.

   ![ Dialoog die de bevestigingsoptie van de datasetverwijdering van dataflow toont.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Uitvoerrechten gegevensset {#licensing-entitlement}

Raadpleeg de productbeschrijvingsdocumenten om te begrijpen hoeveel gegevens u per jaar voor elke Experience Platform-toepassing mag exporteren. Bijvoorbeeld, kunt u de Beschrijving van het Product van Real-Time CDP [ hier ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) bekijken.

De gegevensuitvoerrechten voor verschillende aanvragen zijn niet additief. Dit betekent bijvoorbeeld dat als u Real-Time CDP Ultimate en Adobe Journey Optimizer Ultimate koopt, de uitvoerrechten voor profielen de hoogste van de twee rechten zijn, zoals beschreven in de productbeschrijvingen. Uw volumeregelingen worden berekend door het totale aantal gelicentieerde profielen te nemen en te vermenigvuldigen met 500 kB voor Real-Time CDP Premium of 700 kB voor Real-Time CDP Ultimate om te bepalen hoeveel gegevensvolume u hebt.

Anderzijds, als u toe:voegen-ons zoals Gegevens Distiller kocht, vertegenwoordigt de grens van de gegevensuitvoer die u gerechtigd bent om te zijn de som van de productrij en de toe:voegen-op.

U kunt uw profielexport bekijken en volgen op basis van uw contractuele limieten in het licentiedashboard.

## Bekende beperkingen {#known-limitations}

Houd in mening de volgende beperkingen voor de algemene beschikbaarheidsversie van de uitvoer van datasets:

* Momenteel, kunt u stijgende dossiers slechts uitvoeren en een einddatum kan niet voor uw datasetuitvoer worden geselecteerd.
* Geëxporteerde bestandsnamen kunnen momenteel niet worden aangepast.
* Datasets die via API zijn gemaakt, zijn momenteel niet beschikbaar voor export.
* UI blokkeert momenteel niet u van het schrappen van een dataset die naar een bestemming wordt uitgevoerd. Verwijder geen datasets die naar bestemmingen worden geëxporteerd. [ verwijder de dataset ](#remove-dataset) uit een bestemmingsdataflow alvorens het te schrappen.
* De metriek van de controle voor de uitvoer van datasets wordt momenteel gemengd met aantallen voor profieluitvoer zodat weerspiegelen zij niet de ware uitvoeraantallen.
* Gegevens met een tijdstempel die ouder is dan 365 dagen, worden niet geëxporteerd voor gegevenssets. Voor meer informatie, bekijk de [ gidsen voor de geplande uitvoer van datasets ](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)
