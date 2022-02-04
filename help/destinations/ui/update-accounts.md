---
keywords: bestemmingsaccount bijwerken, bestemmingsaccounts, accounts bijwerken, doel bijwerken
title: Doelaccounts bijwerken
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen voor het bijwerken van bestemmingsaccounts in de gebruikersinterface van Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Doelaccounts bijwerken

## Overzicht {#overview}

De **[!UICONTROL Accounts]** het lusje toont u details over de verbindingen die u met diverse bestemmingen hebt gevestigd. Zie de [Overzicht van accounts](../ui/destinations-workspace.md#accounts) voor alle informatie u op elke bestemmingsrekening kunt krijgen.

Deze zelfstudie behandelt de stappen om de details van de bestemmingsrekening bij te werken door het Experience Platform UI te gebruiken.

U kunt de details van de bestemmingsrekening bijwerken om geloofsbrieven voor uw huidige of verlopen rekeningen voor bestemmingen te verfrissen en opnieuw voor authentiek te verklaren u momenteel gebruikt. Typisch, hebben OAuth en dragertokens een beperkt leven, afhankelijk van het bestemmingsplatform. Wanneer deze tokens verlopen, kunt u ze in de hieronder beschreven workflow vernieuwen. Deze workflow geeft u de opdracht de OAuth-workflow te doorlopen of een token opnieuw in te voegen. Op dezelfde manier als een wachtwoord of gebruikerstoegang in het stroomafwaartse platform zijn veranderd, kunt u geloofsbrieven verfrissen.

Voor batchbestemmingen kunt u de toegang of de geheime sleutel bijwerken als een van deze wijzigingen is gewijzigd. Als u uw bestanden verder wilt coderen, kunt u bovendien een openbare RSA-sleutel invoegen en worden uw geëxporteerde bestanden vervolgens versleuteld.

![Het tabblad Accounts](../assets/ui/update-accounts/destination-accounts.png)

## Accounts bijwerken {#update}

Voer de onderstaande stappen uit om verbindingsgegevens bij te werken naar bestaande doelen.

1. Aanmelden bij de [UI Experience Platform](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteren **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![Het tabblad Accounts](../assets/ui/update-accounts/accounts-tab.png)

2. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/update-accounts/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![Bestemmingsaccounts filteren](../assets/ui/update-accounts/filter-accounts.png)

3. De ovalen selecteren (`...`) naast de naam van de account die u wilt bijwerken. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Activate segments]**, **[!UICONTROL Edit details]**, en **[!UICONTROL Delete]** de rekening. Selecteer ![Knop Details bewerken](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit details]** om de accountgegevens te bewerken.

   ![Account bewerken](../assets/ui/update-accounts/accounts-edit.png)

4. Voer uw bijgewerkte accountgegevens in.

   * Voor accounts die een `OAuth1` of `OAuth2` verbindingstype, selecteren **[!UICONTROL Reconnect OAuth]** om uw accountgegevens te vernieuwen. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![Details OAuth bewerken](../assets/ui/update-accounts/edit-details-oauth.png)

   * Voor accounts die een `Access Key` of `ConnectionString` van het verbindingstype, kunt u uw informatie van de rekeningsauthentificatie, met inbegrip van informatie zoals toegangs identiteitskaart, geheime sleutels, of verbindingskoorden uitgeven. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![Toegangstoets details bewerken](../assets/ui/update-accounts/edit-details-key.png)

   * Voor accounts die een `Bearer token` verbindingstype, kunt u een nieuw dragertoken invoeren, indien nodig. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![Token details van drager bewerken](../assets/ui/update-accounts/edit-details-bearer.png)

   * Voor accounts die een `Server to server` verbindingstype kunt u de naam en beschrijving van uw account bijwerken.

   ![Details van server naar server bewerken](../assets/ui/update-accounts/edit-details-s2s.png)

5. Selecteren **[!UICONTROL Save]** om de update van de accountdetails te voltooien.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht **[!UICONTROL destinations]** werkruimte om bestaande accounts bij te werken.

Voor meer informatie over bestemmingen, verwijs naar [Overzicht van doelen](../catalog/overview.md).