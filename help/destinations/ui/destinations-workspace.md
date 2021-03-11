---
keywords: platform;bestemmingen;bestemmingswerkruimte;werkruimte;ui;bestemmingen ui;catalogus;doelcatalogus;
title: Overzicht van de werkruimte Doelen
description: De werkruimte Doelen bestaat uit vier secties, Catalogus, Bladeren, Rekeningen, en de Mening van het Systeem, die in de hieronder secties worden beschreven.
seo-description: In Adobe Experience Platform, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
translation-type: tm+mt
source-git-commit: 95ff15b212e0d6f454f0319ac1ec5bbee9c07dac
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# Overzicht van de werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Experience Platform **[!UICONTROL Doelen]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Doelen] te openen.

De werkruimte [!UICONTROL Doelen] bestaat uit vier secties, [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts], en [!UICONTROL System View], die in de volgende secties worden beschreven.

![Overzicht van bestemmingen](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catalogus] {#catalog}

Het **[!UICONTROL lusje van de Catalogus]** toont een lijst van alle bestemmingen beschikbaar in Platform, dat u gegevens kunt verzenden naar.

De gebruikersinterface van het Platform verstrekt een aantal onderzoek en filteropties op de pagina van de bestemmingscatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Doelen filteren met het besturingselement [!UICONTROL Categorieën].
* Wissel tussen [!UICONTROL Alle bestemmingen] en [!UICONTROL Mijn bestemmingen]. Wanneer **[!UICONTROL Alle bestemmingen]** wordt geselecteerd, worden alle beschikbare Platforms bestemmingen getoond. Wanneer **[!UICONTROL Mijn bestemmingen]** wordt geselecteerd, kunt u slechts de bestemmingen zien waarmee u een verbinding hebt gevestigd.
* Selecteer deze optie om **[!UICONTROL Verbindingen]** en/of **[!UICONTROL Extensies]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, zie [De Types van Bestemming en Categorieën](../destination-types.md).

![doelen filteren en zoeken, demo](../assets/ui/workspace/destinations-search-and-filter.gif)

De bestemmingskaarten bevatten of een **[!UICONTROL Configure]** of een **[!UICONTROL Activate]** controle, en een secundaire controle die meer opties omhoog brengt. Deze worden allemaal hieronder beschreven:

| Control | Beschrijving |
---------|----------
| [!UICONTROL Configureren] | Hiermee kunt u verbinding maken met het doel. |
| [!UICONTROL Activeren] | Nadat u een verbinding met de bestemming hebt gemaakt, kunt u segmenten activeren. |
| [!UICONTROL Account weergeven] | Bekijk de accounts waarmee u verbinding hebt gemaakt voor een bestemming. |
| [!UICONTROL Gegevensstromen weergeven] | Bekijk de gegevensactiveringsstromen die voor een bestemming bestaan. |
| [!UICONTROL Documentatie weergeven] | Opent een verbinding aan de documentatiepagina voor die specifieke bestemming, voor meer informatie en om u te helpen opstelling het. |

![Controles op de bestemmingskaart](../assets/ui/workspace/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen.  Hier, kunt u een beschrijving van de bestemming zien. De rechterspoorstaaf bevat dezelfde besturingselementen als in de bovenstaande tabel, alsmede een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![Opties voor doelcatalogus](../assets/ui/workspace/destination-right-rail.png)

Zie [Doelcatalogus](../catalog/overview.md) en [Doeltypen en -categorieën](../destination-types.md) voor meer informatie over doelcategorieën en informatie over elke bestemming.

## [!UICONTROL Accounts] {#accounts}

Op **[!UICONTROL Accounts]** lusje, kunt u meer over de verbindingen leren die u met diverse bestemmingen hebt gevestigd. Zie de tabel hieronder voor alle informatie die u op elke bestemming kunt krijgen:

>[!TIP]
>
>Gebruik de ![knop Gegevens toevoegen](../assets/ui/workspace/add-data-symbol.png) in de kolom **[!UICONTROL Platform]** om een nieuwe doelverbinding voor die account te maken.

![Het tabblad Accounts](../assets/ui/workspace/edit-account-destinations.png)

| Element | Beschrijving |
---------|----------
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Verbindingstype] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: Basisverificatie voor SFTP</li></ul> |
| [!UICONTROL Gebruikersnaam] | De gebruikersnaam die u hebt geselecteerd in [verbind bestemmingstovenaar](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Doelen] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsstromen die met basisinformatie worden verbonden die voor een bestemming wordt gecreeerd. |
| [!UICONTROL Geautoriseerd] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |

Bovendien kunt u uw accountgegevens bewerken of bijwerken. Selecteer de ![knop Account bewerken](../assets/ui/workspace/pencil-icon.png) in de kolom **[!UICONTROL Platform]** om de accountgegevens te bewerken.

Voor accounts die een verbindingstype `OAuth2` gebruiken, kunt u **[!UICONTROL OAuth]** opnieuw verbinden selecteren om uw accountgegevens te vernieuwen.

![Oautische afbeelding](../assets/ui/workspace/reconnect-oauth.png)

Voor accounts die een verbindingstype `Access Key` of `ConnectionString` gebruiken, kunt u de verificatiegegevens van uw account bewerken, zoals toegang-id, geheime sleutels of verbindingstekenreeksen.

![Afbeelding met accountgegevens](../assets/ui/workspace/edit-account-details.png)

Als u klaar bent met het bewerken van uw accountgegevens, selecteert u **[!UICONTROL Opslaan]** om de update te voltooien.

## [!UICONTROL Bladeren] {#browse}

Het **[!UICONTROL Browse]** lusje toont de bestemmingen waarmee u een verbinding hebt gevestigd. Doelen met de **[!UICONTROL Ingeschakelde]** schakeloptie ingeschakeld zetten de bestemming in op actief en vice versa. U kunt de bestemmingen ook bekijken waar u gegevens door **[!UICONTROL Segmenten]** > **[!UICONTROL Bladeren]** te selecteren en een segment te inspecteren selecteert. Zie de lijst hieronder voor alle informatie die voor elke bestemming in het Browse lusje wordt verstrekt:

>[!TIP]
>
> * Gebruik ![Voeg segmenten toe knoop](../assets/ui/workspace/add-data-symbol.png) in **[!UICONTROL Naam]** kolom om extra segmenten aan die bestemming te activeren.
> * Gebruik de ![knop Doelen verwijderen](../assets/ui/workspace/delete-destination-symbol.png) in de kolom **[!UICONTROL Naam]** om een bestaande verbinding naar een doel te verwijderen.


![Tabblad Bladeren](../assets/ui/workspace/browse-tab.png)

| Element | Beschrijving |
---------|----------
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. Dezelfde kolom bevat twee besturingselementen: [!UICONTROL Activeer ] en [!UICONTROL Verwijder doel]. |
| Status van laatste flowuitvoering | De status van de laatste gegevensstroom die wordt uitgevoerd. Zie [De bestemmingsdetails van de Mening](destination-details-page.md) voor meer informatie over dataflow looppas. |
| Datum van laatste Flow-uitvoering | Tijd en datum waarop de laatste dataflow-run plaatsvond. Zie [De bestemmingsdetails van de Mening](destination-details-page.md) voor meer informatie over dataflow looppas. |
| [!UICONTROL Bestemming] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Verbindingstype] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3, FTP of [!DNL Azure Blob] zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server.</li><li>Voor streamingdoelen: Kan [!DNL Azure Event Hubs] of [!DNL Amazon Kinesis] zijn.</li></ul> |
| [!UICONTROL Gebruikersnaam] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Activeringsgegevens] | Geeft het aantal segmenten aan dat op dit doel wordt geactiveerd. Selecteer dit besturingselement voor meer informatie over de geactiveerde segmenten. Raadpleeg [Activeringsgegevens](/help/destinations/ui/destination-details-page.md#activation-data) op de pagina met doeldetails voor meer informatie over de geactiveerde segmenten. |
| [!UICONTROL Gemaakt] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of er momenteel gegevens op dit doel worden geactiveerd. Zie [Activering uitschakelen](./activate-destinations.md#disable-activation) om de status te bewerken. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf te tonen.

![Doelrij klikken](../assets/ui/workspace/click-destination-row.png)

Selecteer de doelnaam om informatie over de segmenten te zien die aan deze bestemming worden geactiveerd. Klik **[!UICONTROL Activering bewerken]** om de segmenten die naar deze bestemming worden verzonden, te wijzigen of aan de segmenten toe te voegen.

## [!UICONTROL Systeemweergave] {#system-view}

Op het tabblad **[!UICONTROL Systeemweergave]** wordt een grafische weergave weergegeven van de activeringsstromen die u hebt ingesteld in de Adobe Experience Platform.

![Gegevensstromen1](../assets/ui/workspace/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en druk **[!UICONTROL de stromen van de Mening]** om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Gegevensstromen2](../assets/ui/workspace/data-flows2.png)