---
keywords: Experience Platform;publiceer een model;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;score een dienst
solution: Experience Platform
title: Publiceer een Model als Dienst in de Werkruimte van de Wetenschap van Gegevens UI
topic: tutorial
type: Tutorial
description: Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.
translation-type: tm+mt
source-git-commit: 13fa4af388c6f31768a6b7e1da05cb56c5635c9e
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---


# Publiceer een model als dienst in de Werkruimte van de Wetenschap van Gegevens UI

Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang tot een Organisatie IMS in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Voor deze zelfstudie is een bestaand model met een geslaagde trainingsuitvoering vereist. Als u geen publiceerbaar Model hebt, volg [Trein en evalueer een Model in UI](./train-evaluate-model-ui.md) leerprogramma alvorens verder te gaan.

Als u liever een model publiceert met API&#39;s voor Sensei Machine Learning, raadpleegt u de [API-zelfstudie](./publish-model-service-api.md).

## Model {#publish-a-model} publiceren

Selecteer in Adobe Experience Platform **[!UICONTROL Models]** in de linkernavigatiekolom en selecteer vervolgens het tabblad **[!UICONTROL Browse]** om alle bestaande modellen weer te geven. Selecteer de naam van het model dat u als service wilt publiceren.

![](../images/models-recipes/publish-model/browse_model.png)

Selecteer **[!UICONTROL Publish]** in de rechterbovenhoek van de overzichtspagina Model om een proces voor het maken van de service te starten.

![](../images/models-recipes/publish-model/view_training.png)

Voer een gewenste naam voor de service in en geef desgewenst een servicebeschrijving en selecteer **[!UICONTROL Next]** als u klaar bent.

![](../images/models-recipes/publish-model/configure_training.png)

Alle geslaagde trainingen voor het model worden weergegeven. De nieuwe Dienst zal training en het scoren configuraties van de geselecteerde trainingslooppas erven.

![](../images/models-recipes/publish-model/select_training_run.png)

Selecteer **[!UICONTROL Finish]** om de service te maken en omleiding naar **[!UICONTROL Service Gallery]** om alle beschikbare services weer te geven, inclusief de nieuwe service.

![](../images/models-recipes/publish-model/service_gallery.png)

## Score met een service {#access-a-service}

Selecteer in Adobe Experience Platform de tab **[!UICONTROL Services]** in de linkernavigatiekolom voor toegang tot **[!UICONTROL Service Gallery]**. Zoek de service die u wilt gebruiken en selecteer **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Selecteer **[!UICONTROL Score]** op de pagina met het serviceoverzicht.

![](../images/models-recipes/publish-model/score_service.png)

Selecteer een aangewezen inputdataset voor de het scoren looppas, dan uitgezocht **[!UICONTROL Next]**. U wordt gevraagd om de zelfde stap voor de het scoren dataset te doen. Zodra u de input en outputdataset hebt geselecteerd, kunt u de configuraties bijwerken.

![](../images/models-recipes/publish-model/select_datasets.png)

Wanneer een Dienst wordt gecreeerd, erft het gebrek die configuraties scoring. U kunt deze configuraties bekijken en deze naar wens aanpassen door op de waarden te dubbelklikken. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Finish]** om de scoring te starten.

![](../images/models-recipes/publish-model/scoring_configs.png)

Op de pagina **Overzicht** van de Dienst, worden de details van de nieuwe het scoren baan en zijn vooruitgang getoond. Nadat de taak is voltooid, wordt de **[!UICONTROL Most Recent]**-koptekst in de container **[!UICONTROL Scoring]** bijgewerkt.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een Model als toegankelijke Dienst gepubliceerd, en gegevens gesorteerd gebruikend de nieuwe Dienst door [!UICONTROL Service Gallery]. Ga verder met de volgende zelfstudie om te leren hoe u geautomatiseerde training en scoring kunt plannen op een Service](./schedule-models-ui.md).[
