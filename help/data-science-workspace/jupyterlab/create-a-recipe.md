---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Een recept maken met Jupyter-laptops
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1447196da7dbf59c1f498de40f12ed74c328c0e6

---


# Een recept maken met Jupyter-laptops

Deze zelfstudie heeft betrekking op twee hoofdsecties. Eerst, zult u een machine het leren model gebruikend een malplaatje binnen Notitieboekje JupyterLab creëren. Vervolgens gebruikt u de workflow voor het maken van een notebook naar het recept in JupyterLab om een recept te maken in de Data Science Workspace.

## Ingevoerde concepten:

- **Ontvangers:** Een recept is de term van Adobe voor een modelspecificatie en is een container van het hoogste niveau die een specifiek machine het leren, AI algoritme of een samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en daardoor helpen specifieke bedrijfsproblemen oplossen.
- **Model:** Een model is een geval van een machine het leren recept dat gebruikend historische gegevens en configuraties wordt opgeleid om voor een bedrijfs geval op te lossen.
- **Training:** Training is het proces van leerpatronen en inzichten van gelabelde gegevens.
- **Scores:** Scores is het proces om inzichten van gegevens te produceren gebruikend een opgeleid model.

## Aan de slag met de JupyterLab-laptopomgeving

U kunt een geheel nieuw recept maken in de Data Science Workspace. Navigeer naar het [Adobe Experience Platform](https://platform.adobe.com) en klik op het **[!UICONTROL Notebooks]** tabblad aan de linkerkant. Maak een nieuw notebook door de Recipe Builder-sjabloon te selecteren in de JupyterLauncher.

Met de Recipe Builder-laptop kunt u trainingen en scoring uitvoeren in de laptop. Dit geeft u de flexibiliteit om veranderingen in hun `train()` en `score()` methodes tussen het runnen van experimenten op de opleiding en het scoren gegevens aan te brengen. Als u tevreden bent met de resultaten van de training en scoring, kunt u een recept maken voor gebruik in de Data Science Workspace met behulp van de laptop voor de receptionfunctionaliteit die is ingebouwd in de Recipe Builder-laptop.

>[!NOTE]
>De Recipe Builder-laptop ondersteunt het werken met alle bestandsindelingen, maar momenteel ondersteunt de functie Ontvanger maken alleen Python.

![](../images/jupyterlab/create-recipe/recipe-builder.png)

Wanneer u klikt op de Recipe Builder-laptop van de draagtas, wordt de laptop geopend op het tabblad. Het model dat in de laptop wordt gebruikt, is de Python Retail Sales Forecasting Recipe die ook in [deze openbare opslagplaats te vinden is](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

U zult zien dat er op de werkbalk drie extra acties zijn, namelijk - **[!UICONTROL Train]**, **[!UICONTROL Score]** en **[!UICONTROL Create Recipe]**. Deze pictogrammen worden alleen weergegeven in het notebook met de functie Recipe Builder. Meer informatie over deze acties wordt besproken [in de sectie](#training-and-scoring) Training en score nadat u de Recipe hebt gemaakt in de laptop.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Bewerkingen uitvoeren om bestanden te recept

Als u de receptenbestanden wilt bewerken, navigeert u naar de cel in Jupyter die overeenkomt met het bestandspad. Als u bijvoorbeeld wijzigingen wilt aanbrengen in `evaluator.py`, zoekt u `%%writefile demo-recipe/evaluator.py`.

Breng de benodigde wijzigingen in de cel aan en voer de cel uit als u klaar bent. Met de `%%writefile filename.py` opdracht wordt de inhoud van de cel naar de cel geschreven `filename.py`. U moet de cel voor elk bestand met wijzigingen handmatig uitvoeren.

>[!NOTE] U moet de cellen indien nodig handmatig uitvoeren.

## Ga aan de slag met de Recipe Builder-laptop

Nu u de basisbeginselen van de JupyterLab-laptopomgeving kent, kunt u beginnen met het bekijken van de bestanden die een model voor machinaal leren vormen. De bestanden waarover we het hebben, worden hier weergegeven:

- [Vereisten, bestand](#requirements-file)
- [Configuratiebestanden](#configuration-files)
- [Opleidingsgegevensloader](#training-data-loader)
- [Scoregegevenslader](#scoring-data-loader)
- [Pipetbestand](#pipeline-file)
- [Evaluatorbestand](#evaluator-file)
- [Gegevensopslagbestand](#data-saver-file)

### Vereisten, bestand {#requirements-file}

Het bestand requirements wordt gebruikt om extra bibliotheken te declareren die u in het recept wilt gebruiken. U kunt het versienummer specificeren als er een gebiedsdeel is. Ga naar https://anaconda.org als u meer bibliotheken wilt zoeken. De lijst met hoofdbibliotheken die al worden gebruikt, bevat:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>Bibliotheken of specifieke versies die u toevoegt, zijn mogelijk niet compatibel met de bovenstaande bibliotheken.

### Configuratiebestanden {#configuration-files}

De configuratiedossiers, `training.conf` en `scoring.conf`, worden gebruikt om de datasets te specificeren u voor opleiding en het scoren wenst te gebruiken evenals hyperparameters toe te voegen. Er zijn verschillende configuraties voor training en scoring.

Gebruikers moeten de volgende variabelen invullen voordat ze training en scoring uitvoeren:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Om dataset en schema IDs te vinden, ga naar het Lusje van Gegevens binnen notitieboeken op de linkernavigatiebar (onder het omslagpictogram).

![](../images/jupyterlab/create-recipe/datasets.png)

Dezelfde informatie vindt u op het [Adobe Experience Platform](https://platform.adobe.com/) onder de tabbladen **[Schema](https://platform.adobe.com/schema)**en**[Datasets](https://platform.adobe.com/dataset/overview)** .

Standaard worden de volgende configuratieparameters voor u ingesteld wanneer u toegang krijgt tot gegevens:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Opleidingsgegevensloader {#training-data-loader}

Het doel van de trainingsgegevenslader is het instantiëren van gegevens die worden gebruikt voor het maken van het model voor machinaal leren. Er zijn doorgaans twee taken die de lader van de trainingsgegevens uitvoert:
- Gegevens laden van platform
- Gegevensvoorbereiding en functietechniek

De volgende twee secties gaan over het laden van gegevens en het voorbereiden van gegevens.

### Gegevens laden {#loading-data}

In deze stap wordt het dataframe van de [pandas gebruikt](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Gegevens kunnen worden geladen uit bestanden in het Adobe Experience Platform met behulp van de Platform SDK (`platform_sdk`) of uit externe bronnen die gebruikmaken van panda&#39;s `read_csv()` of `read_json()` -functies.

- [Platform SDK](#platform-sdk)
- [Externe bronnen](#external-sources)

>[!NOTE]
>In de Recipe Builder-laptop worden gegevens geladen via de `platform_sdk` gegevenslader.

### Platform SDK {#platform-sdk}

Voor een diepgaande zelfstudie over het gebruik van de `platform_sdk` gegevenslader gaat u naar de handleiding [van](../authoring/platform-sdk.md)Platform SDK. Dit leerprogramma verstrekt informatie over bouwstijlauthentificatie, basislezing van gegevens, en basisschrijven van gegevens.

### Externe bronnen {#external-sources}

In deze sectie ziet u hoe u een JSON- of CSV-bestand importeert naar een pandaobject. De officiële documentatie van de pandabibliotheek is te vinden op:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Ten eerste is hier een voorbeeld van het importeren van een CSV-bestand. Het `data` argument is het pad naar het CSV-bestand. Deze variabele is geïmporteerd uit het `configProperties` vorige gedeelte [](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

U kunt ook importeren vanuit een JSON-bestand. Het `data` argument is het pad naar het CSV-bestand. Deze variabele is geïmporteerd uit het `configProperties` vorige gedeelte [](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Uw gegevens bevinden zich nu in het dataframe-object en kunnen in de [volgende sectie](#data-preparation-and-feature-engineering)worden geanalyseerd en gemanipuleerd.

### Van SDK voor gegevenstoegang (afgekeurd)

>[!CAUTION]
> `data_access_sdk_python` niet meer wordt aanbevolen, raadpleeg de [gegevenstoegangscode converteren naar Platform SDK](../authoring/platform-sdk.md) voor een handleiding over het gebruik van de `platform_sdk` gegevenslader.

Gebruikers kunnen gegevens laden met de SDK voor gegevenstoegang. De bibliotheek kan boven aan de pagina worden geïmporteerd door de volgende regel op te nemen:

`from data_access_sdk_python.reader import DataSetReader`

Wij gebruiken dan de `load()` methode om de trainingsdataset van `trainingDataSetId` zoals die in ons configuratie (`recipe.conf`) dossier wordt geplaatst te pakken.

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>Zoals vermeld in de sectie [van het Dossier van de](#configuration-files)Configuratie, worden de volgende configuratieparameters geplaatst voor u wanneer u tot gegevens van het Platform van de Ervaring toegang hebt:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Nu u uw gegevens hebt, kunt u beginnen met gegevensvoorbereiding en functietechniek.

### Gegevensvoorbereiding en functietechniek {#data-preparation-and-feature-engineering}

Nadat de gegevens zijn geladen, worden de gegevens voorbereid en vervolgens gesplitst in de `train` gegevenssets en de `val` gegevensbestanden. De voorbeeldcode wordt hieronder weergegeven:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

In dit voorbeeld worden er vijf dingen aan de originele dataset gedaan:
- toevoegen `week` en `year` kolommen
- converteren `storeType` naar een indicatorvariabele
- omzetten `isHoliday` in een numerieke variabele
- verschuiving `weeklySales` om verkoopwaarde in de toekomst en in het verleden te bepalen
- gesplitste gegevens, op datum, naar `train` en `val` gegevensset

Eerst worden `week` en `year` kolommen gemaakt en wordt de oorspronkelijke `date` kolom omgezet in Python- [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Week- en jaarwaarden worden geëxtraheerd uit het datetime-object.

Daarna, `storeType` wordt omgezet in drie kolommen die de drie verschillende opslagtypes vertegenwoordigen, (`A`, `B`, en `C`). Elk object bevat een booleaanse waarde die true `storeType` is. De `storeType` kolom wordt verwijderd.

Op dezelfde manier wijzigt `weeklySales` u de `isHoliday` booleaanse waarde in een numerieke representatie, één of nul.

Deze gegevens worden opgesplitst tussen `train` en `val` gegevensset.

De `load()` functie zou met de `train` en `val` dataset als output moeten voltooien.

### Scoregegevenslader {#scoring-data-loader}

De procedure voor het laden van gegevens voor scoring is vergelijkbaar met de trainingsgegevens voor het laden van de `split()` functie. We gebruiken de SDK voor gegevenstoegang om gegevens te laden uit de `scoringDataSetId` gegevens in ons `recipe.conf` bestand.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

Nadat de gegevens zijn geladen, worden de gegevens voorbereid en worden de functies verbeterd.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Aangezien het doel van ons model de toekomstige wekelijkse verkoop moet voorspellen, zult u een het scoren dataset moeten creëren die wordt gebruikt om te evalueren hoe goed de voorspelling van het model presteert.

Dit doet de Recipe Builder-laptop door onze wekelijkse verkoop 7 dagen vooruit te compenseren. U ziet dat er elke week metingen worden uitgevoerd voor 45 winkels, zodat u de `weeklySales` waarden 45 gegevenssets kunt verplaatsen naar een nieuwe kolom met de naam `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Op dezelfde manier kunt u een kolom maken `weeklySalesLag` door 45 achteruit te schuiven. Op deze manier kunt u ook het verschil in wekelijkse verkopen berekenen en deze in kolom opslaan `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Aangezien u datapoints 45 datasets door:sturen en 45 datasets achterwaarts compenseert om nieuwe kolommen tot stand te brengen, zullen de eerste en laatste 45 gegevenspunten waarden NaN hebben. `weeklySales` U kunt deze punten uit onze dataset verwijderen door de `df.dropna()` functie te gebruiken die alle rijen verwijdert die waarden NaN hebben.

```PYTHON
df.dropna(0, inplace=True)
```

De `load()` functie in uw het scoren gegevenslader zou met de het scoren dataset als output moeten voltooien.

### Pipetbestand {#pipeline-file}

Het `pipeline.py` bestand bevat logica voor training en scoring.

### Training {#training}

Het doel van opleiding is een model te creëren gebruikend eigenschappen en etiketten in uw opleidingsdataset.

>[!NOTE]\
>_Functies_ verwijzen naar de invoervariabele die door het model voor machinaal leren wordt gebruikt om de _labels_ te voorspellen.

De `train()` functie moet het trainingsmodel bevatten en het getrainde model retourneren. Sommige voorbeelden van verschillende modellen zijn te vinden in de documentatie [van de](https://scikit-learn.org/stable/user_guide.html)handleiding van scikit-learn.

Na het kiezen van uw trainingsmodel, zult u uw x en y opleidingsdataset aan het model passen en de functie zal het getrainde model terugkeren. Een voorbeeld dat dit toont is als volgt:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Afhankelijk van uw toepassing hebt u argumenten in uw `GradientBoostingRegressor()` functie. `xTrainingDataset` moet de functies bevatten die voor training worden gebruikt, maar moet ook uw labels `yTrainingDataset` bevatten.

### Scores {#scoring}

De `score()` functie moet het scorealgoritme bevatten en een meting retourneren om aan te geven hoe succesvol het model is. De `score()` functie gebruikt de het scoren datasetetiketten en het opgeleide model om een reeks voorspelde eigenschappen te produceren. Deze voorspelde waarden worden vervolgens vergeleken met de eigenlijke kenmerken in de gegevensset voor scoren. In dit voorbeeld gebruikt de `score()` functie het getrainde model om functies te voorspellen met de labels uit de scoredataset. De voorspelde functies worden geretourneerd.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Evaluatorbestand {#evaluator-file}

Het `evaluator.py` bestand bevat logica voor de manier waarop u uw getrainde recept wilt evalueren en voor de manier waarop uw trainingsgegevens moeten worden gesplitst. In het voorbeeld van de detailhandel wordt de logica voor het laden en voorbereiden van de trainingsgegevens opgenomen. We zullen de twee onderstaande secties doornemen.

### De gegevensset splitsen {#split-the-dataset}

De fase van de gegevensvoorbereiding voor opleiding vereist opsplitsing van de gegevensset die voor opleiding en tests moet worden gebruikt. Deze `val` gegevens worden impliciet gebruikt om het model te evalueren nadat het is opgeleid. Dit proces staat los van scoring.

In deze sectie wordt de functie weergegeven die `split()` eerst gegevens in de laptop laadt en worden de gegevens vervolgens opgeschoond door niet-verwante kolommen uit de gegevensset te verwijderen. Vanaf dat punt kunt u functietechniek uitvoeren. Dit is het proces om aanvullende relevante functies te maken op basis van bestaande onbewerkte functies in de gegevens. Een voorbeeld van dit proces is hieronder samen met een verklaring te zien.

De `split()` functie wordt hieronder weergegeven. Het dataframe dat in het argument wordt opgegeven, wordt gesplitst naar de te retourneren variabelen `train` `val` en variabelen.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Evalueer het getrainde model {#evaluate-the-trained-model}

De `evaluate()` functie wordt uitgevoerd nadat het model wordt opgeleid en zal metrisch terugkeren om erop te wijzen hoe succesvol het model presteert. De `evaluate()` functie gebruikt de het testen etiketten van de dataset en het Getrainde model om een reeks eigenschappen te voorspellen. Deze voorspelde waarden worden vervolgens vergeleken met de feitelijke kenmerken in de testdataset. Veelvoorkomende scoringsalgoritmen zijn:
- [Gemiddelde absolute percentagefout (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Gemiddelde absolute fout (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Root-gemiddelde-vierkante fout (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


De `evaluate()` functie in de steekproef van de detailhandel wordt hieronder weergegeven:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

De functie retourneert een `metric` object met een array van evaluatiemetriek. Deze metriek zal worden gebruikt om te evalueren hoe goed het opgeleide model presteert.

### Gegevensopslagbestand {#data-saver-file}

Het `datasaver.py` bestand bevat de `save()` functie waarmee u uw voorspelling kunt opslaan tijdens het testen van scoring. De `save()` functie gebruikt uw voorspelling en maakt gebruik van Experience Platform Catalog API&#39;s en schrijft de gegevens naar de `scoringResultsDataSetId` opgegeven gegevens in uw `scoring.conf` bestand.

Het voorbeeld dat in het in de detailhandel verkrijgbare product wordt gebruikt, is hier te zien. Let op het gebruik van de `DataSetWriter` bibliotheek voor het schrijven van gegevens naar Platform:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Training en scores {#training-and-scoring}

Wanneer u klaar bent met het aanbrengen van wijzigingen in uw laptop en uw recept wilt trainen, kunt u op de bijbehorende knoppen boven aan de balk klikken om een trainingsrun in de cel te maken. Nadat u op de knop hebt geklikt, wordt een logboek met opdrachten en uitvoer uit het trainingsscript weergegeven in het notitieblok (onder de `evaluator.py` cel). Conda installeert eerst alle gebiedsdelen, dan wordt de opleiding in werking gesteld.

Let erop dat u minstens één keer training moet uitvoeren voordat u scoring kunt uitvoeren. Als u op de **[!UICONTROL Run Scoring]** knop klikt, wordt het getrainde model weergegeven dat tijdens de training is gegenereerd. Het scorescript wordt onder `datasaver.py`weergegeven.

Voor het zuiveren doeleinden, als u wenst om de verborgen output te zien, voeg aan het eind van de outputcel toe en stel het opnieuw in werking. `debug`

## recept maken {#create-recipe}

Als u klaar bent met het bewerken van het recept en tevreden bent met de trainings-/scoringuitvoer, kunt u een recept van de laptop maken door op de navigatie rechtsboven **[!UICONTROL Create Recipe]** te drukken.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Nadat u op de knop hebt gedrukt, wordt u gevraagd een naam voor het recept in te voeren. Deze naam staat voor het recept dat op Platform is gemaakt.

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Als u eenmaal op **[!UICONTROL Ok]** drukt, kunt u naar het nieuwe recept navigeren op het [Adobe Experience Platform](https://platform.adobe.com/). U kunt op de **[!UICONTROL View Recipes]** knop klikken om naar de **[!UICONTROL Recipes]** tab onder **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Zodra het proces is voltooid, zal het recept er ongeveer als volgt uitzien:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - Geen van de bestandscellen verwijderen
> - De `%%writefile` regel boven aan de bestandscellen niet bewerken
> - Geen recepten in verschillende notebooks tegelijk maken


## Volgende stappen {#next-steps}

Door deze zelfstudie te voltooien, hebt u geleerd hoe u een model voor computerleren kunt maken in de Recipe Builder-laptop. U hebt ook geleerd hoe u de workflow voor notebooks kunt gebruiken om een recept te maken in de Data Science Workspace.

Als u wilt blijven leren werken met bronnen in de Data Science Workspace, gaat u naar de recepten en vervolgkeuzelijst voor de Data Science Workspace.

## Aanvullende bronnen {#additional-resources}

De volgende video is ontworpen om uw inzicht in het bouwen en implementeren van modellen te ondersteunen.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


