---
keywords: Experience Platform;publiceer een model;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;score een dienst
solution: Experience Platform
title: Publiceer een Model als Dienst in de Werkruimte van de Wetenschap van Gegevens UI
topic: tutorial
type: Tutorial
description: Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Publiceer een model als dienst in de Werkruimte van de Wetenschap van Gegevens UI

Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang tot een Organisatie IMS in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Voor deze zelfstudie is een bestaand model met een geslaagde trainingsuitvoering vereist. Als u geen publiceerbaar Model hebt, volg [Trein en evalueer een Model in UI](./train-evaluate-model-ui.md) leerprogramma alvorens verder te gaan.

Als u liever een model publiceert met API&#39;s voor Sensei Machine Learning, raadpleegt u de [API-zelfstudie](./publish-model-service-api.md).

## Model {#publish-a-model} publiceren

1. Klik in Adobe Experience Platform op de koppeling **[!UICONTROL Modellen]** in de linkernavigatiekolom om alle bestaande modellen weer te geven. Zoek en klik op de naam van het model dat als service moet worden gepubliceerd.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Klik op **[!UICONTROL Publiceren]** rechtsboven in de pagina Modeloverzicht om een serviceproces te starten.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Voer een gewenste naam voor de service in en geef desgewenst een servicebeschrijving op en klik op **[!UICONTROL Volgende]** als u klaar bent.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Alle geslaagde trainingen voor het model worden weergegeven. De nieuwe Dienst zal training en het scoren configuraties van de geselecteerde trainingslooppas erven.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Klik op **[!UICONTROL Voltooien]** om de service te maken en omleiden naar de **[!UICONTROL Servicegalerie]** om alle beschikbare services weer te geven, inclusief de nieuwe service.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Score met een service {#access-a-service}

1. Klik in Adobe Experience Platform op het tabblad **[!UICONTROL Services]** in de linkernavigatiekolom voor toegang tot de **[!UICONTROL Servicegalerie]**. Zoek de service die u wilt gebruiken en klik op **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selecteer een aangewezen inputdataset voor de het scoren looppas, dan klik **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selecteer een geschikte uitvoerdataset voor de het scoren resultaten, dan klik **[!UICONTROL Volgende]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Wanneer een Dienst wordt gecreeerd, erft het gebrek die configuraties scoring. U kunt deze configuraties bekijken en deze naar wens aanpassen door op de waarden te dubbelklikken. Als u tevreden bent met de configuraties, klikt u op **[!UICONTROL Voltooien]** om de scoring te starten.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Op de pagina **Overzicht** van de Dienst, worden de details van de nieuwe het scoren baan en zijn vooruitgang getoond. Nadat de taak is voltooid, wordt de **[!UICONTROL Meest recente]**-header in de **[!UICONTROL Scoring]**-container bijgewerkt.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een Model als toegankelijke Dienst gepubliceerd, en gegevens gesorteerd gebruikend de nieuwe Dienst door [!UICONTROL de Galerij van de Dienst]. Ga verder met de volgende zelfstudie om te leren hoe u geautomatiseerde training en scoring kunt plannen op een Service](./schedule-models-ui.md).[
