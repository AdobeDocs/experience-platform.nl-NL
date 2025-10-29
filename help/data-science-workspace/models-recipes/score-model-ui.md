---
keywords: Experience Platform;score een model;Data Science Workspace;populaire onderwerpen;ui;scoring run;scores resultaten
solution: Experience Platform
title: Een model score in de gebruikersinterface van Data Science Workspace
type: Tutorial
description: Scores in Adobe Experience Platform Data Science Workspace kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Score een model in de UI van de Wetenschap van Gegevens

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Scores in Adobe Experience Platform [!DNL Data Science Workspace] kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

In deze zelfstudie worden de stappen beschreven die zijn vereist om een model te scoren in de gebruikersinterface van [!DNL Data Science Workspace] .

## Aan de slag

U moet toegang hebben tot [!DNL Experience Platform] om deze zelfstudie te kunnen voltooien. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform] , neemt u contact op met uw systeembeheerder voordat u verdergaat.

Voor deze zelfstudie is een getraind model vereist. Als u geen getraind Model hebt, volg de [&#x200B; trein en evalueer een Model in het UI &#x200B;](./train-evaluate-model-ui.md) leerprogramma alvorens verder te gaan.

## Nieuwe scores maken

Er wordt een scoring-run gemaakt met geoptimaliseerde configuraties van een eerder voltooide en geëvalueerde training. De reeks optimale configuraties voor een Model wordt typisch bepaald door de metriek van de evaluatie van de opleidingslooppas te herzien.

Vind de meest optimale trainingslooppas om zijn configuraties voor het scoren te gebruiken. Open vervolgens de gewenste trainingsrun door de hyperlink te selecteren die aan de naam is gekoppeld.

![&#x200B; Uitgezochte trainingslooppas &#x200B;](../images/models-recipes/score/select-run.png)

Selecteer op het tabblad Trainingsuitvoering **[!UICONTROL Evaluation]** de optie **[!UICONTROL Score]** die zich rechtsboven in het scherm bevindt. Er wordt een nieuwe workflow voor scoren gestart.

![](../images/models-recipes/score/training_run_overview.png)

Selecteer de gegevensset voor de invoerscoring en selecteer **[!UICONTROL Next]** .

![](../images/models-recipes/score/scoring_input.png)

Selecteer de output die dataset noteert, is dit de specifieke outputdataset waar de het scoren resultaten worden opgeslagen. Bevestig de selectie en selecteer **[!UICONTROL Next]** .

![](../images/models-recipes/score/scoring_results.png)

In de laatste stap in de workflow wordt u gevraagd uw scoring uit te voeren. Deze configuraties worden gebruikt door het model voor het scoren looppas.
U kunt overgeërfde parameters die tijdens het maken van modellen zijn ingesteld, niet verwijderen. U kunt niet-overgeërfde parameters bewerken of herstellen door te dubbelklikken op de waarde of het pictogram Omkeren te selecteren terwijl u de muisaanwijzer op de invoer plaatst.

![&#x200B; configuratie &#x200B;](../images/models-recipes/score/configuration.png)

Controleer en bevestig de scoreconfiguraties en selecteer **[!UICONTROL Finish]** om de scoringbewerking te maken en uit te voeren. U wordt naar het tabblad **[!UICONTROL Scoring Runs]** geleid en de nieuwe scoring wordt met de status **[!UICONTROL Pending]** weergegeven.

![&#x200B; het scoren looppas tabel &#x200B;](../images/models-recipes/score/scoring_runs_tab.png)

Een scoring kan worden weergegeven met een van de volgende statussen:

- In behandeling
- Voltooid
- Mislukt
- Wordt uitgevoerd

Statussen worden automatisch bijgewerkt. Ga naar de volgende stap als de status **[!UICONTROL Complete]** of **[!UICONTROL Failed]** is.

## De resultaten van scores weergeven

Als u de resultaten van scores wilt weergeven, selecteert u eerst een trainingsprogramma.

![&#x200B; Uitgezochte trainingslooppas &#x200B;](../images/models-recipes/score/select-run.png)

U wordt omgeleid naar de trainingspagina **[!UICONTROL Evaluation]** . Selecteer boven aan de evaluatiepagina van de trainingsrun het tabblad **[!UICONTROL Scoring Runs]** om een lijst met bestaande scoringuitvoering weer te geven.

![&#x200B; evaluatiepagina &#x200B;](../images/models-recipes/score/view_scoring_runs.png)

Selecteer vervolgens een scoring om de uitvoergegevens weer te geven.

![&#x200B; looppas details &#x200B;](../images/models-recipes/score/view_details.png)

Als de geselecteerde scoring-runtime de status &quot;Voltooid&quot; of &quot;Mislukt&quot; heeft, wordt de koppeling **[!UICONTROL View Activity Logs]** beschikbaar gesteld. Als een scoring mislukt, kunnen uitvoeringslogboeken nuttige informatie bevatten om de oorzaak van de fout te bepalen. Selecteer **[!UICONTROL View Activity Logs]** om de uitvoeringslogboeken te downloaden.

![&#x200B; Uitgezochte meningslogboeken &#x200B;](../images/models-recipes/score/view_logs.png)

De pop-up **[!UICONTROL View activity logs]** wordt weergegeven. Selecteer een URL om de bijbehorende logboeken automatisch te downloaden.

![](../images/models-recipes/score/activity_logs.png)

U kunt ook de resultaten van uw scoring weergeven door **[!UICONTROL Preview scoring results dataset]** te selecteren.

![&#x200B; Uitgezochte voorproefresultaten &#x200B;](../images/models-recipes/score/view_results.png)

Er wordt een voorvertoning van de uitvoergegevensset weergegeven.

![&#x200B; voorproefresultaten &#x200B;](../images/models-recipes/score/preview_results.png)

Selecteer voor de volledige set met scoringresultaten de koppeling **[!UICONTROL Scoring Results Dataset]** in de rechterkolom.

## Volgende stappen

In deze zelfstudie werden de stappen doorlopen om gegevens te scoren met behulp van een getraind model in [!DNL Data Science Workspace] . Volg het leerprogramma op [&#x200B; het publiceren van een Model als Dienst in UI &#x200B;](./publish-model-service-ui.md) om gebruikers binnen uw organisatie toe te staan om gegevens te scoren door gemakkelijke toegang tot een machine het leren Dienst te verlenen.
