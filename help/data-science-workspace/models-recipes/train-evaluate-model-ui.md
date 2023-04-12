---
keywords: Experience Platform;trainen en evalueren;De Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;creeer een model;creeer een trainingslooppas
solution: Experience Platform
title: Een model trainen en evalueren in de gebruikersinterface van de Data Science Workspace
type: Tutorial
description: In de Werkruimte van de Wetenschap van Gegevens van Adobe Experience Platform, wordt een machine het leren Model gecreeerd door bestaande Ontvanger op te nemen die voor de intentie van het Model aangewezen is. Het model wordt vervolgens getraind en geëvalueerd om de efficiëntie en werkzaamheid van de werking te optimaliseren door de bijbehorende hyperparameters te verfijnen. Ontvangers zijn herbruikbaar, wat betekent dat er meerdere modellen kunnen worden gemaakt en op specifieke doeleinden kunnen worden afgestemd met één ontvanger.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 1%

---

# Een model trainen en evalueren in de gebruikersinterface van de Data Science Workspace

In de Werkruimte van de Wetenschap van Gegevens van Adobe Experience Platform, wordt een machine het leren Model gecreeerd door bestaande Ontvanger op te nemen die voor de intentie van het Model aangewezen is. Het model wordt vervolgens getraind en geëvalueerd om de efficiëntie en werkzaamheid van de werking te optimaliseren door de bijbehorende hyperparameters te verfijnen. Ontvangers zijn herbruikbaar, wat betekent dat er meerdere modellen kunnen worden gemaakt en op specifieke doeleinden kunnen worden afgestemd met één ontvanger.

Deze zelfstudie doorloopt de stappen voor het maken, trainen en evalueren van een model.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.

Voor deze zelfstudie is een bestaande ontvanger vereist. Als u geen Ontvanger hebt, volg [Een gecomprimeerde ontvanger importeren in de gebruikersinterface](./import-packaged-recipe-ui.md) zelfstudie voordat u verdergaat.

## Een model maken

Selecteer in Experience Platform de optie **[!UICONTROL Models]** in de linkernavigatie en selecteer vervolgens het tabblad Bladeren om uw bestaande modellen weer te geven. Selecteren **[!UICONTROL Create Model]** rechtsboven op de pagina om een modelontwerpproces te starten.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Blader door de lijst met bestaande ontvangers, zoek en selecteer de ontvanger die u wilt gebruiken om het model te maken en selecteer **[!UICONTROL Next]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Selecteer een geschikte gegevensset en selecteer **[!UICONTROL Next]**. Hiermee wordt de standaardgegevensset voor de invoertraining voor het model ingesteld.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Geef een naam op voor het model en bekijk de standaardmodelconfiguraties. De standaardconfiguraties zijn toegepast tijdens het maken van Recipe, herzie en wijzig de configuratiewaarden door op de waarden te dubbelklikken.

Selecteer **[!UICONTROL Upload New Config]** en sleep een JSON-bestand met Modelconfiguraties naar het browservenster. Selecteren **[!UICONTROL Finish]** om het model te maken.

