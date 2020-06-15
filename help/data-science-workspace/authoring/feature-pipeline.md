---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topics
solution: Adobe Experience Platform Data Science Workspace
title: Een functiepijplijn maken
topic: Tutorial
translation-type: tm+mt
source-git-commit: 20e26c874204da75cac7e8d001770702658053f1
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---


# Een functiepijplijn maken

>[!IMPORTANT]
> Functiepijpleidingen zijn momenteel alleen beschikbaar via API.

Met Adobe Experience Platform kunt u aangepaste functiepijpleidingen maken en maken om functies op schaal te laten engineering via de Sensei Machine Learning Framework Runtime (hierna &quot;Runtime&quot; genoemd).

Dit document beschrijft de diverse klassen die in een eigenschappijpleiding worden gevonden, en verstrekt een geleidelijke zelfstudie voor het creëren van een pijpleiding van de douaneeigenschap gebruikend [ModelAuthoring SDK](./sdk.md) in PySpark.

De volgende workflow vindt plaats wanneer een functiepijplijn wordt uitgevoerd:

1. Het recept laadt de dataset aan een pijpleiding.
2. De transformatie van de eigenschap wordt gedaan op de dataset en terug naar Adobe Experience Platform geschreven.
3. De getransformeerde gegevens worden geladen voor training.
4. De eigenschappijpleiding bepaalt de stadia met de Regressor van de Verloop van de Verhoging als gekozen model.
5. De pijpleiding wordt gebruikt om de opleidingsgegevens te passen en het opgeleide model wordt gecreeerd.
6. Het model wordt getransformeerd met de het scoren dataset.
7. De interessante kolommen van de output worden dan geselecteerd en terug bewaard aan [!DNL Experience Platform] de bijbehorende gegevens.

## Aan de slag

Om een recept in om het even welke organisatie in werking te stellen, wordt het volgende vereist:
- Een invoergegevensset.
- Het schema van de gegevensset.
- Een getransformeerd schema en een lege dataset die op dat schema wordt gebaseerd.
- Een outputschema en een lege dataset die op dat schema wordt gebaseerd.

Alle bovengenoemde datasets moeten aan [!DNL Platform] UI worden geupload. Gebruik het door Adobe verschafte [opstartscript](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)om dit in te stellen.

## Klassen van de eigenschappijplijn

De volgende lijst beschrijft de belangrijkste abstracte klassen die u moet uitbreiden om een eigenschappijpleiding te bouwen:

| Abstracte klasse | Beschrijving |
| -------------- | ----------- |
| DataLoader | Een klasse DataLoader biedt implementatie voor het ophalen van invoergegevens. |
| DatasetTransformer | Een klasse DatasetTransformer verstrekt implementaties om de inputdataset om te zetten. U kunt verkiezen om geen klasse te verstrekken DatasetTransformer en uw logica van de eigenschapengineering binnen de klasse FeaturePipelineFactory in plaats daarvan uit te voeren. |
| FeaturePipelineFactory | Een klasse FeaturePipelineFactory bouwt een Pijpleiding van de Vonk die uit een reeks Transformers van de Vonk bestaat om eigenschapengineering uit te voeren. U kunt verkiezen om geen klasse te verstrekken FeaturePipelineFactory en uw logica van de eigenschapengineering in plaats daarvan binnen de klasse DatasetTransformer uit te voeren. |
| DataSaver | Een klasse DataSaver verstrekt de logica voor de opslag van een eigenschapdataset. |

Wanneer een baan van de Pijpleiding van de Eigenschap in werking wordt gesteld, voert Runtime eerst DataLoader uit om inputgegevens als DataFrame te laden en wijzigt dan DataFrame door of DatasetTransformer, FeaturePipelineFactory, of allebei uit te voeren. Tot slot wordt de resulterende eigenschapdataset opgeslagen door DataSaver.

