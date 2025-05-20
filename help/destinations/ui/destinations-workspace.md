---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;bestemmingscatalogus;
title: Werkruimte Doelen
description: De werkruimte van Doelen bestaat uit vijf secties, Overzicht, Catalogus, doorbladeren, Rekeningen, en de Mening van het Systeem. Deze worden in de onderstaande secties beschreven.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '1175'
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

De gebruikersinterface van [!DNL Experience Platform] biedt verschillende zoek- en filteropties op de pagina met de doelcatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Filter doelen met het besturingselement [!UICONTROL Categories] .
* Schakelen tussen [!UICONTROL All destinations] en [!UICONTROL My destinations] . Wanneer u **[!UICONTROL All destinations]** selecteert, worden alle beschikbare [!DNL Experience Platform] -doelen weergegeven. Wanneer u **[!UICONTROL My destinations]** selecteert, kunt u alleen de doelen zien waarmee u een verbinding hebt gemaakt.
* Selecteer deze optie om de typen **[!UICONTROL Connections]** en/of **[!UICONTROL Extensions]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, lees [ de Types en de Categorieën van Bestemming ](../destination-types.md).

![ catalogus van Doelen die een paar reclame en wolkenopslagbestemmingen tonen.](../assets/ui/workspace/catalog.png)

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

## [!UICONTROL Accounts] {#accounts}

Op het tabblad **[!UICONTROL Accounts]** vindt u meer informatie over de verbindingen die u hebt gemaakt met verschillende doelen. Bovendien kunt u bestaande accountgegevens bijwerken of verwijderen. Zie de tabel hieronder voor alle informatie die u op elke doelaccount kunt krijgen.

>[!TIP]
>
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![ controle ](/help/images/icons/data-add.png)**[!UICONTROL Activate]**activeren/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik ![ uitgeven detailcontrole ](/help/images/icons/edit.png)**[!UICONTROL Edit details]**controle om [ ](update-accounts.md) de details van een bestaande bestemmingsrekening bij te werken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Platform] kolom en gebruik de ![ controle van de Schrapping ](/help/images/icons/delete.png)**[!UICONTROL Delete]**controle [ om ](delete-destination-account.md) een bestaande bestemmingsrekening te schrappen.

![ Rekeningen tabel ](../assets/ui/workspace/destination-account-options.png)

| Element | Beschrijving |
|---|---|
| [!UICONTROL Destination] | De bestemmingsschakelaar waarvoor u opstelling de verbinding hebt. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het type van rekeningsverbinding aan uw opslagemmer of bestemming. Afhankelijk van de bestemming, zijn de authentificatieopties: <ul><li>Voor e-mailmarketingbestemmingen: kan S3, FTP of Azure Blob zijn.</li><li>Voor reclame-bestemmingen in real time: Server-aan-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: basisverificatie voor SFTP</li><li>OAuth 1- of OAuth 2-verificatie</li><li>Toekennerverificatie</li></ul> |
| [!UICONTROL Username] | De gebruikersbenaming u in [ selecteerde verbind bestemmingswerkschema ](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsdataflows die met basisinformatie worden verbonden voor een bestemming worden gecreeerd. |
| [!UICONTROL Authorization date] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |
| [!UICONTROL Expiration date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor de [ verbinding van Facebook ](../catalog/social/facebook.md). |

{style="table-layout:auto"}

## [!UICONTROL Browse] {#browse}

Op het tabblad **[!UICONTROL Browse]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt. Doelen waarvoor de schakeloptie **[!UICONTROL Enabled/Disabled]** is ingeschakeld, stellen het doel in op respectievelijk actief of inactief. U kunt ook de doelen weergeven waar de gegevens stromen door **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** te selecteren en een publiek te selecteren dat moet worden geïnspecteerd. Zie de tabel hieronder voor alle informatie die voor elke bestemming wordt opgegeven op het tabblad [!UICONTROL Browse] :

>[!TIP]
>
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ activeer de controle van het publiek ](/help/images/icons/data-add.png)**[!UICONTROL Activate]**controle om publiek of datasets naar die bestemming uit te voeren.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![ controle van de Schrapping ](/help/images/icons/delete.png)**[!UICONTROL Delete]**controle [ om ](delete-destinations.md) een bestaande verbinding aan een bestemming te verwijderen.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik de ![ Mening in controle ](/help/images/icons/monitoring.png)**[!UICONTROL View in monitoring]**controle om activeringsinformatie voor deze bestemming in het [ controledashboard ](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) te bekijken.
> * Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ Abonneren aan alarm ](/help/images/icons/alert-add.png)**[!UICONTROL Subscribe to alerts]**controle om aan bestemmingdataflow alarm in te tekenen. U kunt zich op alarm intekenen om berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. Zie [ aan in-context bestemmingsalarm ](alerts.md) voor gedetailleerde informatie over bestemmingdataflow alarm abonneren.

![ doorbladert Lusje ](../assets/ui/workspace/browse-tab.png)

| Element | Beschrijving |
|---------|----------|
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. Dezelfde kolom bevat twee besturingselementen: [!UICONTROL Activate] en [!UICONTROL Delete destination] . |
| Gegevenstype | Het type gegevens dat wordt ondersteund door de doelverbinding. Ondersteunde gegevenstypen: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | De status van de laatste gegevensstroomuitvoering. Zie [ de bestemmingsdetails van de Mening ](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Last Dataflow Run Date] | Tijd en datum waarop de laatste dataflow-run heeft plaatsgevonden. Zie [ de bestemmingsdetails van de Mening ](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Account Expiration Date] | De datum waarop de verbindingsvergunning aan deze bestemming zal verlopen. <br>**Belangrijk**: Deze kolom is momenteel beschikbaar slechts voor de [ verbinding van Facebook ](../catalog/social/facebook.md). |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor marketingdoelen voor e-mail: Kan S3, FTP of [!DNL Azure Blob] zijn.</li><li>Voor reclame-bestemmingen in real time: server-aan-server.</li><li>Voor streamingdoelen: kan [!DNL Azure Event Hubs] of [!DNL Amazon Kinesis] zijn.</li></ul> |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activation Data] | Geeft het aantal soorten publiek aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement om meer te weten te komen over het geactiveerde publiek. Verwijs naar [ Gegevens van de Activering ](/help/destinations/ui/destination-details-page.md#activation-data) in de pagina van bestemmingsdetails voor meer informatie over het geactiveerde publiek. |
| [!UICONTROL Created] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. Selecteer het pijl-omhoog/pijl-omlaag om de activeringsstromen eerst op de nieuwste of eerst op de oudste te sorteren. |
| [!UICONTROL Status] | `Enabled` of `Disabled` . Geeft aan of gegevens op dit doel worden geactiveerd. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf, zoals bestemmings identiteitskaart, beschrijving, het aantal geactiveerde doelsoorten, en meer te tonen.

![ klik bestemmingsrij ](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over het publiek te zien dat aan deze bestemming wordt geactiveerd. Klik op **[!UICONTROL Edit activation]** om het publiek dat naar dit doel wordt verzonden, te wijzigen of er aan toe te voegen.

## [!UICONTROL System View] {#system-view}

Het tabblad **[!UICONTROL System View]** geeft een grafische weergave weer van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![ gegevens-flows1 ](../assets/ui/workspace/data-flows1.png)

Selecteer een van de doelen die op de pagina worden weergegeven en klik op **[!UICONTROL View dataflows]** om informatie weer te geven over alle verbindingen die u voor elke bestemming hebt ingesteld.

![ gegevens-flows2 ](../assets/ui/workspace/data-flows2.png)
