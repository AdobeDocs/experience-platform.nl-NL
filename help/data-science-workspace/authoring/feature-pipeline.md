---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Een functiepijpleiding maken
topic: Tutorial
translation-type: tm+mt
source-git-commit: b9b0578a43182650b3cfbd71f46bcb817b3b0cda

---


# Een functiepijpleiding maken

Met het Adobe Experience Platform kunt u aangepaste functiepijpleidingen maken en maken die op schaal functietechnieken kunnen uitvoeren via de Sensei Machine Learning Framework Runtime (hierna &quot;Runtime&quot; genoemd).

Dit document beschrijft de diverse klassen die in een Pijpleiding van de Eigenschap worden gevonden, en verstrekt een geleidelijke zelfstudie voor het creëren van een pijpleiding van de Eigenschap van de douane die de [ModelAuthoring SDK](./sdk.md) in PySpark en Vonk gebruikt.

De zelfstudie behandelt de volgende stappen:
- [Voer uw klassen van de Pijpleiding van de Eigenschap uit](#implement-your-feature-pipeline-classes)
   - [Variabelen definiëren in een configuratiebestand](#define-variables-in-the-configuration-json-file)
   - [De invoergegevens voorbereiden met DataLoader](#prepare-the-input-data-with-dataloader)
   - [Transformeer een dataset met DatasetTransformer](#transform-a-dataset-with-datasettransformer)
   - [Gegevensfuncties van engineer met FeaturePipelineFactory](#engineer-data-features-with-featurepipelinefactory)
   - [Sla uw eigenschapdataset met DataSaver op](#store-your-feature-dataset-with-datasaver)
   - [Geef de geïmplementeerde klassenamen op in het toepassingsbestand](#specify-your-implemented-class-names-in-the-application-file)
- [Bouw het binaire artefact](#build-the-binary-artifact)
- [Een engine voor een functiepijpleiding maken met de API](#create-a-feature-pipeline-engine-using-the-api)

## Functiepijpklassen

De volgende lijst beschrijft de belangrijkste Abstracte Klassen die u moet uitbreiden om een Pijl van de Eigenschap te bouwen:

| Abstracte klasse | Beschrijving |
| -------------- | ----------- |
| DataLoader | Een klasse DataLoader biedt implementatie voor het ophalen van invoergegevens. |
| DatasetTransformer | Een klasse DatasetTransformer verstrekt implementaties om de inputdataset om te zetten. U kunt verkiezen om geen klasse te verstrekken DatasetTransformer en uw logica van de eigenschapengineering binnen de klasse FeaturePipelineFactory in plaats daarvan uit te voeren. |
| FeaturePipelineFactory | Een klasse FeaturePipelineFactory bouwt een Pijpleiding van de Vonk die uit een reeks Transformers van de Vonk bestaat om eigenschapengineering uit te voeren. U kunt verkiezen om geen klasse te verstrekken FeaturePipelineFactory en uw logica van de eigenschapengineering in plaats daarvan binnen de klasse DatasetTransformer uit te voeren. |
| DataSaver | Een klasse DataSaver verstrekt de logica voor de opslag van een eigenschapdataset. |

Wanneer een baan van de Pijpleiding van de Eigenschap in werking wordt gesteld, zal Runtime eerst DataLoader uitvoeren om inputgegevens als DataFrame te laden en dan DataFrame wijzigen door of DatasetTransformer, of FeaturePipelineFactory, of allebei uit te voeren. Tot slot wordt de resulterende eigenschapdataset opgeslagen door DataSaver.

Het volgende stroomschema toont de orde van uitvoering van Runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Voer uw klassen van de Pijpleiding van de Eigenschap uit

De volgende secties verstrekken details en voorbeelden bij het uitvoeren van de vereiste klassen voor een Pijpleiding van de Eigenschap.

### Definieer variabelen in het JSON-configuratiebestand

Het configuratie-JSON-bestand bestaat uit sleutel-waardeparen en is bedoeld om alle variabelen op te geven die later tijdens de runtime moeten worden gedefinieerd. Deze sleutel-waarde paren kunnen eigenschappen zoals de plaats van de inputdataset, identiteitskaart van de outputdataset, huurder identiteitskaart, kolomkopballen, etc. bepalen.

In het volgende voorbeeld ziet u hoe sleutel-waardeparen worden gevonden in een configuratiebestand. Vouw het voorbeeld uit om details weer te geven:


**JSON-voorbeeld voor configuratie**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



U kunt tot de configuratie JSON door om het even welke klassenmethode toegang hebben die `configProperties` als parameter bepaalt. Bijvoorbeeld:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### De invoergegevens voorbereiden met DataLoader

DataLoader is verantwoordelijk voor het ophalen en filteren van invoergegevens. Uw implementatie van DataLoader moet de abstracte klasse uitbreiden `DataLoader` en de abstracte methode met voeten treden `load`.

Het volgende voorbeeld wint een dataset van het Platform door identiteitskaart terug en keert het als DataFrame terug, waar dataset identiteitskaart (`datasetId`) een bepaald bezit in het configuratiedossier is. Vouw elk voorbeeld uit om details weer te geven:


**Voorbeeld van PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark-voorbeeld**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### Transformeer een dataset met DatasetTransformer

Een DatasetTransformer verstrekt de logica voor het omzetten van een input DataFrame en keert een nieuwe afgeleide DataFrame terug. Deze klasse kan worden uitgevoerd om of samen met een FeaturePipelineFactory te werken, als enige component van de eigenschapengineering te werken, of u kunt verkiezen om deze klasse niet uit te voeren.

In het volgende voorbeeld wordt de klasse DatasetTransformer uitgebreid. Vouw elk voorbeeld uit om details weer te geven:


**Voorbeeld van PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark-voorbeeld**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Gegevensfuncties van engineer met FeaturePipelineFactory

Een FeaturePipelineFactory staat u toe om uw logica van de eigenschaptechniek uit te voeren door een reeks Transformers van de Vonk door een Pijpleiding van de Vonk te bepalen en samen te ketenen. Deze klasse kan worden uitgevoerd om of samen met een DatasetTransformer te werken, als enige component van de eigenschapengineering te werken, of u kunt verkiezen om deze klasse niet uit te voeren.

Het volgende voorbeeld breidt de klasse FeaturePipelieFactory uit en voert een reeks transformatoren van de Vonk als veelvoudige stadia in een Pijpleiding van de Vonk uit. Vouw elk voorbeeld uit om details weer te geven:


**Voorbeeld van PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark-voorbeeld**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Sla uw eigenschapdataset met DataSaver op

DataSaver is de oorzaak van het opslaan van uw resulterende eigenschapdatasets in een opslagplaats. Uw implementatie van DataSaver moet de abstracte klasse uitbreiden `DataSaver` en de abstracte methode met voeten treden `save`.

Het volgende voorbeeld breidt de klasse DataSaver uit die gegevens aan een dataset van het Platform door identiteitskaart opslaat, waar dataset identiteitskaart (`featureDatasetId`) en huurder identiteitskaart (`tenantId`) bepaalde eigenschappen in het configuratiedossier zijn. Vouw elk voorbeeld uit om details weer te geven:


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




**Spark-voorbeeld**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Geef de geïmplementeerde klassenamen op in het toepassingsbestand

Nu uw klassen van de Pijl van de Eigenschap worden bepaald en uitgevoerd, moet u de namen van uw klassen in het toepassingsdossier specificeren.

In de volgende voorbeelden worden geïmplementeerde klassenamen opgegeven. Vouw het voorbeeld uit om details weer te geven:


**Voorbeeld van PySpark**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark-voorbeeld**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Bouw het binaire artefact

Nu uw uitgevoerde klassen van de Pijl van de Eigenschap, kunt u het in een binair artefact bouwen en compileren dat dan kan worden gebruikt om een Pijpleiding van de Eigenschap door API vraag tot stand te brengen.

**PySpark**

Als u een PySpark-functiepijpleiding wilt maken, voert u het Python-script uit dat zich in de hoofdmap van de ModelontwerpSDK bevindt. `setup.py`

>[!NOTE] Voor het bouwen van een PySpark-functiepijpleiding moet Python 3 op uw computer zijn geïnstalleerd.

```shell
python3 setup.py bdist_egg
```

De bouw van uw Pijpleiding van de Eigenschap zal met succes een `.egg` artefact in de `/dist` folder produceren, wordt dit artefact gebruikt om een Pijpleiding van de Eigenschap tot stand te brengen.

**Spark**

Om een Pijpleiding van de Eigenschap van de Vonk te bouwen, stel het volgende consolebevel in de wortelfolder van ModelAuthoring SDK in werking:

>[!NOTE] Voor het bouwen van een Spark Feature Pipeline dient u Scala en sbt op uw computer te hebben geïnstalleerd.

```shell
mvn clean install
```

De bouw van uw Pijpleiding van de Eigenschap zal met succes een `.jar` artefact in de `/dist` folder produceren, wordt dit artefact gebruikt om een Pijpleiding van de Eigenschap tot stand te brengen.

## Een engine voor een functiepijpleiding maken met de API

Nu u uw Pijpleiding van de Eigenschap hebt ontworpen en het binaire vervorming hebt gebouwd, kunt u een Motor van de Pijpleiding van de Eigenschap [tot stand brengen gebruikend de het Leren API](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)van de Machine van Sensei. Als u een engine voor de functiepijpleiding maakt, ontvangt u een engine-id als onderdeel van de responsstructuur. Sla deze waarde op voordat u verdergaat met de volgende stappen.

## Volgende stappen

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Door dit document te lezen, hebt u een Pijpleiding van de Eigenschap geschreven gebruikend ModelAuthoring SDK, bouwde een binair artefact, en gebruikte het artefact om een Motor van de Pijpleiding van de Eigenschap door een API vraag tot stand te brengen. U bent nu klaar om een Model [van de Pijpleiding van de Eigenschap te](../api/mlinstances.md#create-an-mlinstance) creëren gebruikend uw pas gecreëerde Motor en begonnen datasets te transformeren en gegevenseigenschappen bij schaal te halen.