---
title: Werkruimte Doelen
seo-title: Werkruimte Doelen
description: In het Platform van de Gegevens van de Klant van Adobe in real time, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
seo-description: In het Platform van de Gegevens van de Klant van Adobe in real time, uitgezochte Doelen van de linkernavigatiebar om tot de bestemmingswerkruimte toegang te hebben.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 2%

---


# Werkruimte Doelen {#destinations-workspace}

In het Platform van de Gegevens van de Klant van Adobe in real time, uitgezochte **[!UICONTROL Doelen]** van de linkernavigatiebar om tot de werkruimte van [!UICONTROL Doelen] toegang te hebben.

De [!UICONTROL werkruimte van Doelen] bestaat uit vier secties, **[!UICONTROL Catalogus]**, **[!UICONTROL doorbladeren]**, **[!UICONTROL Rekeningen]**, en de Mening **[!UICONTROL van]** het Systeem, die in de hieronder secties worden beschreven.

![Overzicht van bestemmingen](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalogus] {#catalog}

Op het tabblad **[!UICONTROL Catalogus]** wordt een lijst weergegeven met alle doelen die door Adobe worden aangeboden en waarnaar u gegevens kunt verzenden.

Gebruik de onderzoeksfunctionaliteit op de pagina om van een specifieke bestemming of filterbestemmingen de plaats te bepalen gebruikend de controle van **[!UICONTROL Categorieën]** .

Selecteer een bestemming in de catalogus om de rechterrail te openen. Hier, kunt u opstelling een verbinding aan de bestemming (**[!UICONTROL verbind bestemming]**), bestaande bestemmingsverbindingen (**[!UICONTROL doorbladert bestemmingen]**) bekijken of meer gedetailleerde informatie over elke bestemming leren door de documentatie (de documentatie **[!UICONTROL van de]** Mening) te bekijken.

![Opties voor doelcatalogus](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Voor meer informatie over bestemmingscategorieën en informatie over elke bestemming, zie de Catalogus [van de](/help/rtcdp/destinations/destinations-catalog.md)Bestemming.

## [!UICONTROL Bladeren] {#browse}

Op het tabblad **[!UICONTROL Bladeren]** worden de doelen weergegeven waarmee u een verbinding hebt gemaakt. Doelen waarvoor de **[!UICONTROL ingeschakelde]** schakeloptie is ingeschakeld, stellen de bestemming in op actief en andersom. U kunt de bestemmingen ook bekijken waar u gegevens hebt die door **[!UICONTROL Segmenten]** te selecteren > **[!UICONTROL doorbladeren]** en een te inspecteren segment te selecteren stromen. Zie de lijst hieronder voor alle informatie die voor elke bestemming in het Browse lusje wordt verstrekt:

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

## [!UICONTROL Accounts] {#accounts}

Op het tabblad **[!UICONTROL Accounts]** kunt u meer informatie krijgen over de verbindingen die u met verschillende doelen hebt gemaakt. Zie de tabel hieronder voor alle informatie die u op elke bestemming kunt krijgen:

![Het tabblad Accounts](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschrijving |
---------|----------
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Verbindingstype] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: Basisverificatie voor SFTP</li></ul> |
| [!UICONTROL Gebruikersnaam] | De gebruikersnaam die u in de [Connect-doelwizard](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)hebt geselecteerd. |
| [!UICONTROL Gegevensstromen] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsstromen die met basisinformatie worden verbonden die voor een bestemming wordt gecreeerd. |
| [!UICONTROL Geautoriseerd] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |
| [!UICONTROL Status] | `Active` of `Inactive`. Geeft aan of er momenteel gegevens op dit doel worden geactiveerd. Zie [Activering](/help/rtcdp/destinations/activate-destinations.md#disable-activation)uitschakelen om de status te bewerken. |

## [!UICONTROL Systeemweergave] {#system-view}

Op het tabblad **[!UICONTROL Systeemweergave]** wordt een grafische weergave weergegeven van de activeringsstromen die u hebt ingesteld in het Platform Klantgegevens in realtime.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selecteer om het even welke bestemmingen die op de pagina worden getoond en druk de stromen **[!UICONTROL van de]** Mening om informatie over alle verbindingen te zien u opstelling voor elke bestemming hebt.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)