---
keywords: bestemmingsaccount, bestemmingsaccounts verwijderen, accounts verwijderen
title: Doelaccounts verwijderen
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen die moeten worden gezet om bestemmingsaccounts te verwijderen in de gebruikersinterface van Adobe Experience Platform.
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Doelaccounts verwijderen

## Overzicht {#overview}

Op het tabblad **[!UICONTROL Accounts]** ziet u details over de verbindingen die u hebt gemaakt met verschillende doelen. Verwijs naar het [ overzicht van Rekeningen ](../ui/destinations-workspace.md#accounts) voor alle informatie u op elke bestemmingsrekening kunt krijgen.

Deze zelfstudie behandelt de stappen om bestemmingsrekeningen te schrappen die niet meer nodig zijn door het Experience Platform UI te gebruiken.

![ Rekeningen tabel ](../assets/ui/update-accounts/destination-accounts.png)

## Accounts verwijderen {#delete}

>[!TIP]
>
>Voordat u de doelaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de doelaccount zijn gekoppeld. Om bestaande bestemmingsdataflows te schrappen, verwijs naar het leerprogramma bij [ het schrappen van bestemmingsdataflows in UI ](./delete-destinations.md).

Voer de onderstaande stappen uit om bestaande doelaccounts te verwijderen.

1. Login aan het [ Experience Platform UI ](https://platform.adobe.com/) en selecteert **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![ Rekeningen tabel ](../assets/ui/delete-accounts/accounts-tab.png)

2. Selecteer het filterpictogram ![ filter-pictogram ](../assets/ui/update-accounts/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![ bestemmingen van de Filter ](../assets/ui/delete-accounts/filter-accounts.png)

3. Selecteer de ovalen (`...`) naast de naam van de account die u wilt verwijderen. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Activate audiences]** , **[!UICONTROL Edit details]** en **[!UICONTROL Delete]** de account. Selecteer de ![ knoop van de Schrapping ](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Delete]** knoop om de gewenste rekening te schrappen.

   ![ de bestemmingsrekening van de Schrapping ](../assets/ui/delete-accounts/delete-accounts.png)

4. Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![ Bevestig rekeningsschrapping ](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de bestemmingswerkruimte gebruikt om bestaande rekeningen te schrappen.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, te verwijzen gelieve naar het leerprogramma op [ het schrappen van verbindingen gebruikend de Dienst API van de Stroom ](../api/delete-destination-account.md)
