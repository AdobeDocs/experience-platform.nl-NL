---
keywords: doelen verwijderen, bestemmingen verwijderen, doel verwijderen
title: Doelen verwijderen
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen waarmee een bestaand doel in de gebruikersinterface van Adobe Experience Platform kan worden verwijderd
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Doelen verwijderen {#delete-destinations}

## Overzicht {#overview}

In de Adobe Experience Platform-gebruikersinterface kunt u bestaande verbindingen met doelen verwijderen.

Als u een bestemming verwijdert, worden bestaande gegevensstromen naar die bestemming verwijderd. Alle publiek dat aan de bestemmingen wordt geactiveerd die u schrapt wordt unmapped alvorens dataflow wordt geschrapt.

Er zijn twee manieren waarop u doelen kunt verwijderen uit de map [!DNL Experience Platform] [!DNL UI] . U kunt:

* [Doelen verwijderen van het tabblad [!UICONTROL Browse]](#delete-browse-tab)
* [Doelen verwijderen van de pagina met bestemmingsdetails](#delete-destination-details-page)

## Doelen verwijderen op het tabblad Bladeren{#delete-browse-tab}

Voer de onderstaande stappen uit om een doel te verwijderen van het tabblad [!UICONTROL Browse] .

1. Login aan [ UI van Experience Platform ](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Browse]** in de bovenste koptekst om uw bestaande doelen weer te geven.

   ![ doorbladert bestemmingen ](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecteer het filterpictogram ![ filter-pictogram ](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![ bestemmingen van de Filter ](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer de ![ Meer knoop ](/help/images/icons/more.png) in de kolom van de Naam en selecteer dan ![ knoop van de Schrapping ](/help/images/icons/delete.png) **[!UICONTROL Delete]** om een bestaande bestemmingsverbinding te verwijderen.
   ![ schrapt bestemmingen ](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecteer **[!UICONTROL Delete]** om het verwijderen van de bestemmingsverbinding te bevestigen.

   ![ Bevestig schrappingsbestemming ](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Doelen verwijderen van de pagina met bestemmingsdetails{#delete-destination-details-page}

Voer de onderstaande stappen uit om een bestemming te verwijderen van de pagina met doeldetails.

1. Login aan [ UI van Experience Platform ](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Browse]** in de bovenste koptekst om uw bestaande doelen weer te geven.

   ![ doorbladert bestemmingen ](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecteer het filterpictogram ![ filter-pictogram ](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![ bestemmingen van de Filter ](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer de naam van het doel dat u wilt verwijderen.

   ![ Uitgezochte bestemming ](../assets/ui/delete-destinations/delete-destination-select.png)

   * Als de bestemming bestaande gegevensstromen heeft, wordt u genomen aan [!UICONTROL Dataflow runs] tabel.

     ![ de looppas van Dataflow lusje ](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Als het doel geen bestaande gegevensstromen heeft, wordt u genomen aan een lege pagina waar u het publiek kunt beginnen te activeren.

     ![ de details van de Bestemming ](../assets/ui/delete-destinations/destination-details-empty.png)

4. Selecteer **[!UICONTROL Delete]** in de rechtertrack.

   ![ doel van de Schrapping ](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecteer **[!UICONTROL Delete]** in het bevestigingsdialoogvenster om het doel te verwijderen.

   ![ de bestemming van de Schrapping bevestigt ](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Afhankelijk van het laden van de server kan het enkele minuten duren voordat [!DNL Experience Platform] het doel heeft verwijderd.
