---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevenstoegang;spark sdk;gegevenstoegang api;spark recipe;read spark;write spark
solution: Experience Platform
title: Toegang tot gegevens met Spark in Data Science Workspace
type: Tutorial
description: Het volgende document bevat voorbeelden van hoe te om tot gegevens toegang te hebben gebruikend Spark voor gebruik in de Werkruimte van de Wetenschap van Gegevens.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Toegang verkrijgen tot gegevens met Spark in Data Science Workspace

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten voor Data Science Workspace.

Het volgende document bevat voorbeelden van hoe te om tot gegevens toegang te hebben gebruikend Spark voor gebruik in de Werkruimte van de Wetenschap van Gegevens. Voor informatie bij de toegang tot van gegevens gebruikend JupyterLab notibooks, bezoek de [ JupyterLab- notitieboekengegevenstoegang ](../jupyterlab/access-notebook-data.md) documentatie.

## Aan de slag

Het gebruik van [!DNL Spark] vereist prestatieoptimalisaties die aan `SparkSession` moeten worden toegevoegd. Bovendien kunt u `configProperties` ook instellen voor later lezen van en schrijven naar gegevenssets.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Een gegevensset lezen

Tijdens het gebruik van Spark hebt u toegang tot twee leesmodi: interactief en batchgewijs.

Met de interactieve modus wordt een JDBC-verbinding (Java Database Connectivity) gemaakt met [!DNL Query Service] en worden resultaten verkregen via een gewone JDBC `ResultSet` die automatisch wordt omgezet in een `DataFrame` . Deze modus werkt net als de ingebouwde [!DNL Spark] methode `spark.read.jdbc()` . Deze modus is alleen bedoeld voor kleine datasets. Als uw gegevensset meer dan 5 miljoen rijen bevat, kunt u het beste overschakelen op de batchmodus.

In de batchmodus wordt de opdracht COPY van [!DNL Query Service] gebruikt om de resultaatsets van Parket te genereren op een gedeelde locatie. Deze Parquet-bestanden kunnen vervolgens verder worden verwerkt.

Hieronder ziet u een voorbeeld van het lezen van een gegevensset in de interactieve modus:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

Hieronder ziet u een voorbeeld van het lezen van een gegevensset in de batchmodus:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### Kolommen in de gegevensset SELECTEREN

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-component

Met de component DISTINCT kunt u alle afzonderlijke waarden op rij-/kolomniveau ophalen, waarbij alle dubbele waarden uit de reactie worden verwijderd.

Hieronder ziet u een voorbeeld van het gebruik van de functie `distinct()` :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-component

De [!DNL Spark] SDK biedt twee filtermethoden: het gebruik van een SQL-expressie of het filteren door omstandigheden.

Hieronder ziet u een voorbeeld van het gebruik van deze filterfuncties:

#### SQL-expressie

```scala
df.where("age > 15")
```

#### Filteromstandigheden

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY-component

Met de component ORDER BY kunnen ontvangen resultaten worden gesorteerd op een opgegeven kolom in een specifieke volgorde (oplopend of aflopend). In de [!DNL Spark] SDK gebeurt dit met behulp van de `sort()` -functie.

Hieronder ziet u een voorbeeld van het gebruik van de functie `sort()` :

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-component

Met de component LIMIT kunt u het aantal records beperken dat wordt ontvangen uit de gegevensset.

Hieronder ziet u een voorbeeld van het gebruik van de functie `limit()` :

```scala
df = df.limit(100)
```

## Schrijven naar een gegevensset

Met behulp van de `configProperties` -toewijzing kunt u met `QSOption` naar een gegevensset in een Experience Platform schrijven.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Volgende stappen

Adobe Experience Platform Data Science Workspace biedt een Scala (Spark)-receptvoorbeeld waarin de bovenstaande codevoorbeelden worden gebruikt om gegevens te lezen en te schrijven. Als u meer over wilt leren hoe te om Vonk voor de toegang tot van uw gegevens te gebruiken, te herzien gelieve de [&#128279;](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala) Bewaarplaats van de Opslag van GitHub van de Werkruimte van de Wetenschap van 0&rbrace; Gegevens Scala GitHub.
