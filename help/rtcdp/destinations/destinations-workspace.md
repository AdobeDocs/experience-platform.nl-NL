---
keywords: RTCDP;rtcdp
title: Werkruimte Doelen
seo-title: Werkruimte Doelen
description: De werkruimte Doelen bestaat uit vier secties, Catalogus, Bladeren, Rekeningen, en de Mening van het Systeem, die in de hieronder secties worden beschreven.
seo-description: In het Platform van Gegevens van de Klant in real time, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
translation-type: tm+mt
source-git-commit: a3e35dee98b7b2758a4246a63bb0e1bde6b2f165
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---


# Werkruimte Doelen {#destinations-workspace}

In het Platform van Gegevens van de Klant in real time, uitgezochte **[!UICONTROL Doelen]** van de linkernavigatiebar om tot de werkruimte van [!UICONTROL Doelen] toegang te hebben.

De [!UICONTROL werkruimte van Doelen] bestaat uit vier secties, [!UICONTROL Catalogus], [!UICONTROL doorbladeren], [!UICONTROL Rekeningen], en de Mening [!UICONTROL van]het Systeem, die in de hieronder secties worden beschreven.

![Overzicht van bestemmingen](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalogus] {#catalog}

Op het tabblad **[!UICONTROL Catalogus]** wordt een lijst weergegeven met alle bestemmingen die beschikbaar zijn in CDP in real-time, waarnaar u gegevens kunt verzenden.

De gebruikersinterface in real time CDP verstrekt een aantal onderzoek en filteropties op de pagina van de bestemmingscatalogus:

* Gebruik de zoekfunctionaliteit op de pagina om een specifiek doel te zoeken.
* Doelen filteren met het besturingselement [!UICONTROL Categorieën] .
* Wissel tussen [!UICONTROL Alle bestemmingen] en [!UICONTROL Mijn bestemmingen]. Wanneer **[!UICONTROL Alle bestemmingen]** wordt geselecteerd, worden alle beschikbare bestemmingen in real time CDP getoond. Wanneer **[!UICONTROL Mijn bestemmingen]** wordt geselecteerd, kunt u slechts de bestemmingen zien waarmee u een verbinding hebt gevestigd.
* Selecteer deze optie om **[!UICONTROL verbindingen]** en/of **[!UICONTROL extensies]** weer te geven. Om het verschil tussen de twee categorieën te begrijpen, zie de Types en de Categorieën van [Bestemming](/help/rtcdp/destinations/destination-types.md).

![doelen filteren en zoeken, demo](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

De bestemmingskaarten bevatten of **[!UICONTROL vormen]** of een **[!UICONTROL Activate]** controle, en een secundaire controle die meer opties omhoog brengt. Deze worden allemaal hieronder beschreven:

| Control | Beschrijving |
---------|----------
| [!UICONTROL Configureren] | Hiermee kunt u verbinding maken met het doel. |
| [!UICONTROL Activeren] | Nadat u een verbinding met de bestemming hebt gemaakt, kunt u segmenten activeren. |
| [!UICONTROL Account weergeven] | Bekijk de accounts waarmee u verbinding hebt gemaakt voor een bestemming. |
| [!UICONTROL Gegevensstromen weergeven] | Bekijk de gegevensactiveringsstromen die voor een bestemming bestaan. |
| [!UICONTROL Documentatie weergeven] | Opent een verbinding aan de documentatiepagina voor die specifieke bestemming, voor meer informatie en om u te helpen opstelling het. |

![Controles op de bestemmingskaart](/help/rtcdp/destinations/assets/destination-card-options.png)

Selecteer een doelkaart in de catalogus om de rechterrail te openen.  Hier, kunt u een beschrijving van de bestemming zien. De rechterspoorstaaf bevat dezelfde besturingselementen als in de bovenstaande tabel, alsmede een beschrijving van de bestemming en een aanduiding van de categorie en het type van bestemming.

![Opties voor doelcatalogus](/help/rtcdp/destinations/assets/destination-right-rail.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie de Catalogus [van de](/help/rtcdp/destinations/destinations-catalog.md) Bestemming en de Types en de Categorieën [van](/help/rtcdp/destinations/destination-types.md)Bestemming.

## [!UICONTROL Accounts] {#accounts}

Op het tabblad **[!UICONTROL Accounts]** kunt u meer informatie krijgen over de verbindingen die u met verschillende doelen hebt gemaakt. Zie de tabel hieronder voor alle informatie die u op elke bestemming kunt krijgen:

>[!TIP]
>
>Gebruik de knop ![Gegevens](/help/rtcdp/destinations/assets/add-data-symbol.png) toevoegen in de kolom **[!UICONTROL Platform]** om een nieuwe doelverbinding voor die account te maken.

![Het tabblad Accounts](./assets/workspace/edit-account-destinations.png)

| Element | Beschrijving |
---------|----------
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Verbindingstype] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: Basisverificatie voor SFTP</li></ul> |
| [!UICONTROL Gebruikersnaam] | De gebruikersnaam die u in de [Connect-doelwizard](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)hebt geselecteerd. |
| [!UICONTROL Doelen] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsstromen die met basisinformatie worden verbonden die voor een bestemming wordt gecreeerd. |
| [!UICONTROL Geautoriseerd] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |

Bovendien kunt u uw accountgegevens bewerken of bijwerken. Selecteer de knop ![Account](./assets/workspace/pencil-icon.png) bewerken in de kolom **[!UICONTROL Platform]** om de accountgegevens te bewerken.

Voor accounts die een `OAuth2` verbindingstype gebruiken, kunt u OAuth **[!UICONTROL opnieuw verbinden selecteren]** om uw accountgegevens te vernieuwen.

![Oautische afbeelding](./assets/workspace/reconnect-oauth.png)

Voor accounts die een `Access Key` of `ConnectionString` verbindingstype gebruiken, kunt u de verificatiegegevens van uw account bewerken, zoals toegang-id, geheime sleutels of verbindingstekenreeksen.

![Afbeelding met accountgegevens](./assets/workspace/edit-account-details.png)

Als u klaar bent met het bewerken van uw accountgegevens, selecteert u **[!UICONTROL Opslaan]** om de update te voltooien.

## [!UICONTROL Bladeren] {#browse}

Op het tabblad **[!UICONTROL Bladeren]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt. Doelen met de **[!UICONTROL Toegelaten]** schakeloptie ingeschakeld plaatsen de bestemming aan actief en vice versa. U kunt de bestemmingen ook bekijken waar u gegevens hebt die door **[!UICONTROL Segmenten]** te selecteren > **[!UICONTROL doorbladeren]** en een te inspecteren segment te selecteren stromen. Zie de lijst hieronder voor alle informatie die voor elke bestemming in het Browse lusje wordt verstrekt:

>[!TIP]
>
>Gebruik de ![Add knoop](/help/rtcdp/destinations/assets/add-data-symbol.png) van Gegevens in de kolom van de **[!UICONTROL Naam]** om extra segmenten aan die bestemming te activeren.

![Tabblad Bladeren](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschrijving |
---------|----------
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. |
| [!UICONTROL Bestemming] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Verbindingstype] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li></ul> |
| [!UICONTROL Gebruikersnaam] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Segmenten] | Het aantal segmenten dat aan deze bestemming wordt geactiveerd. |
| [!UICONTROL Gemaakt] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of er momenteel gegevens op dit doel worden geactiveerd. Zie [Activering](/help/rtcdp/destinations/activate-destinations.md#disable-activation)uitschakelen om de status te bewerken. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf te tonen.

![Doelrij klikken](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecteer de doelnaam om informatie over de segmenten te zien die aan deze bestemming worden geactiveerd. Klik op Activering **** bewerken om de segmenten die naar dit doel worden verzonden, te wijzigen of aan te vullen.

## [!UICONTROL Systeemweergave] {#system-view}

Op het tabblad **[!UICONTROL Systeemweergave]** wordt een grafische weergave weergegeven van de activeringsstromen die u hebt ingesteld in het Platform Klantgegevens in realtime.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en druk de stromen **[!UICONTROL van de]** Mening om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)