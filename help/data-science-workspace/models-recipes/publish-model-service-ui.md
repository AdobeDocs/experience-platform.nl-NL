---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Een model publiceren als service (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 7dc5075d3101b4780af92897c0381e73a9c5aef0
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Een model publiceren als service (UI)

De Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform staat u toe om uw opgeleid en geëvalueerd Model als Dienst te publiceren, toelatend gebruikers binnen uw organisatie IMS om gegevens te scoren zonder de behoefte om hun eigen Modellen te creëren.

## Aan de slag

Voor het voltooien van deze zelfstudie hebt u toegang tot [!DNL Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], neemt u contact op met uw systeembeheerder voordat u verdergaat.

Voor deze zelfstudie is een bestaand model met een geslaagde trainingsuitvoering vereist. Als u geen publiceerbaar model hebt, volgt u de [training en evalueert u een model in de zelfstudie voor de gebruikersinterface](./train-evaluate-model-ui.md) voordat u verdergaat.

Raadpleeg de [API-zelfstudie](./publish-model-service-api.md)als u een model wilt publiceren met gebruik van API&#39;s voor leren door Sensei-machines.

## Een model publiceren {#publish-a-model}

1. Klik in Adobe Experience Platform op de koppeling **[!UICONTROL Modellen]** in de linkernavigatiekolom om alle bestaande modellen weer te geven. Zoek en klik op de naam van het model dat als service moet worden gepubliceerd.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Klik op **[!UICONTROL Publiceren]** in de rechterbovenhoek van de overzichtspagina Model om een serviceproces te starten.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Voer een gewenste naam voor de service in en geef desgewenst een servicebeschrijving op en klik op **[!UICONTROL Volgende]** als u klaar bent.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Alle geslaagde trainingen voor het model worden weergegeven. De nieuwe Dienst zal training en het scoren configuraties van de geselecteerde trainingslooppas erven.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Klik op **[!UICONTROL Voltooien]** om de service te maken en omleiding naar de **[!UICONTROL servicegalerie]** om alle beschikbare services weer te geven, inclusief de zojuist gemaakte service.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Score met een service {#access-a-service}

1. Klik in Adobe Experience Platform op het tabblad **[!UICONTROL Services]** in de linkernavigatiekolom voor toegang tot de *servicegalerie*. Zoek de service die u wilt gebruiken en klik op **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selecteer een aangewezen inputdataset voor de het scoren looppas, dan klik **[!UICONTROL daarna]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selecteer een geschikte uitvoerdataset voor de het scoren resultaten, dan klik **[!UICONTROL daarna]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Wanneer een Dienst wordt gecreeerd, erft het gebrek die configuraties scoring. U kunt deze configuraties bekijken en deze naar wens aanpassen door op de waarden te dubbelklikken. Als u tevreden bent met de configuraties, klikt u op **[!UICONTROL Voltooien]** om de scoring uit te voeren.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Op de *overzichtspagina* van de Dienst, worden de details van de nieuwe het scoren baan en zijn vooruitgang getoond. Nadat de taak is voltooid, wordt de **[!UICONTROL meest recente]** scores-taak bijgewerkt.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een Model als toegankelijke Dienst gepubliceerd, en gegevens die de nieuwe Dienst door de Galerij *van de* Dienst worden gescoord. Ga verder met de volgende zelfstudie om te leren hoe u geautomatiseerde training en scoring op een service [kunt](./schedule-models-ui.md)plannen.
