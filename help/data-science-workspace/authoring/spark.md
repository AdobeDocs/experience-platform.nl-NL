---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevenstoegang;spark sdk;gegevenstoegang api;spark recept;read spark;write spark
solution: Experience Platform
title: Toegang tot gegevens die Vonk in de Werkruimte van de Wetenschap van Gegevens gebruiken
topic-legacy: tutorial
type: Tutorial
description: Het volgende document bevat voorbeelden op hoe te om tot gegevens toegang te hebben gebruikend Vonk voor gebruik in de Werkruimte van de Wetenschap van Gegevens.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Toegang tot gegevens die Vonk in de Werkruimte van de Wetenschap van Gegevens gebruiken

Het volgende document bevat voorbeelden op hoe te om tot gegevens toegang te hebben gebruikend Vonk voor gebruik in de Werkruimte van de Wetenschap van Gegevens. Raadpleeg de [JupyterLab-laptops voor toegang tot gegevens](../jupyterlab/access-notebook-data.md) documentatie voor informatie over toegang tot gegevens met JupyterLab-laptops.

## Aan de slag

Het gebruik van [!DNL Spark] vereist prestatieoptimalisaties die aan `SparkSession` moeten worden toegevoegd. Bovendien, kunt u `configProperties` voor recenter ook opstelling om aan datasets te lezen en te schrijven.

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

Terwijl het gebruiken van Vonk hebt u toegang tot twee wijzen van lezing: interactief en batchgewijs.

De interactieve wijze leidt tot een verbinding van de Connectiviteit van het Gegevensbestand van Java (JDBC) aan [!DNL Query Service] en krijgt resultaten door een regelmatige JDBC `ResultSet` die automatisch aan `DataFrame` wordt vertaald. Deze modus werkt net als de ingebouwde [!DNL Spark]-methode `spark.read.jdbc()`. Deze wijze wordt bedoeld slechts voor kleine datasets. Als uw dataset 5 miljoen rijen overschrijdt, wordt het geadviseerd u aan partijwijze ruilt.

In de modus Batch wordt de opdracht COPY van [!DNL Query Service] gebruikt om de set met het resultaat van het Parket te genereren op een gedeelde locatie. Deze Parquet-bestanden kunnen vervolgens verder worden verwerkt.

Een voorbeeld van het lezen van een dataset in interactieve wijze kan hieronder worden gezien:

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

Op dezelfde manier kan een voorbeeld van het lezen van een dataset op partijwijze hieronder worden gezien:

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

### Kolommen SELECTEREN uit de gegevensset

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT, component

Met de component DISTINCT kunt u alle afzonderlijke waarden op rij-/kolomniveau ophalen, waarbij alle dubbele waarden uit de reactie worden verwijderd.

Hieronder ziet u een voorbeeld van het gebruik van de functie `distinct()`:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-component

Met de SDK [!DNL Spark] zijn twee filtermethoden mogelijk: Een SQL-expressie gebruiken of filteren door voorwaarden.

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

Met de ORDER BY-component kunnen ontvangen resultaten worden gesorteerd met een opgegeven kolom in een bepaalde volgorde (oplopend of aflopend). In de [!DNL Spark] SDK, wordt dit gedaan door de `sort()` functie te gebruiken.

Hieronder ziet u een voorbeeld van het gebruik van de functie `sort()`:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-component

De clausule LIMIT staat u toe om het aantal verslagen te beperken die van de dataset worden ontvangen.

Hieronder ziet u een voorbeeld van het gebruik van de functie `limit()`:

```scala
df = df.limit(100)
```

## Schrijven naar een gegevensset

Gebruikend uw `configProperties` afbeelding, kunt u aan een dataset in Experience Platform schrijven gebruikend `QSOption`.

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

De Werkruimte van de Wetenschap van Gegevens van Adobe Experience Platform verstrekt een Scala (Vonk) receptensteekproef die de bovengenoemde codesteekproeven gebruikt om gegevens te lezen en te schrijven. Als u meer over wilt leren hoe te om Vonk voor de toegang tot van uw gegevens te gebruiken, te herzien gelieve [de Werkruimte van de Wetenschap van Gegevens Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
