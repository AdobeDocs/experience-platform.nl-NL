---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;bestemmingscatalogus;
title: Werkruimte Doelen
description: De werkruimte van Doelen bestaat uit vijf secties, Overzicht, Catalogus, doorbladeren, Rekeningen, en de Mening van het Systeem. Deze worden in de onderstaande secties beschreven.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Experience Platform **[!UICONTROL Destinations]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Destinations] werkruimte.

De [!UICONTROL Destinations] de werkruimte bestaat uit vijf secties, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts], en [!UICONTROL System View], zoals beschreven in de onderstaande punten.

![Het dashboard met het overzicht van bestemmingen bevat drie widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

De **[!UICONTROL Overview]** tabblad geeft het tabblad [!UICONTROL Destinations] dashboard, dat belangrijke metriek verstrekt met betrekking tot de bestemmingsgegevens van uw organisatie. Ga voor meer informatie naar de [[!UICONTROL Destinations] dashboardhulplijn](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Als uw organisatie nieuw aan Experience Platform is en nog geen actieve bestemmingen heeft, [!UICONTROL Destinations] dashboard en [!UICONTROL Overview] zijn niet zichtbaar. In plaats daarvan selecteert u [!UICONTROL Destinations] van de linkernavigatie toont de [[!UICONTROL Catalog] tab](#catalog).

![Het tabblad Overzicht van het dashboard Doelen.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

De **[!UICONTROL Catalog]** tabblad geeft een lijst weer met alle bestemmingen die beschikbaar zijn in [!DNL Platform], waarnaar u gegevens kunt verzenden.

De [!DNL Platform] De gebruikersinterface verstrekt verscheidene onderzoek en filteropties op de pagina van de bestemmingscatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Doelen filteren met de opdracht [!UICONTROL Categories] controle.
* Schakelen tussen [!UICONTROL All destinations] en [!UICONTROL My destinations]. Wanneer u **[!UICONTROL All destinations]**, alle beschikbare [!DNL Platform] doelen worden weergegeven. Wanneer u **[!UICONTROL My destinations]**, kunt u alleen de doelen zien waarmee u een verbinding hebt gemaakt.
* Selecteer deze optie om de **[!UICONTROL Connections]** en/of **[!UICONTROL Extensions]** typen. Als u het verschil tussen de twee categorieën wilt begrijpen, leest u [Doeltypen en -categorieën](../destination-types.md).

![De catalogus van bestemmingen die een paar reclame en wolkenopslagbestemmingen toont.](../assets/ui/workspace/catalog.png)

De bestemmingskaarten bevatten primaire en secundaire controleopties. De primaire besturingselementen omvatten: [!UICONTROL Set up], [!UICONTROL Activate], [!UICONTROL Activate audiences], of [!UICONTROL Export datasets]. Met de secundaire besturingselementen kunt u opties weergeven. Deze besturingselementen worden hieronder beschreven:

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

![Controles op de bestemmingskaart](../assets/ui/workspace/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen. Hier, kunt u een beschrijving van de bestemming zien. De spoorstaaf rechts bevat dezelfde bedieningsorganen als in de bovenstaande tabel, met inbegrip van een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![Opties voor doelcatalogus](../assets/ui/workspace/destination-right-rail.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie [Doelcatalogus](../catalog/overview.md) en [Doeltypen en -categorieën](../destination-types.md).

## [!UICONTROL Accounts] {#accounts}

De **[!UICONTROL Accounts]** bevat details over de verbindingen die u hebt gemaakt met verschillende doelen en waarmee u bestaande accountgegevens kunt bijwerken of verwijderen. Zie de tabel hieronder voor alle informatie die u op elke doelaccount kunt krijgen.

>[!TIP]
>
> * De ovaal selecteren (`...`) in de [!UICONTROL Platform] en gebruikt u de ![Besturingselement activeren ](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate]**/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**controle om het publiek of de datasets naar die bestemming uit te voeren.
> * De ovaal selecteren (`...`) in de [!UICONTROL Platform] en gebruikt u de ![Detailbesturingselement bewerken ](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Edit details]**controle op [update](update-accounts.md) de details van een bestaande bestemmingsrekening.
> * De ovaal selecteren (`...`) in de [!UICONTROL Platform] en gebruikt u de ![Besturingselement verwijderen ](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete]**controle op [delete](delete-destination-account.md) een bestaande bestemmingsrekening.

![Het tabblad Accounts](../assets/ui/workspace/destination-account-options.png)

| Element | Beschrijving |
|---|---|
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het type van rekeningsverbinding aan uw opslagemmer of bestemming. Afhankelijk van de bestemming, zijn de authentificatieopties: <ul><li>Voor e-mailmarketingbestemmingen: kan S3, FTP of Azure Blob zijn.</li><li>Voor reclame-bestemmingen in real time: Server-aan-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: basisverificatie voor SFTP</li><li>OAuth 1- of OAuth 2-verificatie</li><li>Toekennerverificatie</li></ul> |
| [!UICONTROL Username] | De gebruikersnaam die u in het dialoogvenster [wizard Verbinding maken](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsdataflows die met basisinformatie worden verbonden voor een bestemming worden gecreeerd. |
| [!UICONTROL Authorized] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |

{style="table-layout:auto"}

## [!UICONTROL Browse] {#browse}

De **[!UICONTROL Browse]** toont de bestemmingen waarmee u een verbinding hebt gevestigd. Doelen met de **[!UICONTROL Enabled/Disabled]** Schakel het inschakelen in om de bestemming in te stellen op respectievelijk actief of inactief. U kunt de bestemmingen ook bekijken waar u gegevens hebt die door te selecteren stromen **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** en een publiek selecteren om te inspecteren. Zie de tabel hieronder voor alle informatie die voor elke bestemming wordt verstrekt in het dialoogvenster [!UICONTROL Browse] tab:

>[!TIP]
>
> * De ovaal selecteren (`...`) in de [!UICONTROL Name] en gebruikt u de ![Besturingselement voor publiek activeren ](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate]**controle om het publiek of de datasets naar die bestemming uit te voeren.
> * De ovaal selecteren (`...`) in de [!UICONTROL Name] en gebruikt u de ![Besturingselement verwijderen ](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete]**controle op [remove](delete-destinations.md) een bestaande verbinding met een doel.
> * De ovaal selecteren (`...`) in de [!UICONTROL Name] en gebruikt u de ![Weergeven in controle ](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL View in monitoring]**besturingselement voor weergave van activeringsinformatie voor deze bestemming in het dialoogvenster [controledashboard](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * De ovaal selecteren (`...`) in de [!UICONTROL Name] en gebruikt u de ![Abonneren op waarschuwingen ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Subscribe to alerts]**controle om aan bestemmingdataflow alarm in te schrijven. U kunt zich op alarm intekenen om berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. Zie [Abonneren op in-context-bestemmingswaarschuwingen](alerts.md) voor gedetailleerde informatie over waarschuwingen over bestemmingsgegevensstroom.

![Tabblad Bladeren](../assets/ui/workspace/browse-tab.png)

| Element | Beschrijving |
|---------|----------|
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. Dezelfde kolom bevat twee besturingselementen: [!UICONTROL Activate] en [!UICONTROL Delete destination]. |
| [!UICONTROL Last Flow Run Status] | De status van de laatste gegevensstroomuitvoering. Zie [Doelgegevens weergeven](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Last Flow Run Date] | Tijd en datum waarop de laatste dataflow-run heeft plaatsgevonden. Zie [Doelgegevens weergeven](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor marketingdoelen voor e-mail: Kan zijn: S3, FTP of [!DNL Azure Blob].</li><li>Voor reclame-bestemmingen in real time: server-aan-server.</li><li>Voor streamingdoelen: kan [!DNL Azure Event Hubs] of [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activation Data] | Geeft het aantal soorten publiek aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement om meer te weten te komen over het geactiveerde publiek. Zie [Activeringsgegevens](/help/destinations/ui/destination-details-page.md#activation-data) in de pagina met doeldetails voor meer informatie over het geactiveerde publiek. |
| [!UICONTROL Created] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. Selecteer het pijl-omhoog/pijl-omlaag om de activeringsstromen eerst op de nieuwste of eerst op de oudste te sorteren. |
| [!UICONTROL Status] | `Enabled` of `Disabled`. Geeft aan of gegevens op dit doel worden geactiveerd. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf te tonen.

![Doelrij klikken](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over het publiek te zien dat aan deze bestemming wordt geactiveerd. Klikken **[!UICONTROL Edit activation]** om het publiek te wijzigen of toe te voegen dat naar deze bestemming wordt verzonden.

## [!UICONTROL System View] {#system-view}

De **[!UICONTROL System View]** wordt een grafische weergave weergegeven van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en klik **[!UICONTROL View dataflows]** om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Data-flows2](../assets/ui/workspace/data-flows2.png)
