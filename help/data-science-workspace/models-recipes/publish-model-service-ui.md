---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Een model publiceren als service (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Een model publiceren als service (UI)

Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze hun eigen modellen hoeven te maken.

Dit leerprogramma doorloopt de stappen om een Model als Dienst te publiceren, en score gegevens gebruikend de Dienst door de Galerie *van de* Dienst. Het is opgedeeld in de volgende hoofdsecties:

- [Een model publiceren](#publish-a-model)
- [Score met een service](#access-a-service)

## Aan de slag

Als u deze zelfstudie wilt voltooien, hebt u toegang nodig tot Experience Platform. Als u geen toegang tot een IMS Organisatie in het Platform van de Ervaring hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Voor deze zelfstudie is een bestaand model met een geslaagde trainingsuitvoering vereist. Als u geen publiceerbaar model hebt, volgt u de [training en evalueert u een model in de zelfstudie voor de gebruikersinterface](./train-evaluate-model-ui.md) voordat u verdergaat.

Raadpleeg de [API-zelfstudie](./publish-model-service-api.md)als u een model wilt publiceren met gebruik van API&#39;s voor leren door Sensei-machines.

## Een model publiceren {#publish-a-model}

1. Klik in het Adobe Experience Platform op de **[!UICONTROL Models]** koppeling in de linkernavigatiekolom om alle bestaande modellen weer te geven. Zoek en klik op de naam van het model dat als service moet worden gepubliceerd.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Klik **[!UICONTROL Publish]** dichtbij het hoogste recht van de Model overzichtspagina om een proces van de verwezenlijking van de Dienst te beginnen.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Voer een gewenste naam voor de service in en geef desgewenst een servicebeschrijving op en klik **[!UICONTROL Next]** wanneer u klaar bent.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Alle geslaagde trainingen voor het model worden weergegeven. De nieuwe Dienst zal training en het scoren configuraties van de geselecteerde trainingslooppas erven.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Klik **[!UICONTROL Finish]** om de Dienst tot stand te brengen en aan te leiden **[!UICONTROL Service Gallery]** om alle beschikbare Diensten, met inbegrip van de pas gecreëerde Dienst te tonen.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Score met een service {#access-a-service}

1. Klik in Adobe Experience Platform op het **[!UICONTROL Services]** tabblad in de linkernavigatiekolom voor toegang tot de *servicegalerie*. Zoek de service die u wilt gebruiken en klik op **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selecteer een aangewezen inputdataset voor de scoring looppas, dan klik **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selecteer een geschikte uitvoerdataset voor de het scoren resultaten, dan klik **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Wanneer een Dienst wordt gecreeerd, erft het gebrek die configuraties scoring. U kunt deze configuraties bekijken en deze naar wens aanpassen door op de waarden te dubbelklikken. Als u tevreden bent met de configuraties, klikt u **[!UICONTROL Finish]** om de scoring uit te voeren.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Op de *overzichtspagina* van de Dienst, worden de details van de nieuwe het scoren baan en zijn vooruitgang getoond. Nadat de taak is voltooid, wordt de **[!UICONTROL Most Recent]** scoretaak bijgewerkt.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een Model als toegankelijke Dienst gepubliceerd, en gegevens die de nieuwe Dienst door de Galerij *van de* Dienst worden gescoord. Ga verder met de volgende zelfstudie om te leren hoe u geautomatiseerde training en scoring op een service [kunt](./schedule-models-ui.md)plannen.
