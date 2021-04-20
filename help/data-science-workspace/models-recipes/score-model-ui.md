---
keywords: Experience Platform;score een model;De Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;ui;scoring looppas;scores resultaten
solution: Experience Platform
title: Score een Model in de Werkruimte van de Wetenschap van Gegevens UI
topic: tutorial
type: Tutorial
description: 'Scores in de Adobe Experience Platform Data Science Workspace kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij. '
translation-type: tm+mt
source-git-commit: 7feda18351061600b05dc7be8afbbfb9a0fa7ec1
workflow-type: tm+mt
source-wordcount: '621'
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

Vind de meest optimale trainingslooppas om zijn configuraties voor het scoren te gebruiken. Open vervolgens de gewenste trainingsrun door de hyperlink te selecteren die aan de naam is gekoppeld.

![Trainingsrun selecteren](../images/models-recipes/score/select-run.png)

Selecteer **[!UICONTROL Score]** in de tabel **[!UICONTROL Evaluation]** van de trainingsrun rechtsboven in het scherm. Er wordt een nieuwe workflow voor scoren gestart.

![](../images/models-recipes/score/training_run_overview.png)

Selecteer de gegevensset voor het invoeren van de score en selecteer **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Selecteer de output die dataset noteert, is dit de specifieke outputdataset waar de het scoren resultaten worden opgeslagen. Bevestig uw selectie en selecteer **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

In de laatste stap in de workflow wordt u gevraagd uw scoring uit te voeren. Deze configuraties worden gebruikt door het model voor het scoren looppas.
U kunt overgeërfde parameters die tijdens het maken van modellen zijn ingesteld, niet verwijderen. U kunt niet-overgeërfde parameters bewerken of herstellen door te dubbelklikken op de waarde of het pictogram Omkeren te selecteren terwijl u de muisaanwijzer op de invoer plaatst.

![configuratie](../images/models-recipes/score/configuration.png)

Controleer en bevestig de scoreconfiguraties en selecteer **[!UICONTROL Finish]** om de scoring-run te maken en uit te voeren. U wordt naar het tabblad **[!UICONTROL Scoring Runs]** geleid en de nieuwe scoringstijd met de status **[!UICONTROL Pending]** wordt weergegeven.

![tabblad scores](../images/models-recipes/score/scoring_runs_tab.png)

Een scoring kan worden weergegeven met een van de volgende statussen:
- In behandeling
- Voltooid
- Mislukt
- Wordt uitgevoerd

Statussen worden automatisch bijgewerkt. Ga naar de volgende stap als de status **[!UICONTROL Complete]** of **[!UICONTROL Failed]** is.

## De resultaten van scores weergeven

Als u de resultaten van scores wilt weergeven, selecteert u eerst een trainingsprogramma.

![Trainingsrun selecteren](../images/models-recipes/score/select-run.png)

U wordt omgeleid aan de trainingslooppas **[!UICONTROL Evaluation]** pagina. Selecteer boven aan de evaluatiepagina van de trainingsrun het tabblad **[!UICONTROL Scoring Runs]** om een lijst met bestaande scoring-run weer te geven.

![evaluatiepagina](../images/models-recipes/score/view_scoring_runs.png)

Selecteer vervolgens een scoring om de uitvoergegevens weer te geven.

![details uitvoeren](../images/models-recipes/score/view_details.png)

Als de geselecteerde scoring-run de status &quot;Voltooid&quot; of &quot;Mislukt&quot; heeft, wordt de koppeling **[!UICONTROL View Activity Logs]** beschikbaar gesteld. Als een scoring mislukt, kunnen uitvoeringslogboeken nuttige informatie bevatten om de oorzaak van de fout te bepalen. Selecteer **[!UICONTROL View Activity Logs]** om de uitvoeringslogboeken te downloaden.

![Weergavelogboeken selecteren](../images/models-recipes/score/view_logs.png)

De pop-up **[!UICONTROL View activity logs]** wordt weergegeven. Selecteer een URL om de bijbehorende logboeken automatisch te downloaden.

![](../images/models-recipes/score/activity_logs.png)

U kunt ook de resultaten van uw scoring weergeven door **[!UICONTROL Preview scoring results dataset]** te selecteren.

![Voorvertoningsresultaten selecteren](../images/models-recipes/score/view_results.png)

Er wordt een voorvertoning van de uitvoergegevensset weergegeven.

![voorbeeldresultaten](../images/models-recipes/score/preview_results.png)

Voor de volledige reeks het scoren resultaten, selecteer **[!UICONTROL Scoring Results Dataset]** verbinding die in de juiste kolom wordt gevonden.

## Volgende stappen

In deze zelfstudie werden de stappen doorlopen om gegevens te scoren met behulp van een getraind model in [!DNL Data Science Workspace]. Volg de zelfstudie over [het publiceren van een Model als Dienst in UI](./publish-model-service-ui.md) om gebruikers binnen uw organisatie toe te staan om gegevens te scoren door gemakkelijke toegang tot een machine het leren Dienst te verlenen.
