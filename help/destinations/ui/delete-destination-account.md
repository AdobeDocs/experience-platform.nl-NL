---
keywords: bestemmingsaccount, bestemmingsaccounts verwijderen, accounts verwijderen
title: Doelaccounts verwijderen
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen die moeten worden gezet om bestemmingsaccounts te verwijderen in de gebruikersinterface van Adobe Experience Platform.
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---

# Doelaccounts verwijderen

## Overzicht {#overview}

De **[!UICONTROL Accounts]** het lusje toont u details over de verbindingen die u met diverse bestemmingen hebt gevestigd. Zie de [Overzicht van accounts](../ui/destinations-workspace.md#accounts) voor alle informatie u op elke bestemmingsrekening kunt krijgen.

Deze zelfstudie behandelt de stappen om bestemmingsrekeningen te schrappen die niet meer nodig zijn door het Experience Platform UI te gebruiken.

![Het tabblad Accounts](../assets/ui/update-accounts/destination-accounts.png)

## Accounts verwijderen {#delete}

>[!TIP]
>
>Voordat u de doelaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de doelaccount zijn gekoppeld. Raadpleeg de zelfstudie over het verwijderen van bestaande doelgegevensstromen [het schrappen van bestemmingsdataflows in UI](./delete-destinations.md).

Voer de onderstaande stappen uit om bestaande doelaccounts te verwijderen.

1. Aanmelden bij de [UI Experience Platform](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteren **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![Het tabblad Accounts](../assets/ui/delete-accounts/accounts-tab.png)

2. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/update-accounts/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![Filterdoelen](../assets/ui/delete-accounts/filter-accounts.png)

3. De ovalen selecteren (`...`) naast de naam van de account die u wilt verwijderen. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Activate segments]**, **[!UICONTROL Edit details]**, en **[!UICONTROL Delete]** de rekening. Selecteer ![Knop Verwijderen](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Delete]** om het gewenste account te verwijderen.

   ![Doelaccount verwijderen](../assets/ui/delete-accounts/delete-accounts.png)

4. Er verschijnt een laatste bevestigingsvenster. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![Verwijderen van account bevestigen](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de bestemmingswerkruimte gebruikt om bestaande rekeningen te schrappen.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, raadpleeg de zelfstudie op [verbindingen verwijderen met de Flow Service API](../api/delete-destination-account.md)
