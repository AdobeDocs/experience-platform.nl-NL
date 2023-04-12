---
keywords: Experience Platform;score een model;De Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;ui;scoring looppas;scores resultaten
solution: Experience Platform
title: Score een Model in de Werkruimte van de Wetenschap van Gegevens UI
type: Tutorial
description: Scores in de Adobe Experience Platform Data Science Workspace kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Score een model in de Werkruimte van de Wetenschap van Gegevens UI

Scores in Adobe Experience Platform [!DNL Data Science Workspace] kan worden bereikt door invoergegevens in een bestaand opgeleid model in te voeren. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

Deze zelfstudie demonstreert de stappen die nodig zijn om een model te scoren in het dialoogvenster [!DNL Data Science Workspace] gebruikersinterface.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.

Voor deze zelfstudie is een getraind model vereist. Als u geen getraind model hebt, volg [Een model trainen en evalueren in de gebruikersinterface](./train-evaluate-model-ui.md) zelfstudie voordat u verdergaat.

## Nieuwe scores maken

Er wordt een scoring-run gemaakt met geoptimaliseerde configuraties van een eerder voltooide en geëvalueerde training. De reeks optimale configuraties voor een Model wordt typisch bepaald door de metriek van de evaluatie van de opleidingslooppas te herzien.

Vind de meest optimale trainingslooppas om zijn configuraties voor het scoren te gebruiken. Open vervolgens de gewenste trainingsrun door de hyperlink te selecteren die aan de naam is gekoppeld.

![Trainingsrun selecteren](../images/models-recipes/score/select-run.png)

Vanaf de trainingsrun **[!UICONTROL Evaluation]** tab, selecteert u **[!UICONTROL Score]** zich rechtsboven in het scherm bevindt. Er wordt een nieuwe workflow voor scoren gestart.

![](../images/models-recipes/score/training_run_overview.png)

Selecteer de gegevensset voor de invoerscoring en selecteer **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Selecteer de output die dataset noteert, is dit de specifieke outputdataset waar de het scoren resultaten worden opgeslagen. Bevestig uw selectie en selecteer **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

In de laatste stap in de workflow wordt u gevraagd uw scoring uit te voeren. Deze configuraties worden gebruikt door het model voor het scoren looppas.
U kunt overgeërfde parameters die tijdens het maken van modellen zijn ingesteld, niet verwijderen. U kunt niet-overgeërfde parameters bewerken of herstellen door te dubbelklikken op de waarde of het pictogram Omkeren te selecteren terwijl u de muisaanwijzer op de invoer plaatst.

![configuratie](../images/models-recipes/score/configuration.png)

Bekijk en bevestig de scores en selecteer **[!UICONTROL Finish]**  om de scoring-run te maken en uit te voeren. U wordt naar de **[!UICONTROL Scoring Runs]** en de nieuwe scoring uitvoeren met de **[!UICONTROL Pending]** status wordt weergegeven.

![tabblad scores](../images/models-recipes/score/scoring_runs_tab.png)

Een scoring kan worden weergegeven met een van de volgende statussen:
- In behandeling
- Voltooid
- Mislukt
- Wordt uitgevoerd

Statussen worden automatisch bijgewerkt. Ga naar de volgende stap als de status **[!UICONTROL Complete]** of **[!UICONTROL Failed]**.

## De resultaten van scores weergeven

Als u de resultaten van scores wilt weergeven, selecteert u eerst een trainingsprogramma.

![Trainingsrun selecteren](../images/models-recipes/score/select-run.png)

U wordt omgeleid naar de trainingsrun **[!UICONTROL Evaluation]** pagina. Selecteer boven aan de evaluatiepagina van de trainingsrun de optie **[!UICONTROL Scoring Runs]** om een lijst met bestaande scores weer te geven.

![evaluatiepagina](../images/models-recipes/score/view_scoring_runs.png)

Selecteer vervolgens een scoring om de uitvoergegevens weer te geven.

![details uitvoeren](../images/models-recipes/score/view_details.png)

Als de geselecteerde scoring-runtime de status &quot;Voltooid&quot; of &quot;Mislukt&quot; heeft, wordt de **[!UICONTROL View Activity Logs]** de koppeling is beschikbaar gesteld. Als een scoring mislukt, kunnen uitvoeringslogboeken nuttige informatie bevatten om de oorzaak van de fout te bepalen. Selecteer **[!UICONTROL View Activity Logs]**.

![Weergavelogboeken selecteren](../images/models-recipes/score/view_logs.png)

De **[!UICONTROL View activity logs]** wordt weergegeven. Selecteer een URL om de bijbehorende logboeken automatisch te downloaden.

![](../images/models-recipes/score/activity_logs.png)

U hebt ook de optie om de resultaten van uw scores weer te geven door  **[!UICONTROL Preview scoring results dataset]**.

![Voorvertoningsresultaten selecteren](../images/models-recipes/score/view_results.png)

Er wordt een voorvertoning van de uitvoergegevensset weergegeven.

![voorbeeldresultaten](../images/models-recipes/score/preview_results.png)

Selecteer voor de volledige set met scoringresultaten de optie **[!UICONTROL Scoring Results Dataset]** koppeling gevonden in de rechterkolom.

## Volgende stappen

In deze zelfstudie werden de stappen doorlopen om gegevens te scoren met behulp van een getraind model in [!DNL Data Science Workspace]. Volg de zelfstudie op [het publiceren van een Model als Dienst in UI](./publish-model-service-ui.md) om gebruikers binnen uw organisatie in staat te stellen gegevens te scoren door eenvoudige toegang te bieden tot een service voor machinaal leren.
