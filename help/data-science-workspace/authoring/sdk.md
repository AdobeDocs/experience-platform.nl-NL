---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Handleiding voor SDK-ontwikkelaars
topic: Overview
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Handleiding voor SDK-ontwikkelaars

De ModelAuthoring SDK stelt u in staat om aangepaste machines te ontwikkelen die Ontvangers en kenmerkpijplijnen leren die kunnen worden gebruikt in de Werkruimte van de Wetenschap van Gegevens, die implementeerbare sjablonen in PySpark en Spark verstrekken. [!DNL Adobe Experience Platform]

Dit document bevat informatie over de verschillende klassen in de ModelontwerpSDK.

## DataLoader {#dataloader}

Met de klasse DataLoader wordt alles ingekapseld wat te maken heeft met het ophalen, filteren en retourneren van onbewerkte invoergegevens. Voorbeelden van invoergegevens zijn bijvoorbeeld gegevens voor training, scoring of functietechniek. De laders van gegevens breiden de abstracte klasse uit `DataLoader` en moeten de abstracte methode met voeten treden `load`.

**PySpark**

In de volgende tabel worden de abstracte methoden van de klasse PySpark Data Loader beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Platformgegevens laden en retourneren als een Pandas DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">spark</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

De volgende lijst beschrijft de abstracte methodes van een klasse van de Loader van Gegevens van de Vonk:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Platformgegevens laden en retourneren als een DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Gegevens laden uit een gegevensset van een platform {#load-data-from-a-platform-dataset}

Het volgende voorbeeld wint de gegevens van het Platform door identiteitskaart terug en keert een DataFrame terug, waar dataset identiteitskaart (`datasetId`) een bepaalde bezit in het configuratiedossier is.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver {#datasaver}

De klasse DataSaver kapselt om het even wat verwant met het opslaan van outputgegevens met inbegrip van die van het scoring of eigenschapengineering. Gegevensbesparing breidt de abstracte klasse uit `DataSaver` en moet de abstracte methode met voeten treden `save`.

**PySpark**

In de volgende tabel worden de abstracte methoden van een PySpark-klasse Data Saver beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Ontvang outputgegevens als DataFrame en sla het in een dataset van het Platform op</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">dataframe</code>: Gegevens die moeten worden opgeslagen in de vorm van een DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In de volgende tabel worden de abstracte methoden van de klasse Spark Data Saver beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Ontvang outputgegevens als DataFrame en sla het in een dataset van het Platform op</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">dataFrame</code>: Gegevens die moeten worden opgeslagen in de vorm van een DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Gegevens opslaan naar een gegevensset voor een platform {#save-data-to-a-platform-dataset}

Om gegevens op een dataset van het Platform op te slaan, moeten de eigenschappen of in het configuratiedossier worden verstrekt of worden bepaald:

- Een geldige identiteitskaart van de dataset van het Platform waaraan de gegevens zullen worden opgeslagen
- De huurder-id van uw organisatie

In de volgende voorbeelden worden gegevens (`prediction`) opgeslagen op een gegevensset Platform, waarbij de gegevensset-id (`datasetId`) en huurder-id (`tenantId`) gedefinieerde eigenschappen zijn in het configuratiebestand.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer {#datasettransformer}

De klasse DatasetTransformer wijzigt en transformeert de structuur van een dataset. Voor de Sensei Machine Learning-runtime hoeft deze component niet te worden gedefinieerd en deze wordt op basis van uw vereisten geïmplementeerd.

Met betrekking tot een eigenschappijpleiding, kunnen de datasettransformatoren samen met een eigenschappijpleidingsfabriek worden gebruikt om gegevens voor eigenschapengineering voor te bereiden.

**PySpark**

De volgende lijst beschrijft de klassenmethodes van een PySpark dataset transformatorklasse:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Neemt een dataset als input en output een nieuwe afgeleide dataset</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">dataset</code>: De gegevensset voor invoer voor transformatie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

De volgende lijst beschrijft de abstracte methodes van een de transformatorklasse van de dataset van de Vonk:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Neemt een dataset als input en output een nieuwe afgeleide dataset</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                    <li><code class=" language-undefined">dataset</code>: De gegevensset voor invoer voor transformatie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

De klasse FeaturePipelineFactory bevat eigenschappen extractiealgoritmen en bepaalt de stadia van een Pijpleiding van de Eigenschap van begin tot eind.

**PySpark**

In de volgende tabel worden de klassemethoden van een PySpark FeaturePipelineFactory beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Creeer en terugkeer een Pijpleiding van de Vonk die een reeks Transformers van de Vonk bevat</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Haal paramomkaart van configuratie-eigenschappen op en retourneer deze</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In de volgende tabel worden de klassemethoden van een Spark FeaturePipelineFactory beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Creeer en terugkeer een Pijpleiding die een reeks Transformers bevat</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Toewijzingseigenschappen</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Haal paramomkaart van configuratie-eigenschappen op en retourneer deze</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

De klasse PipelineFactory omvat methodes en definities voor modelopleiding en het scoren, waar de opleidingslogica en algoritmen in de vorm van een Pijpleiding van de Vonk worden bepaald.

**PySpark**

In de volgende tabel worden de klassemethoden van een PySpark PipelineFactory beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Creeer en terugkeer een Pijpleiding van de Vonk die de logica en het algoritme voor modelopleiding en het scoring bevat</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Retourneer een aangepaste pijpleiding die de logica en het algoritme voor het trainen van een model bevat. Deze methode is niet vereist als een Spark Pipeline wordt gebruikt</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">dataframe</code>: Gegevensset met functies voor trainingsinvoer</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Score met behulp van het getrainde model en retourneert de resultaten</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">dataframe</code>: Invoergegevensset voor scoring</li>
                    <li><code class=" language-undefined">model</code>: Een getraind model dat wordt gebruikt voor scores</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Haal paramomkaart van configuratie-eigenschappen op en retourneer deze</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In de volgende tabel worden de klassemethoden van een Spark PipelineFactory beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Creeer en terugkeer een Pijpleiding die de logica en het algoritme voor modelopleiding en het scoring bevat</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Haal paramomkaart van configuratie-eigenschappen op en retourneer deze</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-sessie</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

De klasse MLEvaluator biedt methoden voor het definiëren van evaluatiemetriek en het bepalen van trainings- en testgegevenssets.

**PySpark**

In de volgende tabel worden de klassemethoden van een PySpark MLEvaluator beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Splitst de inputdataset in opleiding en testondergroepen</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">dataframe</code>: Te splitsen gegevensset invoer</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Evalueert een opgeleid model en retourneert de evaluatieresultaten</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Zelfverwijzing</li>
                    <li><code class=" language-undefined">dataframe</code>: Een gegevenskader bestaande uit opleidings- en testgegevens</li>
                    <li><code class=" language-undefined">model</code>: Een getraind model</li>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In de volgende tabel worden de klassemethoden van een Spark MLEvaluator beschreven:

<table>
    <thead>
        <tr>
            <th>Methode en beschrijving</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Splitst de inputdataset in opleiding en testondergroepen</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">data</code>: Te splitsen gegevensset invoer</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Evalueert een opgeleid model en retourneert de evaluatieresultaten</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Configuratieeigenschappen</li>
                    <li><code class=" language-undefined">model</code>: Een getraind model</li>
                    <li><code class=" language-undefined">data</code>: Een gegevenskader bestaande uit opleidings- en testgegevens</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>