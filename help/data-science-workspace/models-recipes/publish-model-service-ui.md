---
keywords: Experience Platform;publiceer een model;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;score een dienst
solution: Experience Platform
title: Publiceer een Model als Dienst in de Werkruimte van de Wetenschap van Gegevens UI
type: Tutorial
description: Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Publiceer een model als dienst in de Werkruimte van de Wetenschap van Gegevens UI

Met de Adobe Experience Platform Data Science Workspace kunt u uw getrainde en geëvalueerde Model als service publiceren, zodat gebruikers binnen uw organisatie gegevens kunnen scoren zonder dat ze zelf modellen hoeven te maken.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.

Voor deze zelfstudie is een bestaand model met een geslaagde trainingsuitvoering vereist. Als u geen publiceerbaar model hebt, voert u de opdracht [Een model trainen en evalueren in de gebruikersinterface](./train-evaluate-model-ui.md) zelfstudie voordat u verdergaat.

Als u een model liever wilt publiceren met de API&#39;s voor leren door Sensei Machine Learning, raadpleegt u de [API-zelfstudie](./publish-model-service-api.md).

## Een model publiceren {#publish-a-model}

Selecteer in Adobe Experience Platform **[!UICONTROL Models]** bevindt zich in de linkernavigatiekolom en selecteert u vervolgens de optie **[!UICONTROL Browse]** om alle bestaande modellen weer te geven. Selecteer de naam van het model dat u als service wilt publiceren.

![](../images/models-recipes/publish-model/browse_model.png)

Selecteren **[!UICONTROL Publish]** in de buurt van de rechterbovenhoek van de pagina Modeloverzicht om een proces voor het maken van services te starten.

![](../images/models-recipes/publish-model/view_training.png)

Voer een gewenste naam voor de service in en geef desgewenst een servicebeschrijving op en selecteer **[!UICONTROL Next]** wanneer gereed.

![](../images/models-recipes/publish-model/configure_training.png)

Alle geslaagde trainingen voor het model worden weergegeven. De nieuwe Dienst zal training en het scoren configuraties van de geselecteerde trainingslooppas erven.

![](../images/models-recipes/publish-model/select_training_run.png)

Selecteren **[!UICONTROL Finish]** om de dienst tot stand te brengen en aan **[!UICONTROL Service Gallery]** om alle beschikbare Diensten, met inbegrip van de pas gecreëerde Dienst te tonen.

![](../images/models-recipes/publish-model/service_gallery.png)

## Score met een service {#access-a-service}

Selecteer in Adobe Experience Platform de optie **[!UICONTROL Services]** tabblad in de linkernavigatiekolom voor toegang tot de **[!UICONTROL Service Gallery]**. Zoek de service die u wilt gebruiken en selecteer **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Selecteer in de pagina met het serviceoverzicht de optie **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Selecteer een geschikte gegevensset voor de scoring-run en selecteer vervolgens **[!UICONTROL Next]**. U wordt gevraagd om de zelfde stap voor de het scoren dataset te doen. Zodra u de input en outputdataset hebt geselecteerd, kunt u de configuraties bijwerken.

![](../images/models-recipes/publish-model/select_datasets.png)

Wanneer een Dienst wordt gecreeerd, erft het gebrek die configuraties scoring. U kunt deze configuraties bekijken en deze naar wens aanpassen door op de waarden te dubbelklikken. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Finish]** om de scoring te starten.

![](../images/models-recipes/publish-model/scoring_configs.png)

Op de service **Overzicht** pagina, worden details van de nieuwe scoretaak en de voortgang ervan weergegeven. Als de taak is voltooid, wordt de opdracht **[!UICONTROL Most Recent]** koptekst in de **[!UICONTROL Scoring]** container wordt bijgewerkt.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een Model als toegankelijke Dienst gepubliceerd, en gegevens gescoord gebruikend de nieuwe Dienst door [!UICONTROL Service Gallery]. Ga verder met de volgende zelfstudie om te leren hoe u kunt [programma geautomatiseerde opleiding en het scoren looppas op de Dienst](./schedule-models-ui.md).
