---
keywords: bestemmingen schrappen; hoe te om bestemmingen te schrappen
title: Doelen verwijderen
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen waarmee een bestaand doel in de gebruikersinterface van Adobe Experience Platform kan worden verwijderd
translation-type: tm+mt
source-git-commit: ebe2a35e66b78acf6a9ffa20664877913cd35648
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Doelen {#delete-destinations} verwijderen

## Overzicht {#overview}

In de Adobe Experience Platform-gebruikersinterface kunt u bestaande verbindingen met doelen verwijderen.

Als u een bestemming verwijdert, worden bestaande gegevensstromen naar die bestemming verwijderd. Alle segmenten die aan de bestemmingen worden geactiveerd die u schrapt worden unmapped alvorens dataflow wordt geschrapt.

Er zijn twee manieren u bestemmingen van [!DNL Platform] [!DNL UI] kunt schrappen. U kunt:

* [Doelen van het  [!UICONTROL Browse] tabblad verwijderen](#delete-browse-tab)
* [Doelen verwijderen van de pagina met bestemmingsdetails](#delete-destination-details-page)

## Doelen verwijderen van het tabblad Bladeren{#delete-browse-tab}

Voer de onderstaande stappen uit om een doel te verwijderen uit het tabblad [!UICONTROL Browse].

1. Meld u aan bij [Experience Platform UI](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk. Om uw bestaande bestemmingen te bekijken, selecteer **[!UICONTROL Browse]** van de hoogste kopbal.

   ![Bladeren door doelen](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecteer het filterpictogram ![Filter-pictogram](../assets/ui/delete-destinations/filter.png) linksboven om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer de ![knop Verwijderen](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** in de kolom **[!UICONTROL Platform]** om een bestaand doel te verwijderen.
   ![Doelen verwijderen](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecteer **[!UICONTROL Delete]** om de verwijdering van de bestemming te bevestigen.

   ![Doel verwijderen bevestigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Doelen verwijderen uit de pagina met doeldetails{#delete-destination-details-page}

Voer de onderstaande stappen uit om een bestemming te verwijderen van de pagina met doeldetails.

1. Meld u aan bij [Experience Platform UI](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk. Om uw bestaande bestemmingen te bekijken, selecteer **[!UICONTROL Browse]** van de hoogste kopbal.

   ![Bladeren door doelen](../assets/ui/delete-destinations/browse-destinations.png)

2. Selecteer het filterpictogram ![Filter-pictogram](../assets/ui/delete-destinations/filter.png) linksboven om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer de naam van het doel dat u wilt verwijderen.

   ![Doel selecteren](../assets/ui/delete-destinations/delete-destination-select.png)

   * Als de bestemming bestaande gegevensstromen heeft, wordt u genomen aan [!UICONTROL Dataflow runs] tabel.

      ![Tabblad DataFlow-uitvoering](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Als het doel geen bestaande gegevensstromen heeft, wordt u genomen aan een lege pagina waar u het publiek kunt beginnen te activeren.

      ![Doelgegevens](../assets/ui/delete-destinations/destination-details-empty.png)


4. Selecteer **[!UICONTROL Delete]** in het juiste spoor.

   ![Doel verwijderen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecteer **[!UICONTROL Delete]** in de bevestigingsdialoog om de bestemming te verwijderen.

   ![Doel bevestigen verwijderen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Afhankelijk van het laden van de server kan het enkele minuten duren voordat [!DNL Platform] het doel heeft verwijderd.