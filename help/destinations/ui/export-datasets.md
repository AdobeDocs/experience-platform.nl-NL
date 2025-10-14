---
title: Datasets exporteren naar cloudopslagdoelen
type: Tutorial
description: Leer hoe u gegevenssets van Adobe Experience Platform naar de gewenste locatie voor cloudopslag exporteert.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 69a1ae08fefebb7fed54564ed06f42af523d2903
workflow-type: tm+mt
source-wordcount: '2656'
ht-degree: 0%

---

# Gegevenssets exporteren naar cloudopslagbestemmingen

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP Prime- of Ultimate-pakket, Adobe Journey Optimizer of Customer Journey Analytics hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

>[!IMPORTANT]
>
>**het punt van de Actie**: De [&#x200B; versie van September 2024 van Experience Platform &#x200B;](/help/release-notes/latest/latest.md#destinations) introduceerde de optie om een `endTime` datum voor de gegevens van de uitvoerdataset te plaatsen. Adobe heeft ook een standaardeinddatum van 1 september 2025 voor alle gegevens van de datasetuitvoer gecreeerd *vóór 1 November, 2024* geïntroduceerd.
>
>Voor om het even welke dataflows, moet u de einddatum in dataflow manueel bijwerken vóór de einddatum, anders zal uw uitvoer op die datum ophouden. Gebruik de gebruikersinterface van Experience Platform om te bekijken welke dataflows op 1 september 2025 worden ingesteld.
>
>Verwijs naar [&#x200B; het plannen sectie &#x200B;](#scheduling) voor informatie over hoe te om de einddatum van een dataset uit te geven uitvoerdataflow.

Dit artikel verklaart het werkschema dat wordt vereist om [&#x200B; datasets &#x200B;](/help/catalog/datasets/overview.md) van Adobe Experience Platform naar uw aangewezen plaats van de wolkenopslag, zoals [!DNL Amazon S3], plaatsen SFTP, of [!DNL Google Cloud Storage] uit te voeren door Experience Platform UI te gebruiken.

U kunt de Experience Platform API&#39;s ook gebruiken om gegevenssets te exporteren. Lees de [&#x200B; leerprogramma&#39;s van de uitvoerdatasets API &#x200B;](/help/destinations/api/export-datasets.md) voor meer informatie.

## Beschikbare gegevensbestanden voor exporteren {#datasets-to-export}

De gegevenssets die u kunt exporteren, variëren op basis van de Experience Platform-toepassing (Real-Time CDP, Adobe Journey Optimizer), de laag (Prime of Ultimate) en alle invoegtoepassingen die u hebt aangeschaft (bijvoorbeeld Data Distiller).

Gebruik de onderstaande tabel om te begrijpen welke gegevenstypen u kunt exporteren, afhankelijk van uw toepassing, productlaag en eventuele aangeschafte invoegtoepassingen:

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
    <td>Prime</td>
    <td>De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de UI van Experience Platform na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Verbinding van Gegevens van Analytics, en Audience Manager worden gecreeerd.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de UI van Experience Platform na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Verbinding van Gegevens van Analytics, en Audience Manager worden gecreeerd.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=nl-NL#profile-attribute-datasets"> systeem-geproduceerde dataset van de Momentopname van het Profiel </a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Raadpleeg de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html?lang=nl-NL#datasets"> documentatie van Adobe Journey Optimizer </a> .</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Raadpleeg de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html?lang=nl-NL#datasets"> documentatie van Adobe Journey Optimizer </a> .</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Alles</td>
    <td> De datasets van de Gebeurtenis van het profiel en van de Ervaring die in de UI van Experience Platform na het opnemen van of het verzamelen van gegevens door Bronnen, Web SDK, Mobiele SDK, de Verbinding van Gegevens van Analytics, en Audience Manager worden gecreeerd.</td>
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

>[!VIDEO](https://video.tv.adobe.com/v/3448824?captions=dut)

## Ondersteunde doelen {#supported-destinations}

Momenteel, kunt u datasets naar de bestemmingen van de wolkenopslag uitvoeren die in het schermafbeelding worden benadrukt en hieronder worden vermeld.

![&#x200B; de cataloguspagina die van Doelen toont welke bestemmingen dataset uitvoeren steunen.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Wanneer moet u het publiek activeren of gegevenssets exporteren {#when-to-activate-audiences-or-activate-datasets}

Sommige op dossier-gebaseerde bestemmingen in de catalogus van Experience Platform steunen zowel publieksactivering als de uitvoer van datasets.

* U kunt doelgroepen activeren als u uw gegevens wilt indelen in profielen die zijn gegroepeerd op belangen of kwalificaties van het publiek.
* U kunt ook gegevenssets exporteren overwegen wanneer u onbewerkte gegevenssets wilt exporteren. Deze zijn niet gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. U kunt deze gegevens gebruiken voor rapportage, workflows voor gegevenswetenschap en vele andere gebruiksgevallen. Bijvoorbeeld, als beheerder, gegevensingenieur, of analist, kunt u gegevens van Experience Platform uitvoeren om met uw gegevenspakhuis te synchroniseren, in de analysehulpmiddelen van BI, externe wolkenhulpmiddelen van XML, of opslag in uw systeem voor de opslagbehoeften op lange termijn te gebruiken.

Dit document bevat alle informatie die nodig is om gegevenssets te exporteren. Als u *publiek* aan cloudopslag of e-mail marketing bestemmingen wilt activeren, lees [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) activeren.

## Vereisten {#prerequisites}

Neem nota van de volgende voorwaarden om datasets uit te voeren:

* Om datasets naar de bestemmingen van de wolkenopslag uit te voeren, moet u met succes [&#x200B; verbonden aan een bestemming &#x200B;](./connect-destination.md) hebben. Als u dit niet reeds hebt gedaan, ga naar de [&#x200B; bestemmingscatalogus &#x200B;](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.
* De datasets van het profiel moeten voor gebruik in het Profiel van de Klant in real time worden toegelaten. [&#x200B; las meer &#x200B;](/help/ingestion/tutorials/ingest-batch-data.md#enable-for-profile) over hoe te om deze optie toe te laten.

### Vereiste machtigingen {#permissions}

Om datasets uit te voeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL View Datasets]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om datasets uit te voeren en dat de bestemming het uitvoeren van datasets steunt, doorblader de bestemmingscatalogus. Als een doel een **[!UICONTROL Activate]** - of **[!UICONTROL Export datasets]** -besturingselement heeft, hebt u de juiste machtigingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![&#x200B; de cataloguslusje van de Bestemming met benadrukte controle van de Catalogus.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate]** of **[!UICONTROL Export datasets]** op de kaart die overeenkomt met het doel waarnaar u gegevenssets wilt exporteren.

   ![&#x200B; de cataloguslusje van de Bestemming met Activate benadrukte controle.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Selecteer **[!UICONTROL Data type Datasets]** en selecteer de doelverbinding waarnaar u gegevenssets wilt exporteren, en selecteer vervolgens **[!UICONTROL Next]** .

>[!TIP]
> 
>Als u opstelling een nieuwe bestemming wilt om datasets uit te voeren, uitgezocht **[!UICONTROL Configure new destination]** om [&#x200B; te teweegbrengen verbind met bestemmings &#x200B;](/help/destinations/ui/connect-destination.md) werkschema.

![&#x200B; benadrukt de activeringswerkschema van de Bestemming met de controle van Datasets.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. De weergave **[!UICONTROL Select datasets]** wordt weergegeven. Ga aan de volgende sectie te werk aan [&#x200B; selecteer uw datasets &#x200B;](#select-datasets) voor de uitvoer.

## Uw gegevenssets selecteren {#select-datasets}

Gebruik de controlevakjes links van de datasetnamen om de datasets te selecteren die u naar de bestemming wilt uitvoeren, dan uitgezocht **[!UICONTROL Next]**.

![&#x200B; de uitvoerwerkschema die van de Dataset de Uitgezochte datasetstap tonen waar u kunt selecteren welke datasets om uit te voeren.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Gegevensexport voor schema {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Exportopties voor bestanden voor gegevenssets"
>abstract="Selecteer **de stijgende dossiers van de Uitvoer** om slechts de gegevens uit te voeren die aan de dataset sinds de laatste uitvoer werden toegevoegd. <br> De eerste incrementele bestandsuitvoer bevat alle gegevens in de gegevensset, die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de gegevens die sinds de eerste export aan de gegevensset zijn toegevoegd. <br> Uitgezochte **Uitvoer volledige dossiers** om het volledige lidmaatschap van elke dataset op elke uitvoer uit te voeren. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="De einddatum voor deze gegevensstroom bijwerken"
>abstract="De einddatum voor deze gegevensstroom bijwerken"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="De einddatum voor deze gegevensstroominhoud bijwerken"
>abstract="Vanwege recente updates voor deze bestemming is voor de gegevensstroom nu een einddatum vereist. Adobe heeft een standaardeinddatum ingesteld op 1 september 2025. Werk de gegevens bij naar de gewenste einddatum. Anders worden de gegevens niet meer geëxporteerd op de standaarddatum."

Met de stap **[!UICONTROL Scheduling]** kunt u:

* Plaats een begindatum en een einddatum, evenals een uitvoerkadentie voor uw datasetuitvoer.
* Vorm als de uitgevoerde datasetdossiers het volledige lidmaatschap van de dataset of enkel stijgende veranderingen in het lidmaatschap op elk uitvoervoorval zouden moeten uitvoeren.
* Pas het mappad aan in uw opslaglocatie waar gegevenssets moeten worden geëxporteerd. Lees meer over hoe te [&#x200B; de weg van de uitvoeromslag &#x200B;](#edit-folder-path) uitgeven.

Gebruik het besturingselement **[!UICONTROL Edit schedule]** op de pagina om de exportsnelheid van exportbewerkingen te bewerken en om te bepalen of volledige of incrementele bestanden moeten worden geëxporteerd.

![&#x200B; geeft programmacontrole uit die in de Plannende stap wordt benadrukt.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

De optie **[!UICONTROL Export incremental files]** is standaard geselecteerd. Dit brengt de uitvoer van één of veelvoudige dossiers teweeg die een volledige momentopname van de dataset vertegenwoordigen. De volgende dossiers zijn stijgende toevoegingen aan de dataset sinds de vorige uitvoer. U kunt ook **[!UICONTROL Export full files]** selecteren. Selecteer in dit geval de frequentie **[!UICONTROL Once]** voor een eenmalige volledige uitvoer van de dataset.

>[!IMPORTANT]
>
>De eerste incrementele bestandsuitvoer bevat alle bestaande gegevens in de dataset, die als backfill werken. Het exporteren kan een of meerdere bestanden bevatten.

![&#x200B; de uitvoerwerkschema die van de Dataset de het plannen stap tonen.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Gebruik de kiezer **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: Plan de incrementele bestandsexport eenmaal per dag, elke dag, op het opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: Plan het incrementele bestand om de 3, 6, 8 of 12 uur.

2. Gebruik de kiezer van **[!UICONTROL Time]** om in [!DNL UTC] -indeling de tijd van de dag te kiezen waarop het exporteren moet plaatsvinden.

3. Gebruik de kiezer van **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden.

4. Selecteer **[!UICONTROL Save]** om het schema op te slaan en door te gaan naar de stap **[!UICONTROL Review]** .

>[!NOTE]
> 
>Voor het exporteren van gegevenssets hebben de bestandsnamen een vooraf ingestelde standaardindeling, die niet kan worden gewijzigd. Zie de sectie [&#x200B; de succesvolle uitvoer van de dataset &#x200B;](#verify) voor meer informatie en voorbeelden van uitgevoerde dossiers verifiëren.

## Mappad bewerken {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Mappad bewerken"
>abstract="Gebruik verschillende beschikbare macro&#39;s om het mappad aan te passen waarin de gegevensset wordt geëxporteerd."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Padvoorvertoning gegevensmap"
>abstract="Bekijk een voorvertoning van de mapstructuur die op uw opslaglocatie wordt gemaakt op basis van de macro&#39;s die u in dit venster hebt toegevoegd."

Selecteer **[!UICONTROL Edit folder path]** om de mappenstructuur in uw opslagplaats aan te passen waar de uitgevoerde datasets worden gedeponeerd.

![&#x200B; geeft de controle van de omslagweg uit die in de het plannen stap wordt benadrukt.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

U kunt verschillende beschikbare macro&#39;s gebruiken om een gewenste mapnaam aan te passen. Dubbelklik op een macro om deze toe te voegen aan het mappad en gebruik `/` tussen de macro&#39;s om de mappen te scheiden.

![&#x200B; de selectie van Macro&#39;s die in het modale venster van de douanemap wordt benadrukt.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

Nadat u de gewenste macro&#39;s hebt geselecteerd, ziet u een voorvertoning van de mapstructuur die op uw opslaglocatie wordt gemaakt. Het eerste niveau in de omslagstructuur vertegenwoordigt **[!UICONTROL Folder path]** dat u wanneer u [&#x200B; met de bestemming &#x200B;](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) verbond om datasets uit te voeren.

![&#x200B; Voorproef van omslagweg die in het modale venster van de douaneomslag wordt benadrukt.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

## Controleren {#review}

Op de pagina **[!UICONTROL Review]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en datasets aan de bestemming te beginnen uitvoeren.

![&#x200B; de uitvoerworkflow die van de Dataset de overzichtsstap toont.](/help/destinations/assets/ui/export-datasets/review.png)

## Controleren of gegevensset is geëxporteerd {#verify}

Bij het exporteren van gegevenssets maakt Experience Platform een of meerdere `.json` - of `.parquet` -bestanden op de opslaglocatie die u hebt opgegeven. Nieuwe bestanden worden naar verwachting op uw opslaglocatie gedeponeerd volgens het exportschema dat u hebt opgegeven.

Experience Platform maakt een mappenstructuur op de opslaglocatie die u hebt opgegeven, waar de geëxporteerde gegevenssetbestanden worden opgeslagen. Het standaard patroon van de omslaguitvoer wordt hieronder getoond, maar u kunt [&#x200B; de omslagstructuur met uw aangewezen macro&#39;s &#x200B;](#edit-folder-path) aanpassen.

>[!TIP]
> 
>Het eerste niveau in deze omslagstructuur - `folder-name-you-provided` - vertegenwoordigt **[!UICONTROL Folder path]** die u wanneer u [&#x200B; met de bestemming &#x200B;](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) verbonden om datasets uit te voeren.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

De standaardbestandsnaam wordt willekeurig gegenereerd en zorgt ervoor dat geëxporteerde bestandsnamen uniek zijn.

### Voorbeeldgegevenssetbestanden {#sample-files}

De aanwezigheid van deze bestanden op uw opslaglocatie is een bevestiging van een geslaagde export. Om te begrijpen hoe de uitgevoerde dossiers gestructureerd zijn, kunt u een steekproef [.parquet dossier &#x200B;](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) of [&#x200B; .json dossier &#x200B;](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json) downloaden.

#### Gecomprimeerde gegevensbestanden {#compressed-dataset-files}

In [&#x200B; verbind met bestemmingswerkschema &#x200B;](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), kunt u de uitgevoerde datasetdossiers selecteren om worden samengeperst, zoals hieronder getoond:

![&#x200B; het type van Dossier en compressieselectie wanneer het verbinden met een bestemming om datasets uit te voeren.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Houd rekening met het verschil in bestandsindeling tussen de twee bestandstypen bij het comprimeren:

* Bij het exporteren van gecomprimeerde JSON-bestanden heeft de geëxporteerde bestandsindeling de waarde `json.gz` . De indeling van de geëxporteerde JSON is NDJSON, de standaardindeling voor gegevensuitwisseling in het ecosysteem big data. Adobe raadt u aan een NDJSON-compatibele client te gebruiken om de geëxporteerde bestanden te lezen.
* Bij het exporteren van gecomprimeerde parketbestanden is de geëxporteerde bestandsindeling `gz.parquet`

De uitvoer naar JSON- dossiers wordt gesteund *op een samengeperste slechts wijze*. Exporteren naar Parquet-bestanden wordt ondersteund in een gecomprimeerde en niet-gecomprimeerde modus.

## Gegevenssets verwijderen uit doelen {#remove-dataset}

Om datasets uit een bestaande gegevensstroom te verwijderen, volg de stappen hieronder:

1. Login aan [&#x200B; UI van Experience Platform &#x200B;](https://experience.adobe.com/platform/) en selecteer **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Browse]** in de bovenste koptekst om de bestaande doelgegevens weer te geven.

   ![&#x200B; doorbladert de Bestemming mening met een getoonde bestemmingsverbinding en de rest vervaagd uit.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Selecteer het filterpictogram ![&#x200B; filter-pictogram &#x200B;](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

2. Van de **[!UICONTROL Activation data]** kolom, selecteer de datasetcontrole om alle datasets te bekijken die aan dit de uitvoerdataflow in kaart worden gebracht.

   ![&#x200B; de beschikbare optie van de datasetnavigatie die in de kolom van de Gegevens van de Activering wordt benadrukt.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. De pagina **[!UICONTROL Activation data]** voor het doel wordt weergegeven. Gebruik de selectievakjes aan de linkerkant van de lijst met gegevenssets om de gegevenssets te selecteren die u wilt verwijderen en selecteer vervolgens **[!UICONTROL Remove datasets]** in de rechterrail om het dialoogvenster voor het bevestigen van gegevenssets te openen.

   ![&#x200B; verwijder datasetdialoog die de Remove datasetcontrole in het juiste spoor toont.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. Selecteer in het bevestigingsdialoogvenster **[!UICONTROL Remove]** om de gegevensset direct te verwijderen uit het exporteren naar het doel.

   ![&#x200B; Dialoog die de bevestigingsoptie van de datasetverwijdering van dataflow toont.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Uitvoerrechten gegevensset {#licensing-entitlement}

Raadpleeg de productbeschrijvingsdocumenten om te begrijpen hoeveel gegevens u per jaar voor elke Experience Platform-toepassing mag exporteren. Bijvoorbeeld, kunt u de Beschrijving van het Product van Real-Time CDP [&#x200B; hier &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) bekijken.

De gegevensuitvoerrechten voor verschillende aanvragen zijn niet additief. Dit betekent bijvoorbeeld dat als u Real-Time CDP Ultimate en Adobe Journey Optimizer Ultimate koopt, de uitvoerrechten voor profielen de hoogste van de twee rechten zijn, zoals beschreven in de productbeschrijvingen. Uw volumeregelingen worden berekend door het totale aantal gelicentieerde profielen te nemen en te vermenigvuldigen met 500 kB voor Real-Time CDP Prime of 700 kB voor Real-Time CDP Ultimate om te bepalen hoeveel hoeveelheid gegevens u hebt.

Anderzijds, als u toe:voegen-ons zoals Gegevens Distiller kocht, vertegenwoordigt de grens van de gegevensuitvoer die u gerechtigd bent om te zijn de som van de productrij en de toe:voegen-op.

U kunt uw profieluitvoer tegen uw contractuele grenzen in het [&#x200B; dashboard van het vergunningsgebruik bekijken en volgen &#x200B;](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md).

## Bekende beperkingen {#known-limitations}

Houd in mening de volgende beperkingen voor de algemene beschikbaarheidsversie van de uitvoer van datasets:

* Experience Platform kan meerdere bestanden exporteren, zelfs voor kleine gegevenssets. Dataset exporteren is ontworpen voor systeemintegratie en geoptimaliseerd voor prestaties. Het aantal geëxporteerde bestanden kan daarom niet worden aangepast.
* De geëxporteerde bestandsnamen kunnen momenteel niet worden aangepast.
* UI blokkeert momenteel niet u van het schrappen van een dataset die naar een bestemming wordt uitgevoerd. Verwijder geen datasets die naar bestemmingen worden geëxporteerd. [&#x200B; verwijder de dataset &#x200B;](#remove-dataset) uit een bestemmingsdataflow alvorens het te schrappen.
* De metriek van de controle voor de uitvoer van datasets wordt momenteel gemengd met aantallen voor profieluitvoer zodat weerspiegelen zij niet de ware uitvoeraantallen.
* Gegevens met een tijdstempel die ouder is dan 365 dagen, worden niet geëxporteerd voor gegevenssets. Voor meer informatie, bekijk de [&#x200B; gidsen voor de geplande uitvoer van datasets &#x200B;](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)

## Veelgestelde vragen {#faq}

**kunnen wij een dossier zonder een omslag produceren als wij enkel bij `/` als omslagweg bewaren? Ook, als wij geen omslagweg vereisen, hoe dossiers met dubbele namen in een omslag of een plaats worden geproduceerd?**

+++Antwoord
Vanaf de release van september 2024 kunt u de mapnaam aanpassen en zelfs `/` gebruiken voor het exporteren van bestanden voor alle gegevenssets in dezelfde map. Adobe adviseert dit niet voor bestemmingen die veelvoudige datasets uitvoeren, aangezien de systeem-geproduceerde filenames die tot verschillende datasets behoren in de zelfde omslag zullen worden gemengd.
+++

**kunt u het manifestdossier aan één omslag en gegevensdossiers in een andere omslag leiden?**

+++Antwoord
Nee, het manifestbestand kan niet naar een andere locatie worden gekopieerd.
+++

**kunnen wij het rangschikken of timing van dossierlevering controleren?**

+++Antwoord
Er zijn opties voor het plannen van het exporteren. Er zijn geen opties om de kopie van de bestanden te vertragen of in volgorde te zetten. Ze worden naar de opslaglocatie gekopieerd zodra ze worden gegenereerd.
+++

**Welke formaten zijn beschikbaar voor het manifestdossier?**

+++Antwoord
Het manifestbestand heeft de indeling .json.
+++

**is er API beschikbaarheid voor het duidelijke dossier?**

+++Antwoord
Er is geen API beschikbaar voor het manifestbestand, maar het bevat wel een lijst met bestanden die de export omvatten.
+++

**kunnen wij extra details aan het manifestdossier (d.w.z., verslagtelling) toevoegen? Zo ja, hoe?**

+++Antwoord
Er is geen mogelijkheid om aanvullende informatie aan het manifestbestand toe te voegen. Het aantal records is beschikbaar via de entiteit `flowRun` (kan worden opgevraagd via de API). Lees meer in bestemmingen controle.
+++

**Hoe worden de gegevensdossiers verdeeld? Hoeveel verslagen per dossier?**

+++Antwoord
Gegevensbestanden worden gesplitst volgens de standaardpartitionering in het Experience Platform-gegevensmeer. Grotere datasets hebben een hoger aantal verdelingen. Standaard het verdelen is niet configureerbaar door de gebruiker aangezien het voor lezing wordt geoptimaliseerd.
+++

**kunnen wij een drempel (aantal verslagen per dossier) plaatsen?**

+++Antwoord
Nee, dat is niet mogelijk.
+++

**hoe wij opnieuw een gegevensreeks in de gebeurtenis sturen dat de aanvankelijke verzendt slecht is?**

+++Antwoord
Voor de meeste typen systeemfouten worden automatisch opnieuw opgestart.
+++