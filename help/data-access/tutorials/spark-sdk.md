---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Spark Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: f7714b8bebe37b29290794a48314962e42b24058
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Secure Spark Data Access SDK

De Secure Spark [!DNL Data Access] SDK is een softwareontwikkelkit waarmee gegevens van het Adobe Experience Platform kunnen worden gelezen en geschreven.

## Aan de slag

U moet het [authentificatieleerprogramma](../../tutorials/authentication.md) hebben voltooid om toegang tot de waarden te hebben om vraag aan Secure Spark [!DNL Data Access] SDK te maken:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Het gebruiken van SDK van de Vonk vereist de naam en identiteitskaart van de zandbak de verrichting in zal plaatsvinden:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

## Omgevingsinstelling

De [!DNL Spark] SDK verwacht dat u referenties opgeeft in omgevingsvariabelen of gegevensbronopties.

| Variabele | Waarde |
| -------- | ----- | 
| `SERVICE_TOKEN` | Uw token voor servicevergunning. |
| `SERVICE_API_KEY` | De API-sleutel voor uw service. Dit is doorgaans hetzelfde als uw IMS-client-id. |
| `ORG_ID` | Je `{IMS_ORG}` ID-waarde. |
| `USER_TOKEN` | Uw `{ACCESS_TOKEN}` waarde. |

Andere configuratieparameters zijn:

| Variabele | Waarde |
| -------- | ----- |
| `ENVIRONMENT_NAME` | De omgeving waarmee u verbinding probeert te maken. Het kan een van &quot;dev&quot;, &quot;stage&quot; of &quot;prod&quot; zijn. |
| `SANDBOX_NAME` | De naam van de sandbox waarmee u verbinding maakt. |

U kunt ook, afgezien van `ENVIRONMENT_NAME`de bovenstaande omgevingsvariabelen, instellen binnen `QSOption`, zoals in het onderstaande voorbeeld wordt getoond:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Installatie

Het gebruik van de [!DNL Spark] SDK vereist prestatieoptimalisaties die aan de `SparkSession`SDK moeten worden toegevoegd. U kunt deze op een van de volgende manieren toepassen:

Pas het rechtstreeks op huidige SparkSession toe:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Plaats de volgende conf vóór, of op de verwezenlijking SparkSession:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Een gegevensset lezen

De [!DNL Spark] SDK ondersteunt twee leesmodi: interactief en batchgewijs.

De interactieve wijze leidt tot een verbinding van de Connectiviteit van het Gegevensbestand van Java (JDBC) aan [!DNL Query Service] en krijgt resultaten door een regelmatige JDBC `ResultSet` die automatisch aan een `DataFrame`. wordt vertaald. Deze wijze werkt gelijkaardig aan de ingebouwde methode van de Vonk `spark.read.jdbc()`. Deze wijze wordt bedoeld slechts voor kleine datasets en vereist slechts een gebruikerstoken voor authentificatie.

In de modus Batch wordt [!DNL Query Service]de opdracht COPY gebruikt om de set met het resultaat van het Parket te genereren op een gedeelde locatie. Deze Parquet-bestanden kunnen vervolgens verder worden verwerkt. Deze wijze vereist zowel een gebruikerstoken als een de dienstteken met het `acp.foundation.catalog.credentials` werkingsgebied.

Een voorbeeld van het lezen van een dataset in interactieve wijze kan hieronder worden gezien:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

Op dezelfde manier kan een voorbeeld van het lezen van een dataset op partijwijze hieronder worden gezien:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

### Kolommen SELECTEREN uit de gegevensset

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT, component

Met de component DISTINCT kunt u alle afzonderlijke waarden op rij-/kolomniveau ophalen, waarbij alle dubbele waarden uit de reactie worden verwijderd.

Hieronder ziet u een voorbeeld van het gebruik van de `distinct()` functie:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-component

De [!DNL Spark] SDK biedt twee filtermethoden: Een SQL-expressie gebruiken of filteren door voorwaarden.

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

Met de ORDER BY-component kunnen ontvangen resultaten worden gesorteerd met een opgegeven kolom in een bepaalde volgorde (oplopend of aflopend). In de [!DNL Spark] SDK doet u dit door de `sort()` functie te gebruiken.

Hieronder ziet u een voorbeeld van het gebruik van de `sort()` functie:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-component

De clausule LIMIT staat gebruikers toe om het aantal verslagen te beperken die van de dataset worden ontvangen.

Hieronder ziet u een voorbeeld van het gebruik van de `limit()` functie:

```scala
df = df.limit(100)
```

## Schrijven naar een gegevensset

De [!DNL Spark] SDK ondersteunt het schrijven van gegevenssets. De gebruikers zullen eerst een vorige dataset moeten terugwinnen om aan een nieuwe dataset te schrijven.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
