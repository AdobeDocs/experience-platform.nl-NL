---
title: Werkruimte Doelen
seo-title: Werkruimte Doelen
description: In het Platform van de Gegevens van de Klant van Adobe In real time, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
seo-description: In het Platform van de Gegevens van de Klant van Adobe In real time, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Werkruimte Doelen {#destinations-workspace}

Selecteer in Adobe Real-time Customer Data Platform **[!UICONTROL Destinations]** op de linkernavigatiebalk voor toegang tot de [!UICONTROL Destinations] werkruimte.

De [!UICONTROL Destinations] werkruimte bestaat uit vier secties, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]**, en **[!UICONTROL System View]**, die in de hieronder secties worden beschreven.

![Overzicht van bestemmingen](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

Op het **[!UICONTROL Catalog]** tabblad wordt een lijst weergegeven met alle door Adobe aangeboden doelen waarnaar u gegevens kunt verzenden.

Gebruik de onderzoeksfunctionaliteit op de pagina om van een specifieke bestemming of filterbestemmingen de plaats te bepalen gebruikend de **[!UICONTROL Categories]** controle.

Selecteer een bestemming in de catalogus om de rechterrail te openen. Hier, kunt u opstelling een verbinding aan de bestemming (**[!UICONTROL Connect destination]**), bestaande bestemmingsverbindingen (**[!UICONTROL Browse destinations]**) bekijken of meer gedetailleerde informatie over elke bestemming leren door de documentatie (**[!UICONTROL View documentation]**) te bekijken.

![Opties voor doelcatalogus](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie de Catalogus [van de](/help/rtcdp/destinations/destinations-catalog.md)Bestemming.

## [!UICONTROL Browse] {#browse}

Het **[!UICONTROL Browse]** lusje toont de bestemmingen waarmee u een verbinding hebt gevestigd. Doelen waarvoor de **[!UICONTROL enabled]** schakeloptie is ingeschakeld, stellen de bestemming in op actief en andersom. U kunt de bestemmingen ook bekijken waar u gegevens hebt die door een segment te selecteren **[!UICONTROL Segments > Browse]** en te selecteren stromen. Zie de lijst hieronder voor alle informatie die voor elke bestemming in het Browse lusje wordt verstrekt:

![Tabblad Bladeren](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschrijving |
---------|----------
| Naam | De naam die u hebt opgegeven voor de activeringsstroom naar dit doel. |
| [!UICONTROL Destination] | Het doelplatform dat u hebt geselecteerd voor de activeringsstroom. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li></ul> |
| [!UICONTROL Username] | De accountgegevens die u hebt geselecteerd voor de doelstroom. |
| [!UICONTROL Segments] | Het aantal segmenten dat aan deze bestemming wordt geactiveerd. |
| [!UICONTROL Created] | De datum en UTC-tijd waarop de activeringsstroom naar het doel is gemaakt. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of er momenteel gegevens op dit doel worden geactiveerd. Zie [Activering](/help/rtcdp/destinations/activate-destinations.md#disable-activation)uitschakelen om de status te bewerken. |

Klik op een doelrij om meer informatie over de bestemming in de juiste spoorstaaf te tonen.

![Doelrij klikken](/help/rtcdp/destinations/assets/click-destination-row.png)

Selecteer de doelnaam om informatie over de segmenten te zien die aan deze bestemming worden geactiveerd. Klik **[!UICONTROL Edit activation]** om te wijzigen of aan de segmenten toe te voegen die naar deze bestemming worden verzonden.

## [!UICONTROL Accounts] {#accounts}

In het **[!UICONTROL Accounts]** lusje, kunt u meer over de verbindingen leren die u met diverse bestemmingen hebt gevestigd. Zie de tabel hieronder voor alle informatie die u op elke bestemming kunt krijgen:

![Het tabblad Accounts](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschrijving |
---------|----------
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li><li>Voor Amazon S3 cloudopslagbestemmingen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: Basisverificatie voor SFTP</li></ul> |
| [!UICONTROL Username] | De gebruikersnaam die u in de [Connect-doelwizard](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)hebt geselecteerd. |
| [!UICONTROL Data Flows] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsstromen die met basisinformatie worden verbonden die voor een bestemming wordt gecreeerd. |
| [!UICONTROL Authorized] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of er momenteel gegevens op dit doel worden geactiveerd. Zie [Activering](/help/rtcdp/destinations/activate-destinations.md#disable-activation)uitschakelen om de status te bewerken. |

## [!UICONTROL System View] {#system-view}

Op het **[!UICONTROL System View]** tabblad ziet u een grafische weergave van de activeringsstromen die u hebt ingesteld in het Real-time Customer Data Platform.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en druk **[!UICONTROL View flows]** om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)