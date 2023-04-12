---
keywords: Experience Platform;plan een model;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;programma het scoren;programma opleiding
solution: Experience Platform
title: Een model plannen in de gebruikersinterface van de Data Science Workspace
type: Tutorial
description: Met de Adobe Experience Platform Data Science Workspace kunt u geplande scoring- en trainingsprogramma's instellen voor een computerleerservice. Door het trainings- en scoringsproces te automatiseren, kunt u de efficiëntie van een service op tijd behouden en verbeteren door patronen in uw gegevens bij te houden.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Plan een model in de werkruimte van de Wetenschap van Gegevens UI

Adobe Experience Platform [!DNL Data Science Workspace] Hiermee kunt u geplande scoring- en trainingsprogramma&#39;s instellen op een service voor machinaal leren. Het automatiseren van het trainings- en scoringsproces kan de efficiëntie van een service helpen behouden en verbeteren door patronen in uw gegevens bij te houden.

Dit leerprogramma loopt door de stappen om opleiding en het schrapen programma&#39;s op de bestaande dienst door te vormen [!UICONTROL Service Gallery]. Het is opgedeeld in de volgende hoofdsecties:

- [Geplande scoring configureren](#configure-scheduled-scoring)
- [Geplande training configureren](#configure-scheduled-training)

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.

Voor deze zelfstudie is een bestaande service vereist. Als u geen toegankelijke service hebt waarmee u kunt werken, kunt u een service maken door de zelfstudie te volgen voor [het publiceren van een model als dienst](./publish-model-service-ui.md).

## Geplande scoring configureren {#configure-scheduled-scoring}

Model het scoren kan worden gevormd om een geautomatiseerd proces op een geplande basis te zijn. Zodra de dienst wordt gecreeerd, kunt u de stappen volgen hieronder om een het scoren programma te vormen en toe te passen:

Selecteer in Adobe Experience Platform de optie **[!UICONTROL Services]** tabblad in de linkernavigatiekolom voor toegang tot de **[!DNL Service Gallery]**. Zoek de service waarop u scoring wilt plannen en selecteer **[!UICONTROL Open]** om zijn **[!UICONTROL Overview]** pagina.

![](../images/models-recipes/schedule/select_service.png)

De overzichtspagina toont de het scoren van de Dienst informatie. Selecteer **[!UICONTROL Update Schedule]** verbinding om een het scoren programma te vormen.

![](../images/models-recipes/schedule/update_scoring.png)

Vorm de frequentie, begindatum, einddatum, inputdataset, en outputdataset voor het het scoren programma. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Create]** om het het scoren van de dienst programma bij te werken.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Uw bijgewerkte het scoren programma wordt getoond in de dienst **[!UICONTROL Overview]** pagina.

![](../images/models-recipes/schedule/scoring_set.png)

## Geplande training configureren {#configure-scheduled-training}

Het vormen van geplande trainingslooppas op de dienst zorgt ervoor dat het machine het leren model aan de meest recente gegevenspatronen wordt bijgewerkt. Wanneer een geplande trainingsrun is voltooid, wordt het resulterende getrainde model gebruikt om de service aan te sturen tot de volgende geplande trainingsrun.

Nadat een service is gemaakt, kunt u de onderstaande stappen volgen om een trainingsprogramma te configureren en toe te passen:

Selecteer in Adobe Experience Platform de optie **[!UICONTROL Services]** tabblad in de linkernavigatiekolom voor toegang tot de **[!UICONTROL Service Gallery]**. Zoek de service waarop u trainingsprogramma&#39;s wilt plannen en selecteer **[!UICONTROL Open]** om zijn **[!UICONTROL Overview]** pagina.

![](../images/models-recipes/schedule/select_service.png)

De overzichtspagina toont de de opleidingsinformatie van de dienst. Selecteer **[!UICONTROL Update Schedule]** koppeling om een trainingsprogramma te configureren.

![](../images/models-recipes/schedule/update_training.png)

Vorm de frequentie, begindatum, einddatum, en inputdataset die voor het opleidingsprogramma wordt gebruikt. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Create]** om het trainingsschema van de service bij te werken.

![](../images/models-recipes/schedule/set_training_schedule.png)

Uw bijgewerkte trainingsschema wordt weergegeven in de **[!UICONTROL Overview]** pagina.

![](../images/models-recipes/schedule/training_set.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes geautomatiseerde trainings- en scoring-runtime op een service gepland en de [!DNL Data Science Workspace] UI-workflow voor zelfstudie. Als u dit nog niet hebt gedaan, kunt u [zelfstudie opnieuw starten](./create-retails-sales-dataset.md) en volgt de API-workflow om een model te maken, te trainen, te scoren en te publiceren.
