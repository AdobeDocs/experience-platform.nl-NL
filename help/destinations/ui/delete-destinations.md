---
keywords: doelen verwijderen, bestemmingen verwijderen, doel verwijderen
title: Doelen verwijderen
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen waarmee een bestaand doel in de gebruikersinterface van Adobe Experience Platform kan worden verwijderd
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Doelen verwijderen {#delete-destinations}

## Overzicht {#overview}

In de Adobe Experience Platform-gebruikersinterface kunt u bestaande verbindingen met doelen verwijderen.

Als u een bestemming verwijdert, worden bestaande gegevensstromen naar die bestemming verwijderd. Alle segmenten die aan de bestemmingen worden geactiveerd die u schrapt worden unmapped alvorens dataflow wordt geschrapt.

Er zijn twee manieren u bestemmingen van kunt schrappen [!DNL Platform] [!DNL UI]. U kunt:

* [Doelen verwijderen uit het dialoogvenster [!UICONTROL Browse] tab](#delete-browse-tab)
* [Doelen verwijderen van de pagina met bestemmingsdetails](#delete-destination-details-page)

## Doelen verwijderen op het tabblad Bladeren{#delete-browse-tab}

Voer de onderstaande stappen uit om een doel te verwijderen uit de [!UICONTROL Browse] tab.

1. Aanmelden bij de [UI Experience Platform](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Om uw bestaande bestemmingen te bekijken, selecteer **[!UICONTROL Browse]** in de bovenste koptekst.

   ![Bladeren door doelen](../assets/ui/delete-destinations/browse-destinations.png)

2. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/delete-destinations/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer ![Meer, knop](../assets/ui/delete-destinations/more-icon.png) in de kolom Naam en selecteer vervolgens ![Knop Verwijderen](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** om een bestaande doelverbinding te verwijderen.
   ![Doelen verwijderen](../assets/ui/delete-destinations/delete-destinations.png)

4. Selecteren **[!UICONTROL Delete]** om de verwijdering van de bestemmingsverbinding te bevestigen.

   ![Doel verwijderen bevestigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Doelen verwijderen van de pagina met bestemmingsdetails{#delete-destination-details-page}

Voer de onderstaande stappen uit om een bestemming te verwijderen van de pagina met doeldetails.

1. Aanmelden bij de [UI Experience Platform](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Om uw bestaande bestemmingen te bekijken, selecteer **[!UICONTROL Browse]** in de bovenste koptekst.

   ![Bladeren door doelen](../assets/ui/delete-destinations/browse-destinations.png)

2. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/delete-destinations/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/delete-destinations/filter-destinations.png)

3. Selecteer de naam van het doel dat u wilt verwijderen.

   ![Doel selecteren](../assets/ui/delete-destinations/delete-destination-select.png)

   * Als de bestemming bestaande gegevensstromen heeft, wordt u genomen aan [!UICONTROL Dataflow runs] tab.

      ![Tabblad DataFlow-uitvoering](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Als het doel geen bestaande gegevensstromen heeft, wordt u genomen aan een lege pagina waar u het publiek kunt beginnen te activeren.

      ![Doelgegevens](../assets/ui/delete-destinations/destination-details-empty.png)

4. Selecteren **[!UICONTROL Delete]** in het rechterspoor.

   ![Doel verwijderen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Selecteren **[!UICONTROL Delete]** in het bevestigingsdialoogvenster om het doel te verwijderen.

   ![Doel bevestigen verwijderen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Afhankelijk van het laden van de server kan het enkele minuten duren [!DNL Platform] om het doel te verwijderen.
