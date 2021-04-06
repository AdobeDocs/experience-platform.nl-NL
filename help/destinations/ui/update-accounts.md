---
keywords: Doelaccount bijwerken, doelaccounts
title: Doelaccounts bijwerken
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen voor het bijwerken van bestemmingsaccounts in de gebruikersinterface van Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Doelaccounts bijwerken

## Overzicht {#overview}

Het **[!UICONTROL Accounts]** lusje toont u details over de verbindingen die u met diverse bestemmingen hebt gevestigd. Zie de tabel hieronder voor alle informatie die u op elke bestemming kunt krijgen:

![Het tabblad Accounts](../assets/ui/update-accounts/destination-accounts.png)

| Element | Beschrijving |
|---|---|
| [!UICONTROL Platform] | Het doel waarvoor u de verbinding hebt ingesteld. |
| [!UICONTROL Connection Type] | Vertegenwoordigt het verbindingstype aan uw opslagemmer of bestemming. <ul><li>Voor e-mailmarketingdoelen: Kan S3 of FTP zijn.</li><li>Voor realtime advertentiebestemmingen: Server-naar-server</li><li>Voor Amazon S3-cloudopslagdoelen: Toegangstoets </li><li>Voor SFTP-cloudopslagdoelen: Basisverificatie voor SFTP</li></ul> |
| [!UICONTROL Username] | De gebruikersnaam die u hebt geselecteerd in [verbind bestemmingstovenaar](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Vertegenwoordigt het aantal unieke succesvolle bestemmingsstromen die met basisinformatie worden verbonden die voor een bestemming wordt gecreeerd. |
| [!UICONTROL Authorized] | De datum waarop de verbinding met deze bestemming werd geautoriseerd. |

## Accounts {#update} bijwerken

Voer de onderstaande stappen uit om verbindingsgegevens bij te werken naar bestaande doelen.

1. Meld u aan bij [Experience Platform UI](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteer **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![Het tabblad Accounts](../assets/ui/update-accounts/accounts-tab.png)

2. Selecteer het filterpictogram ![Filter-pictogram](../assets/ui/update-accounts/filter.png) linksboven om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![Filterdoelen](../assets/ui/update-accounts/filter-accounts.png)

3. Selecteer de knop ![Account bewerken](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** in de kolom **[!UICONTROL Platform]** om de accountgegevens te bewerken.

   ![Het tabblad Accounts](../assets/ui/update-accounts/accounts-edit.png)

4. Voer uw bijgewerkte accountgegevens in.

   * Voor accounts die een verbindingstype `OAuth2` gebruiken, selecteert u **[!UICONTROL Reconnect OAuth]** om uw accountgegevens te vernieuwen.

      ![Details OAuth bewerken](../assets/ui/update-accounts/edit-details-oauth.png)


   * Voor accounts die een verbindingstype `Access Key` of `ConnectionString` gebruiken, kunt u de verificatiegegevens van uw account bewerken, zoals toegang-id, geheime sleutels of verbindingstekenreeksen.

      ![Toegangstoets details bewerken](../assets/ui/update-accounts/edit-details-key.png)

5. Selecteer **[!UICONTROL Save]** om de aanmeldingsgegevens bij te werken.
