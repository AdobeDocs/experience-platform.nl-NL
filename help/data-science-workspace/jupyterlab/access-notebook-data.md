---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;%dataset;interactive mode;batch mode;Spark sdk;python sdk;access data;notebook data access
solution: Experience Platform
title: Toegang tot gegevens in Jupyterlab-laptops
topic: Developer Guide
description: Deze handleiding is gericht op het gebruik van Jupyter-laptops, die zijn gemaakt in de Data Science Workspace voor toegang tot uw gegevens.
translation-type: tm+mt
source-git-commit: 645a0f595d268fb08ebfa5652f77a4b1628afcd3
workflow-type: tm+mt
source-wordcount: '3078'
ht-degree: 9%

---


# Toegang tot gegevens in [!DNL Jupyterlab] laptops

Elke ondersteunde kernel biedt ingebouwde functies waarmee u gegevens van een Platform in een notitieboekje kunt lezen. Momenteel ondersteunt JupyterLab in de Adobe Experience Platform Data Science Workspace laptops voor [!DNL Python], R, PySpark en Scala. De ondersteuning voor pagineringsgegevens is echter beperkt tot laptops [!DNL Python] en R-laptops. Deze handleiding is gericht op het gebruik van JupyterLab-laptops voor toegang tot uw gegevens.

## Aan de slag

Voordat u deze handleiding leest, moet u eerst de [[!DNL JupyterLab] gebruikershandleiding](./overview.md) bekijken voor een introductie op hoog niveau [!DNL JupyterLab] en de rol ervan in de werkruimte voor wetenschap van gegevens.

## Gegevenslimieten voor laptops {#notebook-data-limits}

