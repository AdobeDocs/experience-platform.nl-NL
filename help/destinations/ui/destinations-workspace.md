---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;bestemmingscatalogus;
title: Werkruimte Doelen
description: De werkruimte van Doelen bestaat uit vijf secties, Overzicht, Catalogus, doorbladeren, Rekeningen, en de Mening van het Systeem. Deze worden in de onderstaande secties beschreven.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 73d84174a9960e180a81c3db938f3f18f68f3beb
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Experience Platform **[!UICONTROL Destinations]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Destinations] .

De werkruimte van [!UICONTROL Destinations] bestaat uit vijf secties, [!UICONTROL Overview] , [!UICONTROL Catalog] , [!UICONTROL Browse] , [!UICONTROL Accounts] en [!UICONTROL System View] , die in de onderstaande secties worden beschreven.

![ het overzichtdashboard van Doelen die drie widgets tonen.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

Op het tabblad **[!UICONTROL Overview]** wordt het dashboard van [!UICONTROL Destinations] weergegeven met meetgegevens die betrekking hebben op de doelgegevens van uw organisatie. Ga voor meer informatie naar de [[!UICONTROL Destinations] dashboardgids ](../../dashboards/guides/destinations.md) .

>[!NOTE]
>
>Als uw organisatie nieuw is voor Experience Platform en nog geen actieve doelen heeft, zijn het dashboard [!UICONTROL Destinations] en het tabblad [!UICONTROL Overview] niet zichtbaar. In plaats daarvan, die [!UICONTROL Destinations] van de linkernavigatie selecteren toont [[!UICONTROL Catalog] lusje ](#catalog).

![ het lusje van het Overzicht van het dashboard van Doelen.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

Op het tabblad **[!UICONTROL Catalog]** wordt een lijst weergegeven met alle doelen die beschikbaar zijn in [!DNL Experience Platform] en waarnaar u gegevens kunt verzenden.

![ catalogus van Doelen die veelvoudige bestemmingen tonen.](../assets/ui/workspace/catalog.png)

De gebruikersinterface van [!DNL Experience Platform] biedt verschillende zoek- en filteropties op de pagina met de doelcatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Filter doelen met het besturingselement **[!UICONTROL Categories]** .
* Schakelen tussen **[!UICONTROL All destinations]** en **[!UICONTROL My destinations]** . Wanneer u **[!UICONTROL All destinations]** selecteert, worden alle beschikbare [!DNL Experience Platform] -doelen weergegeven. Wanneer u **[!UICONTROL My destinations]** selecteert, kunt u alleen de doelen zien waarmee u een verbinding hebt gemaakt.
* Selecteer deze optie om de typen **[!UICONTROL Connections]** en/of **[!UICONTROL Extensions]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, lees [ de Types en de Categorieën van Bestemming ](../destination-types.md).
* Filter de beschikbare die bestemmingen op hun gesteund [ worden gebaseerd gegevenstype ](/help/destinations/destination-sdk/functionality/destination-configuration/audience-data-type.md). U kunt kiezen tussen publiek publiek, accountpubliek, publiek in het vooruitzicht of het exporteren van gegevenssets.

De bestemmingskaarten bevatten primaire en secundaire controleopties. De belangrijkste besturingselementen zijn [!UICONTROL Set up] , [!UICONTROL Activate] , [!UICONTROL Activate audiences] of [!UICONTROL Export datasets] . Met de secundaire besturingselementen kunt u opties weergeven. Deze besturingselementen worden hieronder beschreven:

| Besturing | Beschrijving |
|---------|----------|
| [!UICONTROL Set up] | Hiermee kunt u verbinding maken met het doel. |
| [!UICONTROL Activate] | Zodra u een verbinding aan de bestemming hebt gevestigd, kunt u publiek activeren of datasets uitvoeren naar deze bestemming. |
| [!UICONTROL Activate audiences] | Nadat u een verbinding met de bestemming hebt gemaakt, kunt u het publiek naar deze bestemming activeren. |
| [!UICONTROL Export datasets] | Zodra u een verbinding aan de bestemming hebt gevestigd, kunt u datasets naar deze bestemming uitvoeren. |
| [!UICONTROL View account] | Bekijk de accounts waarmee u verbinding hebt gemaakt voor een bestemming. |
| [!UICONTROL View dataflows] | Bekijk de gegevensactiveringsstromen die voor een bestemming bestaan. |
| [!UICONTROL View documentation] | Opent een verbinding aan de documentatiepagina voor die specifieke bestemming, voor meer informatie en om u te helpen opstelling het. |

{style="table-layout:auto"}

![ Controles op de bestemmingskaart ](../assets/ui/workspace/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen. Hier, kunt u een beschrijving van de bestemming zien. De spoorstaaf rechts bevat dezelfde bedieningsorganen als in de bovenstaande tabel, met inbegrip van een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![ de catalogusopties van de Bestemming ](../assets/ui/workspace/destination-right-rail.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie de [ catalogus van de Bestemming ](../catalog/overview.md) en [ de types en de categorieën van de Bestemming ](../destination-types.md).

## [!UICONTROL Browse] {#browse}

Op het tabblad **[!UICONTROL Browse]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt.

>[!TIP]
>
> Begin met de [ onderzoeksbar ](#search-browse) om specifieke dataflows te vinden, dan gebruik de [ sidebar filters ](#filter-options-browse) om uw resultaten verder te versmallen.

Doelen waarvoor de schakeloptie **[!UICONTROL Enabled/Disabled]** is ingeschakeld, stellen het doel in op respectievelijk **[!UICONTROL Enabled]** of **[!UICONTROL Disabled]** . U kunt ook de doelen weergeven waar de gegevens stromen door **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** te selecteren en een publiek te selecteren dat moet worden geïnspecteerd.

>[!TIP]
>
> ![ doorbladert Lusje ](../assets/ui/workspace/browse-tab.png)
> 
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ activeer de controle van het publiek ](/help/images/icons/data-add.png) **[!UICONTROL Activate audiences]** controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ uitgeven bestemmingscontrole ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**&#x200B;controle om bestaande bestemmingsverbindingen uit te geven. Lees het leerprogramma op [ het uitgeven bestemmingen ](/help/destinations/ui/edit-destination.md) voor meer informatie.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ uitgeven marketing actiecontrole ](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Edit marketing actions]** controle om [ de marketing acties ](/help/destinations/ui/edit-activation.md#edit-marketing-actions) voor de geselecteerde bestemming te veranderen.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![ controle van de Schrapping ](/help/images/icons/delete.png) **[!UICONTROL Delete]** controle [ verwijderen ](delete-destinations.md) een bestaande verbinding aan een bestemming.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![ Mening in controle ](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]** controle om activeringsinformatie voor deze bestemming in het [ controledashboard ](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) te bekijken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ Abonneren aan alarm ](/help/images/icons/alert-add.png) **[!UICONTROL Subscribe to alerts]** controle om aan bestemmingdataflow alarm in te gaan. U kunt zich op alarm intekenen om berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. Zie [ aan in-context bestemmingsalarm ](alerts.md) voor gedetailleerde informatie over bestemmingdataflow alarm abonneren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ beheer markeringen ](/help/images/icons/manage-tags.png) **[!UICONTROL Manage tags]** controle om markeringen toe te voegen of te verwijderen uit een bestemming. Zie [ bestemmingsmarkeringen ](#manage-tags) sectie voor gedetailleerde informatie beheren bij het gebruiken van markeringen.

Zie de tabel hieronder voor alle informatie die voor elke bestemming wordt opgegeven op het tabblad [!UICONTROL Browse] .

| Element | Beschrijving |
|---------|----------|
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. |
| Gegevenstype | Het type gegevens dat wordt ondersteund door de doelverbinding. Ondersteunde gegevenstypen: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | De status van de laatste gegevensstroomuitvoering. Zie [ de bestemmingsdetails van de Mening ](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Last Dataflow Run Date] | Tijd en datum waarop de laatste dataflow-run heeft plaatsgevonden. Zie [ de bestemmingsdetails van de Mening ](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Account Expiration Date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor de [ verbinding van Facebook ](../catalog/social/facebook.md). |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activation Data] | Geeft het aantal soorten publiek aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement om meer te weten te komen over het geactiveerde publiek. Verwijs naar [ Gegevens van de Activering ](/help/destinations/ui/destination-details-page.md#activation-data) in de pagina van bestemmingsdetails voor meer informatie over het geactiveerde publiek. |
| [!UICONTROL Created] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. Selecteer het pijl-omhoog/pijl-omlaag om de activeringsstromen eerst op de nieuwste of eerst op de oudste te sorteren. |
| [!UICONTROL Status] | `Enabled` of `Disabled` . Geeft aan of gegevens op dit doel worden geactiveerd. |
| [!UICONTROL Access labels] | Toont om het even welke toegangslabels die aan dit bestemmingsgegeven werden toegevoegd. Lees meer over [ het toepassen van toegangslabels op bestemmingsdataflows ](/help/access-control/abac/apply-access-labels-destinations.md). |
| [!UICONTROL Tags] | Hiermee geeft u alle tags weer die aan deze doelgegevensstroom zijn toegevoegd. Gebruik labels om uw gegevensstromen te ordenen en te categoriseren voor eenvoudiger beheer. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf, zoals bestemmings identiteitskaart, beschrijving, het aantal geactiveerde doelsoorten, en meer te tonen.

![ klik bestemmingsrij ](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over het publiek te zien dat aan deze bestemming wordt geactiveerd. Klik **[!UICONTROL Edit destination]** om [ de bestemmingsmontages ](/help/destinations/ui/edit-destination.md) te wijzigen of **[!UICONTROL Activate audiences]** om nieuw publiek aan dataflow toe te voegen.

### Gegevens filteren op het tabblad Bladeren {#filter-browse}

Het tabblad **[!UICONTROL Browse]** bevat verbeterde filtermogelijkheden en zoekmogelijkheden waarmee u snel de doelgegevens kunt vinden en beheren. Gebruik de linkerzijbalk om filters toe te passen en de zoekbalk om specifieke gegevensstromen op naam te zoeken.

### Zoekfunctionaliteit {#search-browse}

Gebruik de zoekbalk boven aan de tabel om snel gegevens op naam te zoeken. Terwijl u typt, worden de resultaten automatisch gefilterd om alleen overeenkomende gegevensstromen weer te geven.

>[!NOTE]
>
> Wanneer het zoeken naar gegevensstromen gebruikend de onderzoeksdoos, kunnen de resultaten dataflows omvatten die uw [ de etiketten van de gebruikerstoegang ](/help/access-control/abac/apply-access-labels-destinations.md) u van het zien beperken. Dit gedrag wordt in een toekomstige update gecorrigeerd. Als u dergelijke gegevensstromen selecteert, worden de gegevens niet weergegeven in de rechterrail en kunnen gebruikers zonder toegang tot de vereiste labels geen wijzigingen uitvoeren, zoals het toewijzen van soorten publiek aan de gegevensstroom of het bewerken van het bijbehorende schema.

![ Geanimeerde demonstratie van het zoeken naar een bestemmingsdataflow in het Browse lusje ](../assets/ui/workspace/search.gif)

### Filteropties {#filter-options-browse}

Gebruik de filters in de linkerzijbalk om de zoekopdracht te beperken.

![ de filters van de Bestemming in het Browse lusje ](../assets/ui/workspace/destination-filters.png)


* **[!UICONTROL Destination platform]**: filtergegevens die door specifieke doelplatforms worden gefilterd (bijvoorbeeld [!DNL Amazon S3] , [!DNL Facebook Custom Audience] , [!DNL LinkedIn Matched Audience] , enz.). U kunt meerdere platforms tegelijk selecteren.
* **[!UICONTROL Has any tag]**: filtergegevensstromen waaraan specifieke tags zijn toegewezen. Op deze manier kunt u gegevensstromen ordenen en zoeken op basis van uw aangepaste tags.
* **[!UICONTROL Status]**: De gegevens van de filter door hun operationele status:
   * **[!UICONTROL Enabled]**: alleen actieve gegevensstromen tonen
   * **[!UICONTROL Disabled]**: alleen inactieve gegevensstromen tonen
* **[!UICONTROL Account name]**: filtergegevens op de bijbehorende accountnaam. Hierdoor kunt u alle gegevensstromen vinden die zijn verbonden met een specifieke doelaccount.
* **[!UICONTROL Created]**: filtergegevens door de gebruiker die ze heeft gemaakt. Gebruik dit filter om dataflows te vinden die door specifieke teamleden worden gecreeerd.
* **[!UICONTROL Modified by]**: De gegevens van de filter door de gebruiker die hen het laatst wijzigde. Met dit filter kunt u recente wijzigingen identificeren die door specifieke gebruikers zijn aangebracht.
* **[!UICONTROL Creation date]**: Filter de gegevens op de aanmaakdatum met behulp van een datumbereik:
   * **[!UICONTROL Start date]**: het begin van het datumbereik instellen
   * **[!UICONTROL End date]**: het einde van het datumbereik instellen
* **[!UICONTROL Modified date]**: De gegevens van de filter door hun wijzigingsdatum gebruikend een datumwaaier:
   * **[!UICONTROL Start date]**: het begin van het datumbereik instellen
   * **[!UICONTROL End date]**: het einde van het datumbereik instellen

### Actieve filters {#active-filters-browse}

Wanneer u filters toepast, worden deze weergegeven als tags onder de zoekbalk.

![ Actieve filters die als markeringen onder de onderzoeksbar ](../assets/ui/workspace/active-filters.png) worden getoond

Daar kunt u:

* Alle momenteel actieve filters weergeven
* Afzonderlijke filters verwijderen door op het pictogram `X` op elke filtertag te klikken
* Alle filters tegelijk wissen met de optie **[!UICONTROL Clear all]**

### Doeltags beheren {#manage-tags}

Met tags kunt u uw doelgegevens ordenen en indelen, zodat u ze eenvoudiger kunt beheren. U kunt labels toevoegen aan en verwijderen uit afzonderlijke gegevensstromen om deze te groeperen op basis van uw bedrijfsbehoeften.

Als u een tag wilt toevoegen aan een gegevensstroom, selecteert u de ellips (`...`) in de **[!UICONTROL Name]** -kolom en selecteert u **[!UICONTROL Manage tags]** in het contextmenu.
Typ de naam van een nieuwe tag in het veld **[!UICONTROL Tags]** en selecteer **[!UICONTROL Save]** om de wijzigingen toe te passen.

![ beheert de dialoog van markeringen die markeringsselectie en verwezenlijking opties tonen ](../assets/ui/workspace/tags.gif)

Als u een tag uit een gegevensstroom wilt verwijderen, selecteert u de ellips (`...`) in de **[!UICONTROL Name]** -kolom en selecteert u **[!UICONTROL Manage tags]** in het contextmenu. Vervolgens selecteert u het pictogram `X` op de tag die u wilt verwijderen.

### Aanbevolen werkwijzen labelen {#tag-best-practices}

Zorg ervoor dat de gegevensstromen van uw bestemming georganiseerd, gemakkelijk te vinden en handelbaar blijven door de etiketteringsrichtlijnen hieronder te volgen.

* **de beschrijvende namen van het Gebruik**: Creeer markeringen die duidelijk het doel of de categorie van dataflow (b.v., &quot;de Campagnes van de Marketing&quot;, &quot;Behoud van de Klant&quot;, &quot;Seizoensgebonden Bevorderingen&quot;wijzen)
* **ben verenigbaar**: Gebruik een verenigbare noemende overeenkomst over uw organisatie
* **houd het eenvoudig**: Vermijd het creëren van teveel markeringen, aangezien dit het filtreren minder effectief kan maken
* **hiërarchische markeringen van het Gebruik**: Overweeg het gebruiken van prefixen aan groep verwante markeringen (b.v., &quot;Campagne-Q4&quot;, &quot;Campagne-Q1&quot;)

## [!UICONTROL Accounts] {#accounts}

Op het tabblad **[!UICONTROL Accounts]** vindt u meer informatie over de verbindingen die u hebt gemaakt met verschillende doelen. Bovendien kunt u bestaande accountgegevens bijwerken of verwijderen. Zie de tabel hieronder voor alle informatie die u op elke doelaccount kunt krijgen.

>[!TIP]
>
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![ controle ](/help/images/icons/data-add.png)**[!UICONTROL Activate]**&#x200B;activeren/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**&#x200B;controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![ uitgeven detailcontrole ](/help/images/icons/edit.png)**[!UICONTROL Edit details]**&#x200B;controle om [&#128279;](update-accounts.md) de details van een bestaande bestemmingsrekening bij te werken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik de ![ controle van de Schrapping ](/help/images/icons/delete.png)**[!UICONTROL Delete]**&#x200B;controle [ om ](delete-destination-account.md) een bestaande bestemmingsrekening te schrappen.

![ Rekeningen tabel ](../assets/ui/workspace/accounts-tab.png)

| Element | Beschrijving |
|---|---|
| [!UICONTROL Name] | De naam u aan de bestemmingsrekening toewees terwijl [ vestiging ](connect-destination.md#authenticate) de bestemming. |
| [!UICONTROL Destination] | De bestemmingsschakelaar waarvoor u opstelling de verbinding hebt. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het type van rekeningsverbinding aan uw opslagemmer of bestemming. Afhankelijk van de bestemming, zijn de authentificatieopties: <ul><li>Voor e-mailmarketingbestemmingen: kan S3, FTP of Azure Blob zijn.</li><li>Voor reclame-bestemmingen in real time: Server-aan-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: basisverificatie voor SFTP</li><li>OAuth 1- of OAuth 2-verificatie</li><li>Toekennerverificatie</li></ul> |
| [!UICONTROL Username] | De gebruikersbenaming u in [ selecteerde verbind bestemmingswerkschema ](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsdataflows die met basisinformatie worden verbonden voor een bestemming worden gecreeerd. |
| [!UICONTROL Authorization date] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |
| [!UICONTROL Expiration date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor de [ verbinding van Facebook ](../catalog/social/facebook.md). |

{style="table-layout:auto"}

### Filteraccounts {#filter-accounts}

Het tabblad **[!UICONTROL Accounts]** bevat verbeterde filtermogelijkheden en zoekmogelijkheden, zodat u uw doelaccounts snel kunt vinden en beheren. Gebruik de linkerzijbalk om filters toe te passen en de zoekbalk om specifieke accounts op naam te zoeken.

#### Zoeken naar accounts {#search-accounts}

Gebruik de zoekbalk boven aan de tabel om snel accounts op naam te zoeken. Terwijl u typt, worden de resultaten automatisch gefilterd om alleen overeenkomende accounts weer te geven.

![ bar van het Onderzoek in de Rekeningen tabel.](../assets/ui/workspace/accounts-search.gif)

#### Filteropties {#filter-options-accounts}

Gebruik de filters in de linkerzijbalk om de zoekopdracht te beperken.

![ de filters van de Rekening in het lusje van Rekeningen ](../assets/ui/workspace/account-filters.png)

* **[!UICONTROL Destination platform]**: Filter accounts op specifieke doelplatforms (bijvoorbeeld: [!DNL Microsoft Bing] , [!DNL Amazon S3] , [!DNL Facebook Custom Audiences] , [!DNL LinkedIn Matched Audiences] , enzovoort). U kunt meerdere platforms tegelijk selecteren.
* **[!UICONTROL Created by]**: Filteraccounts van de gebruiker die ze heeft gemaakt. Gebruik dit filter om rekeningen te vinden die door specifieke teamleden worden gecreeerd.

#### Actieve filters {#active-filters-accounts}

Wanneer u filters toepast, worden deze weergegeven als tags onder de zoekbalk.

![ Actieve filters die als markeringen in de Rekeningen tabel ](../assets/ui/workspace/accounts-active-filters.png) worden getoond

Daar kunt u:

* Alle momenteel actieve filters weergeven
* Afzonderlijke filters verwijderen door op het pictogram `X` op elke filtertag te klikken
* Alle filters tegelijk wissen met de optie **[!UICONTROL Clear all]**

## [!UICONTROL System View] {#system-view}

Het tabblad **[!UICONTROL System View]** geeft een grafische weergave weer van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![ gegevens-flows1 ](../assets/ui/workspace/system-view-dataflows.png)

Selecteer een van de doelen die op de pagina worden weergegeven en klik op **[!UICONTROL View dataflows]** om informatie weer te geven over alle verbindingen die u voor elke bestemming hebt ingesteld.

![ gegevens-flows2 ](../assets/ui/workspace/system-view-dataflows-2.png)
