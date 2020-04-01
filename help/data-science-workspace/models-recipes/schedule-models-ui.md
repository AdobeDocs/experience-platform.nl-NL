---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Een model plannen (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 541acd9e1df8a53ae372f71230a705fb6a95d92b

---


# Een model plannen (UI)

Met de Adobe Experience Platform Data Science Workspace kunt u geplande scoring- en trainingsprogramma&#39;s instellen op een computerleerservice. Door het trainings- en scoringsproces te automatiseren, kunt u de efficiëntie van een service op tijd behouden en verbeteren door patronen in uw gegevens bij te houden.

Dit leerprogramma doorloopt de stappen om opleiding en het schrapen programma&#39;s op een bestaande Dienst door de Galerij *van de* Dienst te vormen. Het is opgedeeld in de volgende hoofdsecties:

- [Geplande scoring configureren](#configure-scheduled-scoring)
- [Geplande training configureren](#configure-scheduled-training)

## Aan de slag

Als u deze zelfstudie wilt voltooien, hebt u toegang nodig tot Experience Platform. Als u geen toegang hebt tot een IMS-organisatie in het ervaringsplatform, neemt u contact op met uw systeembeheerder voordat u verdergaat.

Voor deze zelfstudie is een bestaande service vereist. Als u geen toegankelijke Dienst hebt om met te werken, kunt u tot stand brengen door uw Model als Dienst in het leerprogramma [te volgen UI](./publish-model-service-ui.md) publiceren.

## Geplande scoring configureren

Model het scoren kan worden gevormd om een geautomatiseerd proces op een geplande basis te zijn. Zodra een Dienst wordt gecreeerd, kunt u de hieronder stappen volgen om een het scoren programma te vormen en toe te passen:

1. Klik in Adobe Experience Platform op het tabblad **Services** in de linkernavigatiekolom voor toegang tot de *servicegalerie*. Zoek de dienst u wenst om het scoren looppas te plannen en **Open** te klikken om zijn pagina van het *Overzicht* te bekijken.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. De overzichtspagina toont de het scoren van de Dienst informatie. Klik de verbinding van het Programma **van de** Update om een het scoren programma te vormen.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Vorm de frequentie, begindatum, einddatum, inputdataset, en outputdataset voor het het scoren programma. Als u tevreden bent met de configuraties, klikt u op **Maken** om het scoreprogramma van de service bij te werken.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Uw bijgewerkt het scoren programma wordt getoond in de *Overzicht* van de Dienst pagina.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Geplande training configureren

Het vormen van geplande trainingslooppas op de Dienst zorgt ervoor dat het machine het leren Model aan de meest recente gegevenspatronen wordt bijgewerkt. Wanneer een geplande trainingsrun is voltooid, wordt het resulterende getrainde model gebruikt om de service aan te sturen tot de volgende geplande trainingsrun.

Zodra een Dienst wordt gecreeerd, kunt u de hieronder stappen volgen om een trainingsprogramma te vormen en toe te passen:

1. Klik in Adobe Experience Platform op het tabblad **Services** in de linkernavigatiekolom voor toegang tot de *servicegalerie*. Zoek de Dienst u wenst om trainingslooppas te plannen en **Open** te klikken om zijn pagina van het *Overzicht* te bekijken.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. De overzichtspagina toont de de opleidingsinformatie van de Dienst. Klik op de koppeling **Update Schedule** om een trainingsprogramma te configureren.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Vorm de frequentie, begindatum, einddatum, en inputdataset die voor het opleidingsprogramma wordt gebruikt. Als u tevreden bent met de configuraties, klikt u op **Maken** om het trainingsprogramma van de service bij te werken.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Uw bijgewerkte trainingsschema wordt weergegeven op de pagina *Overzicht* van de service.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes geautomatiseerde opleiding en het scoren looppas op de Dienst gepland, en voltooit de werkruimteleerprogramma UI van de Werkruimte van de Wetenschap van Gegevens. Als u dit nog niet hebt gedaan, kunt u de zelfstudie [opnieuw](./create-retails-sales-dataset.md) starten en de API-workflow volgen om een model te maken, te trainen, te scoren en te publiceren.