>[!IMPORTANT]
>
>Voor PySpark- en Scala-laptops als u een fout ontvangt met de reden &quot;Remote RPC client disassociated&quot;. Dit betekent doorgaans dat de bestuurder of een uitvoerder onvoldoende geheugen heeft. Schakel over naar de modus [](#mode) &quot;batch&quot; om deze fout op te lossen.

De volgende informatie definieert de maximale hoeveelheid gegevens die kan worden gelezen, het type gegevens dat is gebruikt en het geschatte tijdsbestek waarin de gegevens worden gelezen.

Voor [!DNL Python] en R werd een notebookserver met een RAM van 40 GB gebruikt voor de benchmarks. Voor PySpark en Scala, werd een gegevensbestandcluster gevormd bij 64GB RAM, 8 kernen, 2 DBU met een maximum van 4 arbeiders gebruikt voor de hieronder vermelde benchmarks.

De gegevens in het ExperienceEvent-schema die werden gebruikt, varieerden van 100 (1K) rijen die oplopen tot 1 miljard (1B) rijen. Merk op dat voor PySpark en [!DNL Spark] metriek, een datumspanwijdte van 10 dagen voor de gegevens XDM werd gebruikt.

De ad-hocschemagegevens zijn vooraf verwerkt met [!DNL Query Service] Create Table as Select (CTAS). Deze gegevens varieerden ook in grootte die van duizend (1K) rijen die zich tot één miljard (1B) rijen uitstrekten.

### Wanneer wordt de batchmodus gebruikt in combinatie met de interactieve modus {#mode}

Wanneer het lezen van datasets met PySpark en Nota&#39;s Scala, hebt u de optie om interactieve wijze of partijwijze te gebruiken om de dataset te lezen. Interactief wordt gemaakt voor snelle resultaten terwijl de partijwijze voor grote datasets is.

- Voor PySpark- en Scala-laptops moet de batchmodus worden gebruikt wanneer 5 miljoen rijen gegevens of meer worden gelezen. Voor meer informatie over de efficiency van elke wijze, zie de [PySpark](#pyspark-data-limits) of [Scala](#scala-data-limits) - gegevenslimietlijsten hieronder.

### [!DNL Python] gegevenslimieten voor laptops

**XDM ExperienceEvent-schema:** U moet maximaal 2 miljoen rijen (~6.1 GB gegevens op schijf) XDM-gegevens in minder dan 22 minuten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Grootte op schijf (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (in seconden) | 20.3 | 86.8 | 63 | 659 | 1315 |

**ad-hocschema:** U moet maximaal 5 miljoen rijen (~5,6 GB gegevens op schijf) niet-XDM (ad-hocgegevens) in minder dan 14 minuten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Grootte op schijf (in MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in seconden) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R-laptopgegevenslimieten

**XDM ExperienceEvent-schema:** U moet maximaal 1 miljoen rijen XDM-gegevens (3 GB gegevens op schijf) kunnen lezen in minder dan 13 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Grootte op schijf (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (in seconden) | 14.03 | 69.6 | 86.8 | 775 |

**ad-hocschema:** U moet maximaal 3 miljoen rijen ad-hocgegevens (293 MB gegevens op schijf) kunnen lezen in ongeveer 10 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Grootte op schijf (in MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK (in sec) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark-[!DNL Python] laptopgegevenslimieten: {#pyspark-data-limits}

**XDM ExperienceEvent-schema:** In de interactieve modus kunt u maximaal 5 miljoen rijen (~13,42 GB gegevens op schijf) XDM-gegevens lezen in ongeveer 20 minuten. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op partijwijze te schakelen. In de batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK (interactieve modus) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (batchmodus) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**ad-hocschema:** In de interactieve modus kunt u maximaal 5 miljoen rijen (~5,36 GB gegevens op schijf) niet-XDM-gegevens lezen in minder dan 3 minuten. In de modus Batch kunt u maximaal 1 miljard rijen (ongeveer 1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 18 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Grootte op schijf | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interactieve SDK-modus (in seconden) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK-batchmodus (in seconden) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] Gegevenslimieten van laptops (Scala kernel): {#scala-data-limits}

**XDM ExperienceEvent-schema:** In de interactieve modus kunt u maximaal 5 miljoen rijen (~13,42 GB gegevens op schijf) XDM-gegevens lezen in ongeveer 18 minuten. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op partijwijze te schakelen. In de batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| Interactieve SDK-modus (in seconden) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK-batchmodus (in seconden) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**ad-hocschema:** Op interactieve wijze zou u een maximum van 5 miljoen rijen (~5.36GB gegevens op schijf) van niet-XDM gegevens in minder dan 3 minuten moeten kunnen lezen. In de batchmodus kunt u maximaal 1 miljard rijen (~1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 16 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Grootte op schijf | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interactieve SDK-modus (in seconden) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK-batchmodus (in seconden) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python-laptops {#python-notebook}

[!DNL Python] met notebooks kunt u gegevens pagineren wanneer u gegevenssets opent. De voorbeeldcode voor het lezen van gegevens met en zonder paginering wordt hieronder getoond. Ga voor meer informatie over de beschikbare starter Python laptops naar de sectie [[!DNL JupyterLab] Launcher](./overview.md#launcher) in de gebruikershandleiding van JupyterLab.

In de onderstaande Python-documentatie worden de volgende concepten beschreven:

- [Lezen van een dataset](#python-read-dataset)
- [Schrijven naar een gegevensset](#write-python)
- [Query-gegevens](#query-data-python)
- [Filter ExperienceEvent-gegevens](#python-filter)

### Lezen van een dataset in Python {#python-read-dataset}

**Zonder paginering:**

Het uitvoeren van de volgende code zal de volledige dataset lezen. Als de uitvoering is gelukt, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Met paginering:**

Het uitvoeren van de volgende code zal gegevens van de gespecificeerde dataset lezen. Paginering wordt bereikt door de gegevens te beperken en te verschuiven via de functies `limit()` en `offset()` . Het beperken van gegevens heeft betrekking op het maximumaantal gegevenspunten dat moet worden gelezen, terwijl het compenseren verwijst naar het aantal gegevenspunten dat vóór het lezen van gegevens moet worden overgeslagen. Als de leesbewerking met succes wordt uitgevoerd, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Schrijven naar een gegevensset in Python {#write-python}

Als u naar een gegevensset in uw JupyterLab-notitie wilt schrijven, selecteert u het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie Gegevens **[!UICONTROL schrijven in notitieboekje]** in het vervolgkeuzemenu op de dataset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

![](../images/jupyterlab/data-access/write-dataset.png)

- Het gebruik **[!UICONTROL schrijft Gegevens in Notitieboekje]** om een schrijfcel met uw geselecteerde dataset te produceren.
- Gebruik **[!UICONTROL Onderzoek Gegevens in Notitieboekje]** om een gelezen cel met uw geselecteerde dataset te produceren.
- De Gegevens van de **[!UICONTROL Vraag van het gebruik in Notitie]** om een basisvraagcel met uw geselecteerde dataset te produceren.

U kunt ook de volgende codecel kopiëren en plakken. Vervang zowel de `{DATASET_ID}` als `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Query-gegevens uitvoeren met [!DNL Query Service] In [!DNL Python] {#query-data-python}

[!DNL JupyterLab] op [!DNL Platform] staat u toe om SQL in een [!DNL Python] notitieboekje te gebruiken om tot gegevens door de Dienst [van de Vraag van](https://www.adobe.com/go/query-service-home-en)Adobe Experience Platform toegang te hebben. Toegang tot gegevens via [!DNL Query Service] kan nuttig zijn voor het omgaan met grote gegevenssets vanwege de superieure doorlooptijden. Houd er rekening mee dat het opvragen van gegevens met een verwerkingstijd van tien minuten [!DNL Query Service] heeft.

Voordat u [!DNL Query Service] de SQL-syntaxis [!DNL JupyterLab]gaat gebruiken, moet u controleren of u goed op de hoogte bent van de [[!DNL Query Service] SQL-syntaxis](https://www.adobe.com/go/query-service-sql-syntax-en).

Het vragen van gegevens die [!DNL Query Service] vereist u om de naam van de doeldataset te verstrekken. U kunt de noodzakelijke codecellen produceren door de gewenste dataset te vinden gebruikend de ontdekkingsreiziger **[!UICONTROL van]** Gegevens. Klik met de rechtermuisknop op de gegevenssetlijst en klik op **[!UICONTROL Query-gegevens in laptop]** om twee codecellen in uw laptop te genereren. Deze twee cellen worden hieronder gedetailleerder beschreven.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Als u [!DNL Query Service] in wilt gebruiken [!DNL JupyterLab], moet u eerst een verbinding maken tussen uw werkende [!DNL Python] laptop en [!DNL Query Service]. Dit kan worden bereikt door de eerste gegenereerde cel uit te voeren.

```python
qs_connect()
```

In de tweede gegenereerde cel moet de eerste regel worden gedefinieerd vóór de SQL-query. Door gebrek, bepaalt de geproduceerde cel een facultatieve variabele (`df0`) die de vraagresultaten als dataframe van de Pandas bewaart. <br>Het `-c QS_CONNECTION` argument is verplicht en geeft de kernel de opdracht om de SQL-query uit te voeren [!DNL Query Service]. Zie de [bijlage](#optional-sql-flags-for-query-service) voor een lijst van extra argumenten.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Er kan rechtstreeks naar Python-variabelen worden verwezen binnen een SQL-query met behulp van een syntaxis met tekenreeksindeling en de variabelen tussen accolades (`{}`), zoals in het volgende voorbeeld wordt getoond:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Gegevens filteren [!DNL ExperienceEvent] {#python-filter}

Om tot een [!DNL ExperienceEvent] dataset in een [!DNL Python] notitieboekje toegang te hebben en te filtreren, moet u identiteitskaart van de dataset (`{DATASET_ID}`) samen met de filterregels verstrekken die een specifieke tijdwaaier gebruikend logische exploitanten bepalen. Wanneer een tijdwaaier wordt bepaald, wordt om het even welke gespecificeerde paginering genegeerd en de volledige dataset wordt overwogen.

Een lijst met filteroperatoren wordt hieronder beschreven:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Logische operator AND
- `Or()`: Logische operator OR

De volgende cel filtert een [!DNL ExperienceEvent] dataset aan gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R-laptops {#r-notebooks}

Met R-laptops kunt u gegevens pagineren wanneer u gegevenssets opent. De voorbeeldcode voor het lezen van gegevens met en zonder paginering wordt hieronder getoond. Ga voor meer informatie over de beschikbare starter R-laptops naar de sectie [[!DNL JupyterLab] Launcher](./overview.md#launcher) in de gebruikershandleiding van JupyterLab.

In de onderstaande R-documentatie worden de volgende concepten beschreven:

- [Lezen van een dataset](#r-read-dataset)
- [Schrijven naar een gegevensset](#write-r)
- [Filter ExperienceEvent-gegevens](#r-filter)

### Lezen van een dataset in R {#r-read-dataset}

**Zonder paginering:**

Het uitvoeren van de volgende code zal de volledige dataset lezen. Als de uitvoering is gelukt, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Met paginering:**

Het uitvoeren van de volgende code zal gegevens van de gespecificeerde dataset lezen. Paginering wordt bereikt door de gegevens te beperken en te verschuiven via de functies `limit()` en `offset()` . Het beperken van gegevens heeft betrekking op het maximumaantal gegevenspunten dat moet worden gelezen, terwijl het compenseren verwijst naar het aantal gegevenspunten dat vóór het lezen van gegevens moet worden overgeslagen. Als de leesbewerking met succes wordt uitgevoerd, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Schrijf aan een dataset in R {#write-r}

Als u naar een gegevensset in uw JupyterLab-notitie wilt schrijven, selecteert u het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie Gegevens **[!UICONTROL schrijven in notitieboekje]** in het vervolgkeuzemenu op de dataset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Het gebruik **[!UICONTROL schrijft Gegevens in Notitieboekje]** om een schrijfcel met uw geselecteerde dataset te produceren.
- Gebruik **[!UICONTROL Onderzoek Gegevens in Notitieboekje]** om een gelezen cel met uw geselecteerde dataset te produceren.

U kunt ook de volgende codecel kopiëren en plakken:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Gegevens filteren [!DNL ExperienceEvent] {#r-filter}

Om tot een [!DNL ExperienceEvent] dataset in een notitieboekje van R toegang te hebben en te filtreren, moet u identiteitskaart van de dataset (`{DATASET_ID}`) samen met de filterregels verstrekken die een specifieke tijdwaaier gebruikend logische exploitanten bepalen. Wanneer een tijdwaaier wordt bepaald, wordt om het even welke gespecificeerde paginering genegeerd en de volledige dataset wordt overwogen.

Een lijst met filteroperatoren wordt hieronder beschreven:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Logische operator AND
- `Or()`: Logische operator OR

De volgende cel filtert een [!DNL ExperienceEvent] dataset aan gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3 notebooks {#pyspark-notebook}

De documentatie PySpark beschrijft hieronder de volgende concepten:

- [sparkSession initialiseren](#spark-initialize)
- [Gegevens lezen en schrijven](#magic)
- [Een lokaal gegevensbestand maken](#pyspark-create-dataframe)
- [Filter ExperienceEvent-gegevens](#pyspark-filter-experienceevent)

### sparkSession initialiseren {#spark-initialize}

Alle [!DNL Spark] 2.4 laptops vereisen dat u de zitting met de volgende boilerplate code initialiseert.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Het gebruiken van %dataset om met een PySpark 3 notitieboekje te lezen en te schrijven {#magic}

Met de introductie van [!DNL Spark] 2.4 wordt `%dataset` aangepaste magie geleverd voor gebruik in PySpark 3 ([!DNL Spark] 2.4) notebooks. Voor meer details over magische bevelen beschikbaar in de pit IPython, bezoek de [toverdocumentatie](https://ipython.readthedocs.io/en/stable/interactive/magics.html)IPython.


**Gebruik**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**Beschrijving**

Een aangepaste opdracht voor het [!DNL Data Science Workspace] schrijven of lezen van een gegevensset van een [!DNL PySpark] laptop ([!DNL Python] 3 kernel).

| Naam | Beschrijving | Vereist |
| --- | --- | --- |
| `{action}` | Het type van actie op de dataset uit te voeren. Er zijn twee handelingen beschikbaar: &quot;read&quot; of &quot;write&quot;. | Ja |
| `--datasetId {id}` | Gebruikt om identiteitskaart van de dataset te leveren om te lezen of te schrijven. | Ja |
| `--dataFrame {df}` | Het dataframe van de pandas. <ul><li> Wanneer de handeling &quot;read&quot; is, is {df} de variabele waar de resultaten van de bewerking voor het lezen van de gegevensset beschikbaar zijn. </li><li> Wanneer de actie &quot;schrijven&quot;is, wordt dit dataframe {df} geschreven aan de dataset. </li></ul> | Ja |
| `--mode` | Een extra parameter die wijzigt hoe gegevens worden gelezen. Toegestane parameters zijn &quot;batch&quot; en &quot;interactief&quot;. De modus is standaard ingesteld op &quot;interactief&quot;. Het wordt aanbevolen de modus &quot;batch&quot; te gebruiken bij het lezen van grote hoeveelheden gegevens. | Nee |

>[!TIP]
>
>Bekijk de PySpark-tabellen in de sectie [voor de gegevenslimieten](#notebook-data-limits) van laptops om te bepalen of `mode` deze moeten worden ingesteld op `interactive` of `batch`.

**Voorbeelden**

- **Voorbeeld** lezen: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Voorbeeld** schrijven: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

U kunt de bovenstaande voorbeelden automatisch genereren bij het aanschaffen van JupyterLab met de volgende methode:

Selecteer het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie Gegevens **[!UICONTROL schrijven in notitieboekje]** in het vervolgkeuzemenu op de dataset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

- Gebruik Gegevens **[!UICONTROL verkennen in laptop]** om een leescel te genereren.
- Gebruik Gegevens **[!UICONTROL schrijven in Notitieboekje]** om een schrijfcel te genereren.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Een lokaal gegevensbestand maken {#pyspark-create-dataframe}

Om een lokaal dataframe tot stand te brengen gebruikend PySpark 3 gebruik SQL vragen. Bijvoorbeeld:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>U kunt ook een optioneel zaadmonster opgeven, zoals een booleaan met Vervanging, een dubbele fractie of een lang zaadmonster.

### Gegevens filteren [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

De toegang tot van en het filtreren van een [!DNL ExperienceEvent] dataset in een notitieboekje PySpark vereist u om de gegevenssetidentiteit (`{DATASET_ID}`), de identiteit van IMS van uw organisatie, en de filterregels te verstrekken die een specifieke tijdwaaier bepalen. Een het filtreren tijdwaaier wordt bepaald door de functie te gebruiken `spark.sql()`, waar de functieparameter een SQL vraagkoord is.

De volgende cellen filteren een [!DNL ExperienceEvent] dataset aan gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Scala-laptops {#scala-notebook}

De onderstaande documentatie bevat voorbeelden van de volgende concepten:

- [sparkSession initialiseren](#scala-initialize)
- [Een gegevensset lezen](#read-scala-dataset)
- [Schrijven naar een gegevensset](#scala-write-dataset)
- [Een lokaal gegevensbestand maken](#scala-create-dataframe)
- [Filter ExperienceEvent-gegevens](#scala-experienceevent)

### SparkSession initialiseren {#scala-initialize}

Alle Scala-laptops vereisen dat u de sessie initialiseert met de volgende bouwsteencode:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Een gegevensset lezen {#read-scala-dataset}

In Scala, kunt u invoeren `clientContext` om Platforms waarden te krijgen en terug te keren, elimineert dit de behoefte om variabelen zoals `var userToken`te bepalen. In het Scala voorbeeld hieronder, `clientContext` wordt gebruikt om alle vereiste waarden te krijgen en terug te keren nodig voor het lezen van een dataset.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Element | Beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `clientContext.getUserToken()`. |
| service-token | Uw servicetoken dat automatisch wordt opgehaald met `clientContext.getServiceToken()`. |
| ims-org | Uw IMS-organisatie-id wordt automatisch opgehaald met `clientContext.getOrgId()`. |
| api-toets | De API-sleutel die automatisch wordt opgehaald met `clientContext.getApiKey()`. |

>[!TIP]
>
>Bekijk de Scala-tabellen in de sectie [Gegevenslimieten](#notebook-data-limits) voor laptops om te bepalen of `mode` deze moeten worden ingesteld op `interactive` of `batch`.

U kunt het bovenstaande voorbeeld automatisch genereren bij het aanschaffen van JupyterLab met de volgende methode:

Selecteer het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop, dan selecteren **[!UICONTROL onderzoek Gegevens in Notitie]** van het drop-down menu op de dataset u wenst te gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.
en
- Gebruik Gegevens **[!UICONTROL verkennen in laptop]** om een leescel te genereren.
- Gebruik Gegevens **[!UICONTROL schrijven in Notitieboekje]** om een schrijfcel te genereren.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Schrijven naar een gegevensset {#scala-write-dataset}

In Scala, kunt u invoeren `clientContext` om Platforms waarden te krijgen en terug te keren, elimineert dit de behoefte om variabelen zoals `var userToken`te bepalen. In het Scala voorbeeld hieronder, `clientContext` wordt gebruikt om alle vereiste waarden te bepalen en terug te keren nodig om aan een dataset te schrijven.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `clientContext.getUserToken()`. |
| service-token | Uw servicetoken dat automatisch wordt opgehaald met `clientContext.getServiceToken()`. |
| ims-org | Uw IMS-organisatie-id wordt automatisch opgehaald met `clientContext.getOrgId()`. |
| api-toets | De API-sleutel die automatisch wordt opgehaald met `clientContext.getApiKey()`. |

>[!TIP]
>
>Bekijk de Scala-tabellen in de sectie [Gegevenslimieten](#notebook-data-limits) voor laptops om te bepalen of `mode` deze moeten worden ingesteld op `interactive` of `batch`.

### een lokaal dataframe maken {#scala-create-dataframe}

SQL-query&#39;s zijn vereist voor het maken van een lokaal dataframe met Scala. Bijvoorbeeld:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Gegevens filteren [!DNL ExperienceEvent] {#scala-experienceevent}

Als u toegang wilt tot en filtert op een [!DNL ExperienceEvent] gegevensset in een Scala-laptop, moet u de identiteit (`{DATASET_ID}`) van de gegevensset, de IMS-identiteit van uw organisatie en de filterregels die een specifiek tijdbereik definiëren, opgeven. Een het Filtreren tijdwaaier wordt bepaald door de functie te gebruiken `spark.sql()`, waar de functieparameter een SQL vraagkoord is.

De volgende cellen filteren een [!DNL ExperienceEvent] dataset aan gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Volgende stappen

In dit document worden de algemene richtlijnen besproken voor toegang tot gegevenssets met JupyterLab-laptops. Voor meer diepgaande voorbeelden bij het vragen van datasets, bezoek de Dienst van de [Vraag in JupyterLab notitieboekendocumentatie](./query-service.md) . Meer informatie over het verkennen en visualiseren van uw gegevenssets vindt u in het document over het [analyseren van uw gegevens met behulp van laptops](./analyze-your-data.md).

## Optionele SQL-markeringen voor [!DNL Query Service] {#optional-sql-flags-for-query-service}

In deze tabel staan de optionele SQL-markeringen waarvoor u kunt kiezen [!DNL Query Service].

| **Markering** | **Beschrijving** |
| --- | --- |
| `-h`, `--help` | Help-bericht weergeven en afsluiten. |
| `-n`, `--notify` | Optie in-/uitschakelen voor het melden van queryresultaten. |
| `-a`, `--async` | Als u deze markering gebruikt, wordt de query asynchroon uitgevoerd en kan de kernel vrijkomen terwijl de query wordt uitgevoerd. Wees voorzichtig wanneer u queryresultaten toewijst aan variabelen, omdat deze mogelijk niet gedefinieerd zijn als de query niet volledig is. |
| `-d`, `--display` | Met deze markering voorkomt u dat resultaten worden weergegeven. |

