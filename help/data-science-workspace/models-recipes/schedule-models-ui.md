---
keywords: Experience Platform;plan een model;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;programma het scoren;programma opleiding
solution: Experience Platform
title: Een model plannen in de gebruikersinterface van de Data Science Workspace
topic: tutorial
type: Tutorial
description: Met de Adobe Experience Platform Data Science Workspace kunt u geplande scoring- en trainingsprogramma's instellen voor een computerleerservice. Door het trainings- en scoringsproces te automatiseren, kunt u de efficiëntie van een service op tijd behouden en verbeteren door patronen in uw gegevens bij te houden.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Plan een model in de werkruimte van de Wetenschap van Gegevens UI

Met Adobe Experience Platform [!DNL Data Science Workspace] kunt u geplande scoring- en trainingsprogramma&#39;s instellen op een computerleerservice. Door het trainings- en scoringsproces te automatiseren, kunt u de efficiëntie van een service op tijd behouden en verbeteren door patronen in uw gegevens bij te houden.

Deze zelfstudie doorloopt de stappen voor het configureren van trainings- en scoring-planningen op een bestaande service via de [!UICONTROL Servicegalerie]. Het is opgedeeld in de volgende hoofdsecties:

- [Geplande scoring configureren](#configure-scheduled-scoring)
- [Geplande training configureren](#configure-scheduled-training)

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang tot een Organisatie IMS in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Voor deze zelfstudie is een bestaande service vereist. Als u geen toegankelijke Dienst hebt om met te werken, kunt u tot stand brengen door [uw Model als Dienst in het UI](./publish-model-service-ui.md) leerprogramma te volgen publiceren.

## Geplande scores {#configure-scheduled-scoring} configureren

Model het scoren kan worden gevormd om een geautomatiseerd proces op een geplande basis te zijn. Zodra een Dienst wordt gecreeerd, kunt u de hieronder stappen volgen om een het scoren programma te vormen en toe te passen:

1. Klik in Adobe Experience Platform op het tabblad **[!UICONTROL Services]** in de linkernavigatiekolom om toegang te krijgen tot **[!DNL Service Gallery]**. Zoek de service waarop u scoring wilt plannen en klik op **[!UICONTROL Open]** om de pagina **Overzicht** te bekijken.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. De overzichtspagina toont de het scoren van de Dienst informatie. Klik **[!UICONTROL Update Plan]** verbinding om een het scoren programma te vormen.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Vorm de frequentie, begindatum, einddatum, inputdataset, en outputdataset voor het het scoren programma. Als u tevreden bent met de configuraties, klikt u op **[!UICONTROL Maken]** om het scoreschema van de service bij te werken.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Uw bijgewerkte scoreschema wordt weergegeven op de pagina **Overzicht** van de service.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Geplande training {#configure-scheduled-training} configureren

Het vormen van geplande trainingslooppas op de Dienst zorgt ervoor dat het machine het leren Model aan de meest recente gegevenspatronen wordt bijgewerkt. Wanneer een geplande trainingsrun is voltooid, wordt het resulterende getrainde model gebruikt om de service aan te sturen tot de volgende geplande trainingsrun.

Zodra een Dienst wordt gecreeerd, kunt u de hieronder stappen volgen om een trainingsprogramma te vormen en toe te passen:

1. Klik in Adobe Experience Platform op het tabblad **[!UICONTROL Services]** in de linkernavigatiekolom voor toegang tot de **[!UICONTROL Servicegalerie]**. Zoek de service waarop u trainingsprogramma&#39;s wilt plannen en klik op **[!UICONTROL Open]** om de **Overview**-pagina weer te geven.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. De overzichtspagina toont de de opleidingsinformatie van de Dienst. Klik **[!UICONTROL Update Plan]** verbinding om een opleidingsprogramma te vormen.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Vorm de frequentie, begindatum, einddatum, en inputdataset die voor het opleidingsprogramma wordt gebruikt. Als u tevreden bent met de configuraties, klikt u op **[!UICONTROL Maken]** om het trainingsschema van de service bij te werken.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Uw bijgewerkte trainingsschema wordt weergegeven op de pagina **Overzicht** van de service.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes geautomatiseerde trainings- en scoring-runtime op een Service gepland en de gebruikersinterface van de [!DNL Data Science Workspace]-zelfstudie voltooid. Als u dit nog niet hebt gedaan, kunt u [de zelfstudie opnieuw starten](./create-retails-sales-dataset.md) en de API-workflow volgen om een model te maken, te trainen, te scoren en te publiceren.
