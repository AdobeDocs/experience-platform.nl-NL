---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;doelcatalogus;
title: Werkruimte Doelen
description: De werkruimte van Doelen bestaat uit vier secties, Catalogus, doorbladeren, Rekeningen, en de Mening van het Systeem. Deze worden in de onderstaande secties beschreven.
seo-description: In Adobe Experience Platform, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Experience Platform **[!UICONTROL Destinations]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Destinations] te openen.

De werkruimte [!UICONTROL Destinations] bestaat uit vijf secties, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts], en [!UICONTROL System View], die in de hieronder secties worden beschreven.

![Overzicht van bestemmingen](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

Op het tabblad **[!UICONTROL Overview]** wordt het dashboard [!UICONTROL Destinations] weergegeven, met daarin belangrijke meetgegevens voor de doelgegevens van uw organisatie. Voor meer informatie gaat u naar de [[!UICONTROL Destinations] dashboardgids](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Als uw organisatie nieuw aan Experience Platform is en nog geen actieve bestemmingen heeft, zijn [!UICONTROL Destinations] dashboard en [!UICONTROL Overview] tabel niet zichtbaar. Als u in plaats daarvan [!UICONTROL Destinations] selecteert in de linkernavigatie, wordt [[!UICONTROL Catalog] tab](#catalog) weergegeven.

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

Het **[!UICONTROL Catalog]** lusje toont een lijst van alle bestemmingen beschikbaar in [!DNL Platform], die u gegevens kunt verzenden naar.

De [!DNL Platform] gebruikersinterface verstrekt verscheidene onderzoek en filteropties op de pagina van de bestemmingscatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* De bestemmingen van de filter gebruikend [!UICONTROL Categories] controle.
* Schakelen tussen [!UICONTROL All destinations] en [!UICONTROL My destinations]. Wanneer u **[!UICONTROL All destinations]** selecteert, worden alle beschikbare [!DNL Platform] bestemmingen getoond. Wanneer u **[!UICONTROL My destinations]** selecteert, kunt u slechts de bestemmingen zien waarmee u een verbinding hebt gevestigd.
* Selecteer deze optie om **[!UICONTROL Connections]** en/of **[!UICONTROL Extensions]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, zie [De Types van Bestemming en Categorieën](../destination-types.md).

![doelen filteren en zoeken, demo](../assets/ui/workspace/destinations-search-and-filter.gif)

De bestemmingskaarten bevatten of een **[!UICONTROL Configure]** of **[!UICONTROL Activate]** controle, en een secundaire controle die meer opties omhoog brengt. Deze besturingselementen worden hieronder beschreven:

| Control | Beschrijving |
|---------|----------|
| [!UICONTROL Configure] | Hiermee kunt u verbinding maken met het doel. |
| [!UICONTROL Activate] | Nadat u een verbinding met de bestemming hebt gemaakt, kunt u segmenten activeren. |
| [!UICONTROL View account] | Bekijk de accounts waarmee u verbinding hebt gemaakt voor een bestemming. |
| [!UICONTROL View dataflows] | Bekijk de gegevensactiveringsstromen die voor een bestemming bestaan. |
| [!UICONTROL View documentation] | Opent een verbinding aan de documentatiepagina voor die specifieke bestemming, voor meer informatie en om u te helpen opstelling het. |

{style=&quot;table-layout:auto&quot;}

![Controles op de bestemmingskaart](../assets/ui/workspace/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen. Hier, kunt u een beschrijving van de bestemming zien. De spoorstaaf rechts bevat dezelfde bedieningsorganen als in de bovenstaande tabel, met inbegrip van een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![Opties voor doelcatalogus](../assets/ui/workspace/destination-right-rail.png)

Zie [Doelcatalogus](../catalog/overview.md) en [Doeltypen en -categorieën](../destination-types.md) voor meer informatie over doelcategorieën en informatie over elke bestemming.

## [!UICONTROL Accounts] {#accounts}

Het **[!UICONTROL Accounts]** lusje toont u details over de verbindingen die u met diverse bestemmingen hebt gevestigd, en staat u toe om bestaande verbindingsdetails bij te werken. Zie [Accounts bijwerken](update-accounts.md) voor gedetailleerde instructies.

## [!UICONTROL Browse] {#browse}

Op het tabblad **[!UICONTROL Browse]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt. Doelen waarvoor de schakeloptie **[!UICONTROL Enabled/Disabled]** is ingeschakeld, stellen de bestemming respectievelijk in op actief of inactief. U kunt de bestemmingen ook bekijken waar u gegevens door **[!UICONTROL Segments]** > **[!UICONTROL Browse]** te selecteren en een segment te inspecteren hebt. Zie de lijst hieronder voor alle informatie die voor elke bestemming in het Browse lusje wordt verstrekt:

>[!TIP]
>
> * Gebruik ![Add segmentknoop](../assets/ui/workspace/add-data-symbol.png) in **[!UICONTROL Name]** kolom om segmenten naar die bestemming te verzenden.
> * Gebruik ![de knoop van bestemmingen ](../assets/ui/workspace/delete-destination-symbol.png) in **[!UICONTROL Name]** kolom aan [delete](delete-destinations.md) een bestaande verbinding aan een bestemming.


![Tabblad Bladeren](../assets/ui/workspace/browse-tab.png)

| Element | Beschrijving |
|---------|----------|
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. Dezelfde kolom bevat twee besturingselementen: [!UICONTROL Activate ] en [!UICONTROL Delete destination]. |
| [!UICONTROL Last Flow Run Status] | De status van de laatste gegevensstroom die wordt uitgevoerd. Zie [De bestemmingsdetails van de Mening](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Last Flow Run Date] | Tijd en datum waarop de laatste dataflow-run heeft plaatsgevonden. Zie [De bestemmingsdetails van de Mening](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3, FTP of [!DNL Azure Blob] zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server.</li><li>Voor streamingdoelen: Kan [!DNL Azure Event Hubs] of [!DNL Amazon Kinesis] zijn.</li></ul> |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activation Data] | Geeft het aantal segmenten aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement voor meer informatie over de geactiveerde segmenten. Raadpleeg [Activeringsgegevens](/help/destinations/ui/destination-details-page.md#activation-data) op de pagina met doeldetails voor meer informatie over de geactiveerde segmenten. |
| [!UICONTROL Created] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of gegevens op dit doel worden geactiveerd. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf te tonen.

![Doelrij klikken](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over de segmenten te zien die aan deze bestemming worden geactiveerd. Klik **[!UICONTROL Edit activation]** om te wijzigen of aan de segmenten toe te voegen die naar deze bestemming worden verzonden.

## [!UICONTROL System View] {#system-view}

Het tabblad **[!UICONTROL System View]** geeft een grafische weergave weer van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![Gegevensstromen1](../assets/ui/workspace/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en klik **[!UICONTROL View flows]** om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Gegevensstromen2](../assets/ui/workspace/data-flows2.png)
