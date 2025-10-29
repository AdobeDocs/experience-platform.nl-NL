---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;bestemmingscatalogus;
title: Werkruimte Doelen
description: De werkruimte van Doelen bestaat uit vijf secties, Overzicht, Catalogus, doorbladeren, Rekeningen, en de Mening van het Systeem. Deze worden in de onderstaande secties beschreven.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Experience Platform **[!UICONTROL Destinations]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Destinations] .

De werkruimte van [!UICONTROL Destinations] bestaat uit vijf secties, [!UICONTROL Overview] , [!UICONTROL Catalog] , [!UICONTROL Browse] , [!UICONTROL Accounts] en [!UICONTROL System View] , die in de onderstaande secties worden beschreven.

![&#x200B; het overzichtdashboard van Doelen die drie widgets tonen.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

Op het tabblad **[!UICONTROL Overview]** wordt het dashboard van [!UICONTROL Destinations] weergegeven met meetgegevens die betrekking hebben op de doelgegevens van uw organisatie. Ga voor meer informatie naar de [[!UICONTROL Destinations] dashboardgids &#x200B;](../../dashboards/guides/destinations.md) .

>[!NOTE]
>
>Als uw organisatie nieuw is voor Experience Platform en nog geen actieve doelen heeft, zijn het dashboard [!UICONTROL Destinations] en het tabblad [!UICONTROL Overview] niet zichtbaar. In plaats daarvan, die [!UICONTROL Destinations] van de linkernavigatie selecteren toont [[!UICONTROL Catalog] lusje &#x200B;](#catalog).

![&#x200B; het lusje van het Overzicht van het dashboard van Doelen.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

Op het tabblad **[!UICONTROL Catalog]** wordt een lijst weergegeven met alle doelen die beschikbaar zijn in [!DNL Experience Platform] en waarnaar u gegevens kunt verzenden.

![&#x200B; catalogus van Doelen die veelvoudige bestemmingen tonen.](../assets/ui/workspace/catalog.png)

De gebruikersinterface van [!DNL Experience Platform] biedt verschillende zoek- en filteropties op de pagina met de doelcatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Filter doelen met het besturingselement **[!UICONTROL Categories]** .
* Schakelen tussen **[!UICONTROL All destinations]** en **[!UICONTROL My destinations]** . Wanneer u **[!UICONTROL All destinations]** selecteert, worden alle beschikbare [!DNL Experience Platform] -doelen weergegeven. Wanneer u **[!UICONTROL My destinations]** selecteert, kunt u alleen de doelen zien waarmee u een verbinding hebt gemaakt.
* Selecteer deze optie om de typen **[!UICONTROL Connections]** en/of **[!UICONTROL Extensions]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, lees [&#x200B; de Types en de Categorieën van Bestemming &#x200B;](../destination-types.md).
* Filter de beschikbare die bestemmingen op hun gesteund [&#x200B; worden gebaseerd gegevenstype &#x200B;](/help/destinations/destination-sdk/functionality/destination-configuration/audience-data-type.md). U kunt kiezen tussen publiek publiek, accountpubliek, publiek in het vooruitzicht of het exporteren van gegevenssets.

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

![&#x200B; Controles op de bestemmingskaart &#x200B;](../assets/ui/workspace/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen. Hier, kunt u een beschrijving van de bestemming zien. De spoorstaaf rechts bevat dezelfde bedieningsorganen als in de bovenstaande tabel, met inbegrip van een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![&#x200B; de catalogusopties van de Bestemming &#x200B;](../assets/ui/workspace/destination-right-rail.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie de [&#x200B; catalogus van de Bestemming &#x200B;](../catalog/overview.md) en [&#x200B; de types en de categorieën van de Bestemming &#x200B;](../destination-types.md).

## [!UICONTROL Browse] {#browse}

>[!NOTE]
>
>Vanwege configuraties met toegangslabels kunnen doelgegevens waarop een gebruiker geen toegang heeft, in de gebruikersinterface worden weergegeven in een status die grijs wordt weergegeven. Lees de documentatie op [&#x200B; gebruikend toegangslabels om gebruikerstoegang tot bestemmingsdataflows &#x200B;](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know) voor meer informatie te beheren.

Op het tabblad **[!UICONTROL Browse]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt.

>[!TIP]
>
> Begin met de [&#x200B; onderzoeksbar &#x200B;](#search-browse) om specifieke dataflows te vinden, dan gebruik de [&#x200B; sidebar filters &#x200B;](#filter-options-browse) om uw resultaten verder te versmallen.

Doelen waarvoor de schakeloptie **[!UICONTROL Enabled/Disabled]** is ingeschakeld, stellen het doel in op respectievelijk **[!UICONTROL Enabled]** of **[!UICONTROL Disabled]** . U kunt ook de doelen weergeven waar de gegevens stromen door **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** te selecteren en een publiek te selecteren dat moet worden geïnspecteerd.

>[!TIP]
>
> ![&#x200B; doorbladert Lusje &#x200B;](../assets/ui/workspace/browse-tab.png)
> 
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![&#x200B; activeer de controle van het publiek &#x200B;](/help/images/icons/data-add.png) **[!UICONTROL Activate audiences]** controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![&#x200B; uitgeven bestemmingscontrole &#x200B;](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**&#x200B;controle om bestaande bestemmingsverbindingen uit te geven. Lees het leerprogramma op [&#x200B; het uitgeven bestemmingen &#x200B;](/help/destinations/ui/edit-destination.md) voor meer informatie.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![&#x200B; uitgeven marketing actiecontrole &#x200B;](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Edit marketing actions]** controle om [&#x200B; de marketing acties &#x200B;](/help/destinations/ui/edit-activation.md#edit-marketing-actions) voor de geselecteerde bestemming te veranderen.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![&#x200B; controle van de Schrapping &#x200B;](/help/images/icons/delete.png) **[!UICONTROL Delete]** controle [&#x200B; verwijderen &#x200B;](delete-destinations.md) een bestaande verbinding aan een bestemming.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![&#x200B; Mening in controle &#x200B;](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]** controle om activeringsinformatie voor deze bestemming in het [&#x200B; controledashboard &#x200B;](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) te bekijken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![&#x200B; Abonneren aan alarm &#x200B;](/help/images/icons/alert-add.png) **[!UICONTROL Subscribe to alerts]** controle om aan bestemmingdataflow alarm in te gaan. U kunt zich op alarm intekenen om berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. Zie [&#x200B; aan in-context bestemmingsalarm &#x200B;](alerts.md) voor gedetailleerde informatie over bestemmingdataflow alarm abonneren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![&#x200B; beheer markeringen &#x200B;](/help/images/icons/manage-tags.png) **[!UICONTROL Manage tags]** controle om markeringen toe te voegen of te verwijderen uit een bestemming. Zie [&#x200B; bestemmingsmarkeringen &#x200B;](#manage-tags) sectie voor gedetailleerde informatie beheren bij het gebruiken van markeringen.

Zie de tabel hieronder voor alle informatie die voor elke bestemming wordt opgegeven op het tabblad [!UICONTROL Browse] .

| Element | Beschrijving |
|---------|----------|
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. |
| Gegevenstype | Het type gegevens dat wordt ondersteund door de doelverbinding. Ondersteunde gegevenstypen: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | De status van de laatste gegevensstroomuitvoering. Zie [&#x200B; de bestemmingsdetails van de Mening &#x200B;](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Last Dataflow Run Date] | Tijd en datum waarop de laatste dataflow-run heeft plaatsgevonden. Selecteer de kolomkop voor toegang tot sorteeropties (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]** ). Zie [&#x200B; de bestemmingsdetails van de Mening &#x200B;](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Account Expiration Date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br> Een waarschuwingspictogram ![&#x200B; Waarschuwing: het pictogram van de rekeningsvervaldatum &#x200B;](/help/images/icons/alert-expiration.png) verschijnt vóór de vervaldatum om u te waarschuwen dat de verbinding zal verlopen en misschien vernieuwing zal vereisen. Gegevensstromen naar verlopen verbindingen worden gestopt en u moet opnieuw verifiëren om uw activeringsworkflows te hervatten. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor [&#x200B; Pinterest &#x200B;](../catalog/advertising/pinterest.md), [&#x200B; LinkedIn &#x200B;](../catalog/social/linkedin.md), en [&#x200B; LinkedIn Gelijke Publiek &#x200B;](../catalog/social/linkedin-b2b.md) verbindingen. <br> ![&#x200B; Voorbeeld van de waarschuwing van de rekeningsvervalsing in Browse lusje &#x200B;](../assets/ui/workspace/account-expiration-browse.png){width="100" zoomable="yes" alt="Screenshot showing the account expiration warning icon and expiration date in the Browse tab."} |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activation Data] | Geeft het aantal soorten publiek aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement om meer te weten te komen over het geactiveerde publiek. Verwijs naar [&#x200B; Gegevens van de Activering &#x200B;](/help/destinations/ui/destination-details-page.md#activation-data) in de pagina van bestemmingsdetails voor meer informatie over het geactiveerde publiek. |
| [!UICONTROL Created] | De datum en tijd waarop de activeringsstroom naar het doel is gemaakt. Selecteer het pijl-omhoog/pijl-omlaag om de activeringsstromen eerst op de nieuwste of eerst op de oudste te sorteren. |
| [!UICONTROL Modified] | De datum en tijd waarop de activeringsstroom naar de bestemming voor het laatst is gewijzigd. |
| [!UICONTROL Status] | `Enabled` of `Disabled` . Geeft aan of gegevens op dit doel worden geactiveerd. |
| [!UICONTROL Access labels] | Toont om het even welke toegangslabels die aan dit bestemmingsgegeven werden toegevoegd. Lees meer over [&#x200B; het toepassen van toegangslabels op bestemmingsdataflows &#x200B;](/help/access-control/abac/apply-access-labels-destinations.md). |
| [!UICONTROL Tags] | Hiermee geeft u alle tags weer die aan deze doelgegevensstroom zijn toegevoegd. Gebruik labels om uw gegevensstromen te ordenen en te categoriseren voor eenvoudiger beheer. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf, zoals bestemmings identiteitskaart, beschrijving, het aantal geactiveerde doelsoorten, en meer te tonen.

![&#x200B; klik bestemmingsrij &#x200B;](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over het publiek te zien dat aan deze bestemming wordt geactiveerd. Klik **[!UICONTROL Edit destination]** om [&#x200B; de bestemmingsmontages &#x200B;](/help/destinations/ui/edit-destination.md) te wijzigen of **[!UICONTROL Activate audiences]** om nieuw publiek aan dataflow toe te voegen.

### Gegevens filteren op het tabblad Bladeren {#filter-browse}

Het tabblad **[!UICONTROL Browse]** bevat verbeterde filtermogelijkheden en zoekmogelijkheden waarmee u snel de doelgegevens kunt vinden en beheren. Gebruik de linkerzijbalk om filters toe te passen en de zoekbalk om specifieke gegevensstromen op naam te zoeken.

### Zoekfunctionaliteit {#search-browse}

Gebruik de zoekbalk boven aan de tabel om snel gegevens op naam te zoeken. Terwijl u typt, worden de resultaten automatisch gefilterd om alleen overeenkomende gegevensstromen weer te geven.

![Geanimeerde demonstratie van het zoeken naar een bestemmingsgegevensstroom in het tabblad Verkennen](../assets/ui/workspace/search.gif)

### Filteropties {#filter-options-browse}

Gebruik de filters in de linkerzijbalk om de zoekopdracht te beperken.

![&#x200B; de filters van de Bestemming in het Browse lusje &#x200B;](../assets/ui/workspace/destination-filters.png)

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

![&#x200B; Actieve filters die als markeringen onder de onderzoeksbar &#x200B;](../assets/ui/workspace/active-filters.png) worden getoond

Daar kunt u:

* Alle momenteel actieve filters weergeven
* Afzonderlijke filters verwijderen door op het pictogram `X` op elke filtertag te klikken
* Alle filters tegelijk wissen met de optie **[!UICONTROL Clear all]**

### Doeltags beheren {#manage-tags}

Met tags kunt u uw doelgegevens ordenen en indelen, zodat u ze eenvoudiger kunt beheren. U kunt labels toevoegen aan en verwijderen uit afzonderlijke gegevensstromen om deze te groeperen op basis van uw bedrijfsbehoeften.

Als u een tag wilt toevoegen aan een gegevensstroom, selecteert u de ellips (`...`) in de **[!UICONTROL Name]** -kolom en selecteert u **[!UICONTROL Manage tags]** in het contextmenu.
Typ de naam van een nieuwe tag in het veld **[!UICONTROL Tags]** en selecteer **[!UICONTROL Save]** om de wijzigingen toe te passen.

![&#x200B; beheert de dialoog van markeringen die markeringsselectie en verwezenlijking opties tonen &#x200B;](../assets/ui/workspace/tags.gif)

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
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![&#x200B; controle &#x200B;](/help/images/icons/data-add.png)**[!UICONTROL Activate]**&#x200B;activeren/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**&#x200B;controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![&#x200B; uitgeven detailcontrole &#x200B;](/help/images/icons/edit.png)**[!UICONTROL Edit details]**&#x200B;controle om [&#x200B; &#x200B;](update-accounts.md) de details van een bestaande bestemmingsrekening bij te werken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik de ![&#x200B; controle van de Schrapping &#x200B;](/help/images/icons/delete.png)**[!UICONTROL Delete]**&#x200B;controle [&#x200B; om &#x200B;](delete-destination-account.md) een bestaande bestemmingsrekening te schrappen.

![&#x200B; Rekeningen tabel &#x200B;](../assets/ui/workspace/accounts-tab.png)

| Element | Beschrijving |
|---|---|
| [!UICONTROL Name] | De naam u aan de bestemmingsrekening toewees terwijl [&#x200B; vestiging &#x200B;](connect-destination.md#authenticate) de bestemming. Selecteer de kolomkop voor toegang tot sorteeropties (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]** ). |
| [!UICONTROL Destination] | De bestemmingsschakelaar waarvoor u opstelling de verbinding hebt. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het type van rekeningsverbinding aan uw opslagemmer of bestemming. Afhankelijk van de bestemming, zijn de authentificatieopties: <ul><li>Voor e-mailmarketingbestemmingen: kan S3, FTP of Azure Blob zijn.</li><li>Voor reclame-bestemmingen in real time: Server-aan-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: basisverificatie voor SFTP</li><li>OAuth 1- of OAuth 2-verificatie</li><li>Toekennerverificatie</li></ul> |
| [!UICONTROL Username] | De gebruikersbenaming u in [&#x200B; selecteerde verbind bestemmingswerkschema &#x200B;](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsdataflows die met basisinformatie worden verbonden voor een bestemming worden gecreeerd. |
| [!UICONTROL Authorization date] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |
| [!UICONTROL Expiration date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br> Een waarschuwingspictogram ![&#x200B; Het waarschuwingspictogram voor verlopen account.](/help/images/icons/alert-expiration.png) wordt vóór de vervaldatum weergegeven om u te waarschuwen dat de verbinding verloopt en mogelijk moet worden vernieuwd. Gegevensstromen naar verlopen verbindingen worden gestopt en u moet opnieuw verifiëren om uw activeringsworkflows te hervatten. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor [&#x200B; Pinterest &#x200B;](../catalog/advertising/pinterest.md), [&#x200B; LinkedIn &#x200B;](../catalog/social/linkedin.md), en [&#x200B; LinkedIn Gelijke Publiek &#x200B;](../catalog/social/linkedin-b2b.md) verbindingen. <br> ![](../assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Filteraccounts {#filter-accounts}

Het tabblad **[!UICONTROL Accounts]** bevat verbeterde filtermogelijkheden en zoekmogelijkheden, zodat u uw doelaccounts snel kunt vinden en beheren. Gebruik de linkerzijbalk om filters toe te passen en de zoekbalk om specifieke accounts op naam te zoeken.

#### Zoeken naar accounts {#search-accounts}

Gebruik de zoekbalk boven aan de tabel om snel accounts op naam te zoeken. Terwijl u typt, worden de resultaten automatisch gefilterd om alleen overeenkomende accounts weer te geven.

![&#x200B; bar van het Onderzoek in de Rekeningen tabel.](../assets/ui/workspace/accounts-search.gif)

#### Filteropties {#filter-options-accounts}

Gebruik de filters in de linkerzijbalk om de zoekopdracht te beperken.

![&#x200B; de filters van de Rekening in het lusje van Rekeningen &#x200B;](../assets/ui/workspace/account-filters.png)

* **[!UICONTROL Destination platform]**: Filter accounts op specifieke doelplatforms (bijvoorbeeld: [!DNL Microsoft Bing] , [!DNL Amazon S3] , [!DNL Facebook Custom Audiences] , [!DNL LinkedIn Matched Audiences] , enzovoort). U kunt meerdere platforms tegelijk selecteren.
* **[!UICONTROL Created by]**: Filteraccounts van de gebruiker die ze heeft gemaakt. Gebruik dit filter om rekeningen te vinden die door specifieke teamleden worden gecreeerd.

#### Actieve filters {#active-filters-accounts}

Wanneer u filters toepast, worden deze weergegeven als tags onder de zoekbalk.

![&#x200B; Actieve filters die als markeringen in de Rekeningen tabel &#x200B;](../assets/ui/workspace/accounts-active-filters.png) worden getoond

Daar kunt u:

* Alle momenteel actieve filters weergeven
* Afzonderlijke filters verwijderen door op het pictogram `X` op elke filtertag te klikken
* Alle filters tegelijk wissen met de optie **[!UICONTROL Clear all]**

## [!UICONTROL System View] {#system-view}

Het tabblad **[!UICONTROL System View]** geeft een grafische weergave weer van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![&#x200B; gegevens-flows1 &#x200B;](../assets/ui/workspace/system-view-dataflows.png)

Selecteer een van de doelen die op de pagina worden weergegeven en klik op **[!UICONTROL View dataflows]** om informatie weer te geven over alle verbindingen die u voor elke bestemming hebt ingesteld.

![&#x200B; gegevens-flows2 &#x200B;](../assets/ui/workspace/system-view-dataflows-2.png)