>[!NOTE]
>
>Configuraties zijn uniek en specifiek voor de beoogde recept. Dit betekent dat configuraties voor de Retail Sales Recipe niet werken voor de Product Recommendations Recipe. Zie de [referentie](#reference) voor een lijst van configuraties van Recipe van de Detailhandel.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Een trainingsrun maken

Selecteer in Experience Platform de optie **[!UICONTROL Models]** in de linkernavigatie en selecteer vervolgens het tabblad Bladeren om uw bestaande modellen weer te geven. Zoek en selecteer de hyperlink die is gekoppeld aan de naam van het model dat u wilt trainen.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle bestaande trainingsprogramma&#39;s met hun huidige trainingsstatus worden weergegeven. Voor modellen die zijn gemaakt met de opdracht [!DNL Data Science Workspace] gebruikersinterface, wordt een trainingslooppas automatisch geproduceerd en uitgevoerd gebruikend de standaardconfiguraties en de dataset van de inputopleiding.

Een nieuwe training maken door **[!UICONTROL Train]** in de buurt van de rechterbovenhoek van de overzichtspagina Model.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Selecteer de dataset van de opleidingsinput voor de trainingslooppas, dan selecteren **[!UICONTROL Next]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

De standaardconfiguraties die tijdens de creatie van het Model worden verstrekt worden getoond, veranderen en wijzigen dienovereenkomstig door de waarden tweemaal te klikken. Selecteren **[!UICONTROL Finish]** om de trainingsrun te maken en uit te voeren.

>[!NOTE]
>
>Configuraties zijn uniek en specifiek voor de beoogde recept. Dit betekent dat configuraties voor de Retail Sales Recipe niet werken voor de Product Recommendations Recipe. Zie de [referentie](#reference) voor een lijst van configuraties van Recipe van de Detailhandel.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Het model evalueren

Selecteer in Experience Platform de optie **[!UICONTROL Models]** in de linkernavigatie en selecteer vervolgens het tabblad Bladeren om uw bestaande modellen weer te geven. Zoek en selecteer de hyperlink die is gekoppeld aan de naam van het model dat u wilt evalueren.

![model selecteren](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alle bestaande trainingsprogramma&#39;s met hun huidige trainingsstatus worden weergegeven. Met veelvoudige voltooide trainingslooppas, kunnen de evaluatiemetriek over verschillende opleidingslooppas in de Modelbeoordelinggrafiek worden vergeleken. Selecteer een evaluatiemetrisch gebruikend dropdown lijst boven de grafiek.

De gemiddelde absolute foutenpercentage (MAPE) metrisch drukt nauwkeurigheid als percentage van de fout uit. Dit wordt gebruikt om het best presterende Experiment te identificeren. Hoe lager de MAPE, hoe beter.

![overzicht van de trainingen](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

De &quot;precisiemetrie&quot; beschrijft het percentage relevante instanties in vergelijking met het totaal *opgehaald* Instanties. Precisie kan worden gezien als de waarschijnlijkheid dat een willekeurig gekozen resultaat correct is.

![uitvoeren, meerdere uitvoering](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Het selecteren van een specifieke trainingslooppas verstrekt de details van die looppas door de evaluatiepagina te openen. Dit kan zelfs worden gedaan alvorens de looppas is voltooid. Op de evaluatiepagina, kunt u andere evaluatiemetriek, configuratieparameters, en visualisaties zien specifiek voor de trainingslooppas.

![voorbeeldlogboeken](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

U kunt activiteitenlogboeken ook downloaden om de details van de looppas te zien. Logs zijn vooral nuttig voor mislukte looppas om te zien wat verkeerd ging.

![activiteitenlogboeken](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hyperparameters kunnen niet worden getraind en een model moet worden geoptimaliseerd door verschillende combinaties van Hyperparameters te testen. Herhaal deze training en evaluatie-procedure voor het model totdat u een geoptimaliseerd model hebt behaald.

## Volgende stappen

In deze zelfstudie hebt u een model gemaakt, getraind en geëvalueerd in [!DNL Data Science Workspace]. Als u eenmaal een geoptimaliseerd model hebt gekozen, kunt u het opgeleide model gebruiken om inzichten te genereren door het volgende te doen: [Score een Model in UI](./score-model-ui.md) zelfstudie.

## Referenties  {#reference}

### Retail Sales Recipe-configuraties

Hyperparameters bepalen het trainingsgedrag van het model. Als u de hyperparameters wijzigt, is dit van invloed op de nauwkeurigheid en precisie van het model:

| Hyperparameter | Beschrijving | Aanbevolen bereik |
| --- | --- | --- |
| learning_rate | Het leren tarief vermindert de bijdrage van elke boom door learning_rate. Er is een compromis tussen learning_rate en n_estimators. | 0.1 |
| n_estimators | Het aantal opstartfasen dat moet worden uitgevoerd. Het verhogen van de gradiënt is vrij robuust aan overmaat zodat een groot aantal gewoonlijk in betere prestaties resulteert. | 100 |
| max_depth | Maximale diepte van de individuele regressieschattingen. De maximale diepte beperkt het aantal knooppunten in de structuur. Deze parameter afstemmen voor de beste prestaties; de beste waarde is afhankelijk van de interactie van de invoervariabelen. | 3 |

Aanvullende parameters bepalen de technische eigenschappen van het model:

| Parametersleutel | Type | Beschrijving |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Tekenreeks | Lijst met door komma&#39;s gescheiden invoerschemakenmerken. |
| `ACP_DSW_TARGET_FEATURES` | Tekenreeks | Lijst met door komma&#39;s gescheiden kenmerken van het uitvoerschema. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Hiermee wordt bepaald of invoer- en uitvoerfuncties kunnen worden gewijzigd |
| `tenantId` | Tekenreeks | Deze id zorgt ervoor dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. [Voer hier de stappen uit](../../xdm/api/getting-started.md#know-your-tenant_id) om je huurder-id te vinden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Tekenreeks | Het invoerschema dat wordt gebruikt voor het trainen van een model. |
| `evaluation.labelColumn` | Tekenreeks | Kolomlabel voor evaluatievisualisaties. |
| `evaluation.metrics` | Tekenreeks | Door komma&#39;s gescheiden lijst met evaluatiemetriek die moet worden gebruikt voor de evaluatie van een model. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Tekenreeks | Het uitvoerschema dat voor het scoren van een model wordt gebruikt. |
