---
keywords: Experience Platform;plan een model;De Wetenschap van Gegevens Workspace;populaire onderwerpen;programma het scoren;programma opleiding
solution: Experience Platform
title: Een model plannen in de gebruikersinterface van de Data Science Workspace
type: Tutorial
description: Met Adobe Experience Platform Data Science Workspace kunt u geplande scoring- en trainingsprogramma's instellen op een computerleerservice. Door het trainings- en scoringsproces te automatiseren, kunt u de efficiëntie van een service op tijd behouden en verbeteren door patronen in uw gegevens bij te houden.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Een model plannen in de gebruikersinterface van Data Science Workspace

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Met Adobe Experience Platform [!DNL Data Science Workspace] kunt u geplande scoring- en trainingsprogramma&#39;s instellen op een leerservice voor computers. Het automatiseren van het trainings- en scoringsproces kan de efficiëntie van een service helpen behouden en verbeteren door patronen in uw gegevens bij te houden.

Deze zelfstudie doorloopt de stappen om trainings- en studieprogramma&#39;s op een bestaande service te configureren via de [!UICONTROL Service Gallery] . Het is opgedeeld in de volgende hoofdsecties:

- [Geplande scoring configureren](#configure-scheduled-scoring)
- [Geplande training configureren](#configure-scheduled-training)

## Aan de slag

U moet toegang hebben tot [!DNL Experience Platform] om deze zelfstudie te kunnen voltooien. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform] , neemt u contact op met uw systeembeheerder voordat u verdergaat.

Voor deze zelfstudie is een bestaande service vereist. Als u geen toegankelijke dienst hebt om met te werken, kunt u tot stand brengen door het leerprogramma voor [&#x200B; te volgen het publiceren van een model als dienst &#x200B;](./publish-model-service-ui.md).

## Geplande scoring configureren {#configure-scheduled-scoring}

Model het scoren kan worden gevormd om een geautomatiseerd proces op een geplande basis te zijn. Zodra de dienst wordt gecreeerd, kunt u de stappen volgen hieronder om een het scoren programma te vormen en toe te passen:

In Adobe Experience Platform selecteert u de tab **[!UICONTROL Services]** in de navigatiekolom links om het bestand **[!DNL Service Gallery]** te openen. Zoek de service waarop u scoring wilt plannen en selecteer **[!UICONTROL Open]** om de bijbehorende **[!UICONTROL Overview]** -pagina weer te geven.

![](../images/models-recipes/schedule/select_service.png)

De overzichtspagina toont de het scoren van de Dienst informatie. Selecteer de koppeling **[!UICONTROL Update Schedule]** om een scoreschema te configureren.

![](../images/models-recipes/schedule/update_scoring.png)

Vorm de frequentie, begindatum, einddatum, inputdataset, en outputdataset voor het het scoren programma. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Create]** om het scoreschema van de service bij te werken.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Het bijgewerkte scoreschema wordt weergegeven op de pagina **[!UICONTROL Overview]** van de service.

![](../images/models-recipes/schedule/scoring_set.png)

## Geplande training configureren {#configure-scheduled-training}

Het vormen van geplande trainingslooppas op de dienst zorgt ervoor dat het machine het leren model aan de meest recente gegevenspatronen wordt bijgewerkt. Wanneer een geplande trainingsrun is voltooid, wordt het resulterende getrainde model gebruikt om de service aan te sturen tot de volgende geplande trainingsrun.

Nadat een service is gemaakt, kunt u de onderstaande stappen volgen om een trainingsprogramma te configureren en toe te passen:

In Adobe Experience Platform selecteert u de tab **[!UICONTROL Services]** in de navigatiekolom links om het bestand **[!UICONTROL Service Gallery]** te openen. Zoek de service waarop u trainingsprogramma&#39;s wilt plannen en selecteer **[!UICONTROL Open]** om de bijbehorende **[!UICONTROL Overview]** -pagina weer te geven.

![](../images/models-recipes/schedule/select_service.png)

De overzichtspagina toont de de opleidingsinformatie van de dienst. Selecteer de koppeling **[!UICONTROL Update Schedule]** om een trainingsprogramma te configureren.

![](../images/models-recipes/schedule/update_training.png)

Vorm de frequentie, begindatum, einddatum, en inputdataset die voor het opleidingsprogramma wordt gebruikt. Als u tevreden bent met de configuraties, selecteert u **[!UICONTROL Create]** om het trainingsschema van de service bij te werken.

![](../images/models-recipes/schedule/set_training_schedule.png)

Het bijgewerkte trainingsschema wordt weergegeven op de pagina **[!UICONTROL Overview]** van de service.

![](../images/models-recipes/schedule/training_set.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u met succes automatische training en scoring gepland voor een service en hebt u de workflow voor de gebruikersinterface van de zelfstudie van [!DNL Data Science Workspace] voltooid. Als u dit niet reeds hebt gedaan, overweeg [&#x200B; herstartend het leerprogramma &#x200B;](./create-retails-sales-dataset.md) en volg het API werkschema om tot stand te brengen, te trainen, te scoren, en een model te publiceren.
