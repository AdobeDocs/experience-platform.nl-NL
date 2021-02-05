---
keywords: Experience Platform;score een model;De Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;ui;scoring looppas;scores resultaten
solution: Experience Platform
title: Score een Model in de Werkruimte van de Wetenschap van Gegevens UI
topic: tutorial
type: Tutorial
description: 'Scores in de Adobe Experience Platform Data Science Workspace kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij. '
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Score een model in de Werkruimte van de Wetenschap van Gegevens UI

Scores in Adobe Experience Platform [!DNL Data Science Workspace] kunnen worden bereikt door inputgegevens in een bestaand getraind Model in te voeren. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

Deze zelfstudie demonstreert de stappen die nodig zijn om een model te scoren in de gebruikersinterface [!DNL Data Science Workspace].

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang tot een Organisatie IMS in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Voor deze zelfstudie is een getraind model vereist. Als u geen getraind Model hebt, volg [trein en evalueer een Model in UI](./train-evaluate-model-ui.md) leerprogramma alvorens verder te gaan.

## Nieuwe scores maken

Er wordt een scoring-run gemaakt met geoptimaliseerde configuraties van een eerder voltooide en geëvalueerde training. De reeks optimale configuraties voor een Model wordt typisch bepaald door de metriek van de evaluatie van de opleidingslooppas te herzien.

1. Vind de meest optimale trainingslooppas om zijn configuraties voor het scoren te gebruiken. Open de gewenste trainingsrun door op de naam ervan te klikken.

2. Klik op het tabblad Evaluatie **[!UICONTROL Evaluatie]** op de knop **[!UICONTROL Score]** rechtsboven in het scherm. Hiermee wordt een nieuwe **Run Scoring**-workflow gestart.
   ![](../images/models-recipes/score/training_run_overview.png)

3. Selecteer de gegevensset voor het noteren van de invoer en klik op **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Selecteer de output die dataset noteert, is dit de specifieke outputdataset waar de het scoren resultaten worden opgeslagen. Bevestig uw selectie en klik **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. In de laatste stap in de workflow wordt u gevraagd uw scoring uit te voeren. Deze configuraties worden gebruikt door het Model voor de scoring looppas.
U kunt overgeërfde parameters die tijdens het maken van het model zijn ingesteld, niet verwijderen. U kunt niet-overgeërfde parameters bewerken of herstellen door te dubbelklikken op de waarde of te klikken op het pictogram Omkeren terwijl u de muisaanwijzer op de invoer plaatst.
   ![](../images/models-recipes/score/configuration.png)
Controleer en bevestig de scoreconfiguraties en klik op  ****  Voltooien om de scoring uit te voeren en te maken. U wordt omgeleid naar het tabblad **[!UICONTROL Score Runs]** en de nieuwe scoring run geeft een status.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
In een scoring worden de volgende statussen weergegeven: In behandeling, Voltooid, Mislukt of Running en worden automatisch bijgewerkt. Ga naar de volgende stap als de status &quot;Voltooid&quot; of &quot;Mislukt&quot; is.

## De resultaten van scores weergeven

1. Vind de trainingslooppas die voor de het scoren looppas werd gebruikt, en klik op de naam om zijn **[!UICONTROL Evaluatie]** pagina te bekijken.

2. Klik boven aan de evaluatiepagina van de trainingsrun op het tabblad **[!UICONTROL Scores uitvoeren]** om een lijst met bestaande scoring-runtime weer te geven. Klik op het scoreningoverzicht om de details ervan in de rechterkolom weer te geven.
   ![](../images/models-recipes/score/view_details.png)

3. Als de geselecteerde scoring-run de status &quot;Voltooid&quot; of &quot;Mislukt&quot; heeft, is de koppeling **[!UICONTROL Activiteitenlogboeken weergeven]** in de rechterkolom actief. Klik op de koppeling om de uitvoeringslogboeken weer te geven of te downloaden. Als een scoring is mislukt, kunnen de uitvoeringslogboeken nuttige informatie bevatten over de oorzaak van de fout.
   ![](../images/models-recipes/score/activity_logs.png)

4. Klik op de koppeling **[!UICONTROL Voorvertoning van het scorebordresultaat Dataset]** in de rechterkolom. U zult een voorproef van de outputdataset van de het scoren looppas kunnen zien.
   ![](../images/models-recipes/score/preview_results.png)

5. Voor de volledige reeks het scoren resultaten, klik op **[!UICONTROL het Scoreren Dataset van Resultaten]** in de juiste kolom wordt gevonden die.

## Volgende stappen

In deze zelfstudie werden de stappen doorlopen om gegevens te scoren met behulp van een getraind model in [!DNL Data Science Workspace]. Volg de zelfstudie over [het publiceren van een Model als Dienst in UI](./publish-model-service-ui.md) om gebruikers binnen uw organisatie toe te staan om gegevens te scoren door gemakkelijke toegang tot een machine het leren Dienst te verlenen.