Het volgende stroomschema toont de orde van uitvoering van Runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Voer uw klassen van de Pijpleiding van de Eigenschap uit {#implement-your-feature-pipeline-classes}

De volgende secties verstrekken details en voorbeelden bij het uitvoeren van de vereiste klassen voor een Pijpleiding van de Eigenschap.

### Definieer variabelen in het JSON-configuratiebestand {#define-variables-in-the-configuration-json-file}

Het configuratie-JSON-bestand bestaat uit sleutel-waardeparen en is bedoeld om alle variabelen op te geven die later tijdens de runtime moeten worden gedefinieerd. Deze sleutel-waarde paren kunnen eigenschappen zoals de plaats van de inputdataset, identiteitskaart van de outputdataset, huurder identiteitskaart, kolomkopballen, etc. bepalen.

In het volgende voorbeeld ziet u hoe sleutel-waardeparen worden gevonden in een configuratiebestand:

**JSON-voorbeeld voor configuratie**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

U kunt tot de configuratie JSON door om het even welke klassenmethode toegang hebben die `config_properties` als parameter bepaalt. Bijvoorbeeld:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Zie het [pijpleiding.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) dossier door de Werkruimte van de Wetenschap van Gegevens voor een meer diepgaande configuratievoorbeeld wordt verstrekt die.

### De invoergegevens voorbereiden met DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader is verantwoordelijk voor het ophalen en filteren van invoergegevens. Uw implementatie van DataLoader moet de abstracte klasse uitbreiden `DataLoader` en de abstracte methode met voeten treden `load`.

Het volgende voorbeeld wint een [!DNL Platform] dataset door identiteitskaart terug en keert het als DataFrame terug, waar dataset identiteitskaart (`dataset_id`) een bepaald bezit in het configuratiedossier is.

**Voorbeeld van PySpark**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformeer een dataset met DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Een DatasetTransformer verstrekt de logica voor het omzetten van een input DataFrame en keert een nieuwe afgeleide DataFrame terug. Deze klasse kan worden uitgevoerd om of samen met een FeaturePipelineFactory te werken, als enige component van de eigenschapengineering te werken, of u kunt verkiezen om deze klasse niet uit te voeren.

In het volgende voorbeeld wordt de klasse DataSetTransformer uitgebreid:


**Voorbeeld van PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Gegevensfuncties van engineer met FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Een FeaturePipelineFactory staat u toe om uw logica van de eigenschaptechniek uit te voeren door een reeks Transformers van de Vonk door een Pijpleiding van de Vonk te bepalen en samen te ketenen. Deze klasse kan worden uitgevoerd om of samen met een DatasetTransformer te werken, als enige component van de eigenschapengineering te werken, of u kunt verkiezen om deze klasse niet uit te voeren.

In het volgende voorbeeld wordt de klasse FeaturePipelineFactory uitgebreid:

**Voorbeeld van PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Sla uw eigenschapdataset met DataSaver op {#store-your-feature-dataset-with-datasaver}

DataSaver is de oorzaak van het opslaan van uw resulterende eigenschapdatasets in een opslagplaats. Uw implementatie van DataSaver moet de abstracte klasse uitbreiden `DataSaver` en de abstracte methode met voeten treden `save`.

Het volgende voorbeeld breidt de klasse DataSaver uit die gegevens aan een [!DNL Platform] dataset door identiteitskaart opslaat, waar dataset ID (`featureDatasetId`) en huurder identiteitskaart (`tenantId`) bepaalde eigenschappen in de configuratie zijn.

**Voorbeeld van PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### Geef de geïmplementeerde klassenamen op in het toepassingsbestand {#specify-your-implemented-class-names-in-the-application-file}

Nu uw klassen van de eigenschappijpleiding worden bepaald en uitgevoerd, moet u de namen van uw klassen in het toepassingsYAML dossier specificeren.

In de volgende voorbeelden worden geïmplementeerde klassenamen opgegeven:

**Voorbeeld van PySpark**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## De pijplijnengine voor functies maken met behulp van de API {#create-feature-pipeline-engine-api}

Nu u uw eigenschappijpleiding hebt ontworpen, moet u een beeld van het Dok tot stand brengen om een vraag aan de eindpunten van de eigenschappijpleiding in het Leren van de Machine van Sensei API te maken. U hebt een beeld URL van het Docker nodig om een vraag aan de eindpunten van de eigenschappijpleiding te maken.

>[!TIP]
>Als u geen Docker URL hebt, bezoek de brondossiers van het [Pakket in een recept](../models-recipes/package-source-files-recipe.md) leerprogramma voor een geleidelijke analyse bij het creëren van een de gastheer URL van het Docker.

Naar keuze, kunt u de volgende inzameling van Postman ook gebruiken om in de voltooiing van het werkschema van de eigenschappijpleiding te helpen API:

https://www.getpostman.com/collections/c5fc0d1d5805a5ddd41a

### Een pijplijnengine maken {#create-engine-api}

Zodra u uw de beeldplaats van de Docker hebt, kunt u een motor [van de eigenschappijpleiding tot stand](../api/engines.md#feature-pipeline-docker) brengen gebruikend Sensei Machine Lerend API door POST aan uit te voeren `/engines`. Het creëren van een motor van de eigenschappijpleiding voorziet u van een unieke identiteitskaart van de Motor (`id`). Sla deze waarde op voordat u doorgaat.

### Een MLInstance maken {#create-mlinstance}

Gebruikend uw onlangs gecreeerd `engineID`, moet u een MLIstance [](../api/mlinstances.md#create-an-mlinstance) tot stand brengen door een POST verzoek aan het `/mlInstance` eindpunt te maken. Een succesvolle reactie keert een lading terug die de details van pas gecreëerde MLInstance met inbegrip van zijn uniek herkenningsteken (`id`) bevat die in de volgende API vraag wordt gebruikt.

### Een experiment maken {#create-experiment}

Vervolgens moet u een [expert](../api/experiments.md#create-an-experiment)maken. Om een Experiment tot stand te brengen moet u uw uniek herkenningsteken MLIstance (`id`) hebben en een verzoek van de POST aan het `/experiment` eindpunt indienen. Een geslaagde reactie retourneert een payload die de details bevat van de nieuwe Experiment, inclusief de unieke id (`id`) die wordt gebruikt in de volgende API-aanroep.

### Specificeer de de eigenschappijpleidingstaak van de in werking stellen Experimenteer {#specify-feature-pipeline-task}

Nadat u een experiment hebt gemaakt, moet u de modus Experimenteren wijzigen in `featurePipeline`. Om de wijze te veranderen, maak een extra POST aan [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) met uw `EXPERIMENT_ID` en in het lichaam verzenden `{ "mode":"featurePipeline"}` om een looppas van de eigenschappijpleiding van de Experiment te specificeren.

Zodra volledig, doe een GET verzoek om `/experiments/{EXPERIMENT_ID}` de experimentstatus [terug te](../api/experiments.md#retrieve-specific) winnen en op de status van de Experiment te wachten om te voltooien.

### De trainingstaak voor het uitvoeren van de Experimentele taak opgeven {#training}

Vervolgens moet u de [taak](../api/experiments.md#experiment-training-scoring)van de trainingsruntime opgeven. Maak een POST aan `experiments/{EXPERIMENT_ID}/runs` en in het lichaam plaatsen de wijze aan `train` en verzendt een serie van taken die uw trainingsparameters bevatten. Een geslaagde reactie retourneert een payload die de details van het gewenste experiment bevat.

Zodra volledig, doe een GET verzoek om `/experiments/{EXPERIMENT_ID}` de experimentstatus [terug te](../api/experiments.md#retrieve-specific) winnen en op de status van de Experiment te wachten om te voltooien.

### De taak voor het uitvoeren van scoring op experimentele wijze opgeven {#scoring}

>[!NOTE]
> Als u deze stap wilt voltooien, moet u ten minste één voltooide training hebben die aan uw expert is gekoppeld.

Nadat de training met succes is uitgevoerd, moet u de taak [van de](../api/experiments.md#experiment-training-scoring)scoringbewerking opgeven. Stel POST in op `experiments/{EXPERIMENT_ID}/runs` en in de hoofdtekst en stel het `mode` kenmerk in op score. Hierdoor start u de uitvoering van uw studieprogramma Experiment.

Zodra volledig, doe een GET verzoek om `/experiments/{EXPERIMENT_ID}` de experimentstatus [terug te](../api/experiments.md#retrieve-specific) winnen en op de status van de Experiment te wachten om te voltooien.

Zodra het scoren heeft voltooid, zou uw eigenschappijpleiding operationeel moeten zijn.

## Volgende stappen {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Door dit document te lezen, hebt u een eigenschappijplijn gebruikend ModelAuthoring SDK gecreeerd, een beeld van de Docker, en gebruikt het beeld URL van de Docker om een model van de eigenschappijplijn tot stand te brengen door Sensei te gebruiken lerend API. U kunt nu gegevenssets transformeren en gegevensfuncties op schaal extraheren met de [Sensei Machine Learning-API](../api/getting-started.md).