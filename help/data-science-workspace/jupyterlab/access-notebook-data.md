---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populaire onderwerpen;%dataset;interactieve modus;batchmodus;Spark sdk;python sdk;toegang tot gegevens;laptop toegang tot gegevens
solution: Experience Platform
title: Toegang tot gegevens in Jupyterlab-laptops
description: Deze gids concentreert zich op hoe te om Notities van Jupyter te gebruiken, die binnen de Wetenschap van Gegevens Workspace worden gebouwd om tot uw gegevens toegang te hebben.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3276'
ht-degree: 2%

---

# Toegang tot gegevens in [!DNL Jupyterlab] laptops

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Elke ondersteunde kernel biedt ingebouwde functies waarmee u Experience Platform-gegevens kunt lezen van een gegevensset in een laptop. JupyterLab in Adobe Experience Platform Data Science Workspace ondersteunt momenteel laptops voor [!DNL Python] , R, PySpark en Scala. Ondersteuning voor paginering van gegevens is echter beperkt tot [!DNL Python] - en R-laptops. Deze handleiding is gericht op het gebruik van JupyterLab-laptops voor toegang tot uw gegevens.

## Aan de slag

Alvorens deze gids te lezen, te herzien gelieve de [[!DNL JupyterLab]  gebruikersgids ](./overview.md) voor een inleiding op hoog niveau aan [!DNL JupyterLab] en zijn rol binnen de Wetenschap van Gegevens Workspace.

## Gegevenslimieten voor laptops {#notebook-data-limits}

>[!IMPORTANT]
>
>Voor PySpark- en Scala-laptops als u een fout ontvangt met de reden &quot;Remote RPC client disassociated&quot;. Dit betekent doorgaans dat de bestuurder of een uitvoerder onvoldoende geheugen heeft. Probeer over te schakelen op [ &quot;partij&quot;wijze ](#mode) om deze fout op te lossen.

De volgende informatie definieert de maximale hoeveelheid gegevens die kan worden gelezen, het type gegevens dat is gebruikt en het geschatte tijdsbestek waarin de gegevens worden gelezen.

Voor [!DNL Python] en R werd een notebookserver met een RAM van 40 GB gebruikt voor de benchmarks. Voor PySpark en Scala, werd een gegevensbestandcluster gevormd bij 64GB RAM, 8 kernen, 2 DBU met een maximum van 4 arbeiders gebruikt voor de hieronder vermelde benchmarks.

De gegevens in het ExperienceEvent-schema die werden gebruikt, varieerden van 100 (1K) rijen die oplopen tot 1 miljard (1B) rijen. Merk op dat voor PySpark en [!DNL Spark] metriek, een datumspanwijdte van 10 dagen werd gebruikt voor de gegevens XDM.

De ad-hocschemagegevens zijn vooraf verwerkt met [!DNL Query Service] Tabel maken als selectie (CTAS). Deze gegevens varieerden ook in grootte die van duizend (1K) rijen die zich tot één miljard (1B) rijen uitstrekten.

### Wanneer wordt de batchmodus gebruikt in combinatie met de interactieve modus {#mode}

Wanneer het lezen van datasets met PySpark en Nota&#39;s Scala, hebt u de optie om interactieve wijze of partijwijze te gebruiken om de dataset te lezen. Interactief wordt gemaakt voor snelle resultaten terwijl de partijwijze voor grote datasets is.

- Voor PySpark- en Scala-laptops moet de batchmodus worden gebruikt wanneer 5 miljoen rijen gegevens of meer worden gelezen. Voor meer informatie over de efficiency van elke wijze, zie [ PySpark ](#pyspark-data-limits) of [ Scala ](#scala-data-limits) hieronder lijsten van de gegevensgrens.

### [!DNL Python] gegevenslimieten voor laptops

**XDM ExperienceEvent schema:** U zou een maximum van 2 miljoen rijen (~6.1 GB gegevens op schijf) van XDM gegevens in minder dan 22 minuten moeten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Grootte op schijf (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in seconden) | 20,3 | 86,8 | 63 | 659 | 1315 |

**ad-hoc schema:** u zou een maximum van 5 miljoen rijen (~5.6 GB gegevens op schijf) van niet-XDM (ad-hoc) gegevens in minder dan 14 minuten moeten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB | 5 MB |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Grootte op schijf (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in seconden) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### R-laptopgegevenslimieten

**XDM ExperienceEvent schema:** u zou een maximum van 1 miljoen rijen van XDM gegevens (3 GB gegevens op schijf) in onder 13 minuten moeten kunnen lezen.

| Aantal rijen | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Grootte op schijf (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (in seconden) | 14,03 | 69,6 | 86,8 | 775 |

**ad-hoc schema:** u zou een maximum van 3 miljoen rijen van ad-hocgegevens (293MB gegevens op schijf) in rond 10 minuten moeten kunnen lezen.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Grootte op schijf (in MB) | 0,082 | 0,612 | 9,0 | 91 | 188 | 293 |
| R SDK (in sec) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### PySpark-laptopgegevenslimieten ([!DNL Python] kernel): {#pyspark-data-limits}

**XDM ExperienceEvent schema:** Op interactieve wijze zou u een maximum van 5 miljoen rijen (~13.42GB gegevens op schijf) van XDM gegevens in rond 20 minuten moeten kunnen lezen. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op partijwijze te schakelen. In de batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB | 5 MB | 10 MB | 50 MB | 100 MB | 500 MB |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2,93 MB | 4,38 MB | 29,02 | 2,69 GB | 5,39 GB | 8,09 GB | 13,42 GB | 26,82 GB | 134,24 GB | 268,39 GB | 1,31 TB |
| SDK (interactieve modus) | 33 s | 32,4 s | 55,1s | 253,5 s | 489,2 s | 729,6 s | 1206,8s | - | - | - | - |
| SDK (Batch-modus) | 815,8 s | 492,8 s | 379,1s | 637,4 s | 624,5 s | 869,2s | 1104.1s | 1786s | 5387,2s | 10624,6s | 50547s |

**ad-hoc schema:** op Interactieve wijze zou u een maximum van 5 miljoen rijen (~5.36GB gegevens op schijf) van niet-XDM gegevens in minder dan 3 minuten moeten kunnen lezen. In de modus Batch kunt u maximaal 1 miljard rijen (ongeveer 1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 18 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB | 5 MB | 10 MB | 50 MB | 100 MB | 500 MB | 1 ter |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Grootte op schijf | 1,12 MB | 11,24 MB | 109,48 MB | 2,69 GB | 2,14 GB | 3,21 GB | 5,36 GB | 10,71 GB | 53,58 GB | 107,52 GB | 535,88 GB | 1,05 TB |
| SDK Interactive-modus (in seconden) | 28,2 s | 18,6 s | 20,8 s | 20,9 s | 23,8 s | 21,7 s | 24,7 s | - | - | - | - | - |
| SDK-batchmodus (in seconden) | 428,8 s | 578,8 s | 641,4s | 538,5 s | 630,9s | 467,3 s | 411s | 675 s | 702 s | 719,2s | 1022.1s | 1122,3s |

### [!DNL Spark] (Scala kernel) laptopgegevenslimieten: {#scala-data-limits}

**XDM ExperienceEvent schema:** Op interactieve wijze zou u een maximum van 5 miljoen rijen (~13.42GB gegevens op schijf) van XDM gegevens in rond 18 minuten moeten kunnen lezen. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op partijwijze te schakelen. In de batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB | 5 MB | 10 MB | 50 MB | 100 MB | 500 MB |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2,93 MB | 4,38 MB | 29,02 | 2,69 GB | 5,39 GB | 8,09 GB | 13,42 GB | 26,82 GB | 134,24 GB | 268,39 GB | 1,31 TB |
| SDK Interactive-modus (in seconden) | 37,9 s | 22,7 s | 45,6 s | 231,7 s | 444,7 s | 660,6 s | 1100s | - | - | - | - |
| SDK-batchmodus (in seconden) | 374,4 s | 398,5 s | 527s | 487,9 s | 588,9s | 829s | 939,1s | 1441s | 5473,2s | 10118,8 | 49207,6 |

**ad-hoc schema:** op interactieve wijze zou u een maximum van 5 miljoen rijen (~5.36GB gegevens op schijf) van niet-XDM gegevens in minder dan 3 minuten moeten kunnen lezen. In de batchmodus kunt u maximaal 1 miljard rijen (~1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 16 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2 MB | 3 MB | 5 MB | 10 MB | 50 MB | 100 MB | 500 MB | 1 ter |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Grootte op schijf | 1,12 MB | 11,24 MB | 109,48 MB | 2,69 GB | 2,14 GB | 3,21 GB | 5,36 GB | 10,71 GB | 53,58 GB | 107,52 GB | 535,88 GB | 1,05 TB |
| SDK Interactive-modus (in seconden) | 35,7 s | 31s | 19,5 s | 25,3 s | 23 s | 33,2 s | 25,5 s | - | - | - | - | - |
| SDK-batchmodus (in seconden) | 448,8 s | 459,7 s | 519s | 475,8 s | 599,9s | 347,6 s | 407,8 s | 397 s | 518,8 s | 487,9 s | 760,2s | 975,4s |

## Python-laptops {#python-notebook}

Met [!DNL Python] -laptops kunt u gegevens pagineren wanneer u gegevenssets opent. De voorbeeldcode voor het lezen van gegevens met en zonder paginering wordt hieronder getoond. Voor meer informatie over de beschikbare starter laptops van de Python, bezoek de ](./overview.md#launcher) sectie van de Lanceerinrichting [[!DNL JupyterLab]  binnen de JupyterLab gebruikersgids.

In de onderstaande Python-documentatie worden de volgende concepten beschreven:

- [Lezen van een dataset](#python-read-dataset)
- [Schrijven naar een gegevensset](#write-python)
- [Querygegevens](#query-data-python)
- [Filter ExperienceEvent-gegevens](#python-filter)

### Lezen van een dataset in Python {#python-read-dataset}

**Zonder paginering:**

Het uitvoeren van de volgende code zal de volledige dataset lezen. Als de uitvoering is gelukt, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele `df` wordt verwezen.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**met paginering:**

Het uitvoeren van de volgende code zal gegevens van de gespecificeerde dataset lezen. Paginering wordt bereikt door het beperken en verschuiven van gegevens via respectievelijk de functies `limit()` en `offset()` . Het beperken van gegevens heeft betrekking op het maximumaantal gegevenspunten dat moet worden gelezen, terwijl het compenseren verwijst naar het aantal gegevenspunten dat vóór het lezen van gegevens moet worden overgeslagen. Als de leesbewerking met succes wordt uitgevoerd, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele `df` wordt verwezen.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Schrijven naar een gegevensset in Python {#write-python}

Als u naar een gegevensset in uw JupyterLab-notitie wilt schrijven, selecteert u het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie **[!UICONTROL Write Data in Notebook]** in het vervolgkeuzemenu in de gegevensset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

![](../images/jupyterlab/data-access/write-dataset.png)

- Gebruik **[!UICONTROL Write Data in Notebook]** om een schrijfcel met uw geselecteerde dataset te produceren.
- Gebruik **[!UICONTROL Explore Data in Notebook]** om een leescel te genereren met de geselecteerde gegevensset.
- Gebruik **[!UICONTROL Query Data in Notebook]** om een basisvraagcel met uw geselecteerde dataset te produceren.

U kunt ook de volgende codecel kopiëren en plakken. Vervang zowel `{DATASET_ID}` als `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Query-gegevens uitvoeren met [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] op [!DNL Experience Platform] staat u toe om SQL in a [!DNL Python] notitieboekje te gebruiken om tot gegevens door [ de Dienst van de Vraag van Adobe Experience Platform ](https://www.adobe.com/go/query-service-home-en) toegang te hebben. Toegang tot gegevens via [!DNL Query Service] kan handig zijn voor het verwerken van grote gegevenssets vanwege de superieure runtime. Houd er rekening mee dat het opvragen van gegevens met [!DNL Query Service] een verwerkingstijd van tien minuten heeft.

Alvorens u [!DNL Query Service] in [!DNL JupyterLab] gebruikt, zorg ervoor u een werkend begrip van de [[!DNL Query Service]  SQL syntaxis ](https://www.adobe.com/go/query-service-sql-syntax-en) hebt.

Voor het aanvragen van gegevens met [!DNL Query Service] moet u de naam van de doelgegevensset opgeven. U kunt de noodzakelijke codecellen produceren door de gewenste dataset te vinden gebruikend **[!UICONTROL Data explorer]**. Klik met de rechtermuisknop op de gegevenssetlijst en klik op **[!UICONTROL Query Data in Notebook]** om twee codecellen in uw notitieboekje te genereren. Deze twee cellen worden hieronder gedetailleerder beschreven.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Als u [!DNL Query Service] in [!DNL JupyterLab] wilt gebruiken, moet u eerst een verbinding maken tussen uw [!DNL Python] -laptop en [!DNL Query Service] . Dit kan worden bereikt door de eerste gegenereerde cel uit te voeren.

```python
qs_connect()
```

In de tweede gegenereerde cel moet de eerste regel worden gedefinieerd vóór de SQL-query. Door gebrek, bepaalt de geproduceerde cel een facultatieve variabele (`df0`) die de vraagresultaten als dataframe van de Pandas bewaart. <br> het `-c QS_CONNECTION` argument is verplicht en vertelt de kernel om de SQL vraag tegen [!DNL Query Service] uit te voeren. Zie [ bijlage ](#optional-sql-flags-for-query-service) voor een lijst van extra argumenten.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

De variabelen van de Python kunnen direct binnen een SQL vraag worden van verwijzingen voorzien door koord-geformatteerde syntaxis te gebruiken en de variabelen in krullende steunen (`{}`), zoals aangetoond in het volgende voorbeeld te verpakken:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter [!DNL ExperienceEvent] gegevens {#python-filter}

Als u een [!DNL ExperienceEvent] dataset in een [!DNL Python] notitieboekje wilt openen en filteren, moet u de identiteitskaart van de dataset (`{DATASET_ID}`) samen met de filterregels verstrekken die een specifieke tijdwaaier gebruikend logische exploitanten bepalen. Wanneer een tijdwaaier wordt bepaald, wordt om het even welke gespecificeerde paginering genegeerd en de volledige dataset wordt overwogen.

Een lijst met filteroperatoren wordt hieronder beschreven:

- `eq()`: gelijk aan
- `gt()`: groter dan
- `ge()`: groter dan of gelijk aan
- `lt()`: Minder dan
- `le()`: kleiner dan of gelijk aan
- `And()`: Logische operator AND
- `Or()`: operator voor logische OR

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

Met R-laptops kunt u gegevens pagineren wanneer u gegevenssets opent. De voorbeeldcode voor het lezen van gegevens met en zonder paginering wordt hieronder getoond. Voor meer informatie over de beschikbare aanzetR laptops, bezoek de ](./overview.md#launcher) sectie van de Lanceerinrichting [[!DNL JupyterLab]  binnen de JupyterLab gebruikersgids.

In de onderstaande R-documentatie worden de volgende concepten beschreven:

- [Lezen van een dataset](#r-read-dataset)
- [Schrijven naar een gegevensset](#write-r)
- [Filter ExperienceEvent-gegevens](#r-filter)

### Lezen van een dataset in R {#r-read-dataset}

**Zonder paginering:**

Het uitvoeren van de volgende code zal de volledige dataset lezen. Als de uitvoering is gelukt, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele `df0` wordt verwezen.

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

**met paginering:**

Het uitvoeren van de volgende code zal gegevens van de gespecificeerde dataset lezen. Paginering wordt bereikt door het beperken en verschuiven van gegevens via respectievelijk de functies `limit()` en `offset()` . Het beperken van gegevens heeft betrekking op het maximumaantal gegevenspunten dat moet worden gelezen, terwijl het compenseren verwijst naar het aantal gegevenspunten dat vóór het lezen van gegevens moet worden overgeslagen. Als de leesbewerking met succes wordt uitgevoerd, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele `df0` wordt verwezen.

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

Als u naar een gegevensset in uw JupyterLab-notitie wilt schrijven, selecteert u het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie **[!UICONTROL Write Data in Notebook]** in het vervolgkeuzemenu in de gegevensset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Gebruik **[!UICONTROL Write Data in Notebook]** om een schrijfcel met uw geselecteerde dataset te produceren.
- Gebruik **[!UICONTROL Explore Data in Notebook]** om een leescel te genereren met de geselecteerde gegevensset.

U kunt ook de volgende codecel kopiëren en plakken:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filter [!DNL ExperienceEvent] gegevens {#r-filter}

Om tot een [!DNL ExperienceEvent] dataset in een notitieboekje van R toegang te hebben en te filtreren, moet u identiteitskaart van de dataset (`{DATASET_ID}`) samen met de filterregels verstrekken die een specifieke tijdwaaier gebruikend logische exploitanten bepalen. Wanneer een tijdwaaier wordt bepaald, wordt om het even welke gespecificeerde paginering genegeerd en de volledige dataset wordt overwogen.

Een lijst met filteroperatoren wordt hieronder beschreven:

- `eq()`: gelijk aan
- `gt()`: groter dan
- `ge()`: groter dan of gelijk aan
- `lt()`: Minder dan
- `le()`: kleiner dan of gelijk aan
- `And()`: Logische operator AND
- `Or()`: operator voor logische OR

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

De documentatie PySpark schetst hieronder de volgende concepten:

- [sparkSession initialiseren](#spark-initialize)
- [Gegevens lezen en schrijven](#magic)
- [Een lokaal gegevensbestand maken](#pyspark-create-dataframe)
- [Filter ExperienceEvent-gegevens](#pyspark-filter-experienceevent)

### sparkSession initialiseren {#spark-initialize}

Voor alle [!DNL Spark] 2.4-laptops moet u de sessie initialiseren met de volgende vaste code.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### %dataset gebruiken om te lezen en te schrijven met een PySpark 3-laptop {#magic}

Met de introductie van [!DNL Spark] 2.4, wordt `%dataset` magie geleverd voor gebruik in PySpark 3 ([!DNL Spark] 2.4) laptops. Voor meer details op magische bevelen beschikbaar in de pit IPython, bezoek de [ IPython magische documentatie ](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Gebruik**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Beschrijving**

Een aangepaste toveropdracht [!DNL Data Science Workspace] voor het lezen of schrijven van een gegevensset van een [!DNL PySpark] -laptop ([!DNL Python] 3-kernel).

| Naam | Beschrijving | Vereist |
| --- | --- | --- |
| `{action}` | Het type van actie op de dataset uit te voeren. Er zijn twee handelingen beschikbaar: &quot;read&quot; of &quot;write&quot;. | Ja |
| `--datasetId {id}` | Gebruikt om identiteitskaart van de dataset te leveren om te lezen of te schrijven. | Ja |
| `--dataFrame {df}` | Het dataframe van de pandas. <ul><li> Wanneer de handeling &quot;read&quot; is, is {df} de variabele waar de resultaten van de bewerking voor het lezen van de gegevensset beschikbaar zijn (zoals een gegevenskader). </li><li> Wanneer de actie &quot;schrijven&quot;is, wordt dit dataframe {df} geschreven aan de dataset. </li></ul> | Ja |
| `--mode` | Een extra parameter die wijzigt hoe gegevens worden gelezen. Toegestane parameters zijn &quot;batch&quot; en &quot;interactief&quot;. De modus is standaard ingesteld op &quot;batch&quot;.<br> Het wordt geadviseerd u &quot;interactieve&quot;wijze voor verhoogde vraagprestaties op kleinere datasets. | Ja |

>[!TIP]
>
>Herzie de PySpark lijsten binnen de [ sectie van de notitieboekjegegevens ](#notebook-data-limits) om te bepalen als `mode` aan `interactive` of `batch` zou moeten worden geplaatst.

**Voorbeelden**

- **Gelezen voorbeeld**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **schrijf voorbeeld**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Gegevens in cache plaatsen met `df.cache()` voordat gegevens worden geschreven, kan de prestaties van een laptop aanzienlijk verbeteren. Dit kan helpen als u een van de volgende fouten ontvangt:
> 
> - Taak afgebroken vanwege een fout in het werkgebied... Kan alleen RDD&#39;s met hetzelfde aantal elementen in elke partitie comprimeren.
> - Externe RPC-client uitgeschakeld en andere geheugenfouten.
> - Slechte prestaties bij het lezen en schrijven van datasets.
> 
> Zie de [ het oplossen van problemengids ](../troubleshooting-guide.md) voor meer informatie.

U kunt de bovenstaande voorbeelden automatisch genereren bij het aanschaffen van JupyterLab met de volgende methode:

Selecteer het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie **[!UICONTROL Write Data in Notebook]** in het vervolgkeuzemenu in de gegevensset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.

- Gebruik **[!UICONTROL Explore Data in Notebook]** om een leescel te genereren.
- Gebruik **[!UICONTROL Write Data in Notebook]** om een schrijfcel te genereren.

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

### Filter [!DNL ExperienceEvent] gegevens {#pyspark-filter-experienceevent}

Voor het verkrijgen en filteren van een [!DNL ExperienceEvent] -dataset in een PySpark-laptop moet u de identiteit van de gegevensset (`{DATASET_ID}` ), de IMS-identiteit van uw organisatie en de filterregels die een specifieke tijdreeks definiëren. Een het filtreren tijdwaaier wordt bepaald door de functie `spark.sql()` te gebruiken, waar de functieparameter een SQL vraagkoord is.

De volgende cellen filteren een [!DNL ExperienceEvent] dataset op gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

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

In Scala kunt u `clientContext` importeren om Experience Platform-waarden op te halen en te retourneren. Hierdoor hoeft u geen variabelen zoals `var userToken` te definiëren. In het onderstaande Scala-voorbeeld wordt `clientContext` gebruikt om alle vereiste waarden voor het lezen van een gegevensset op te halen en te retourneren.

>[!IMPORTANT]
>
> Gegevens in cache plaatsen met `df.cache()` voordat gegevens worden geschreven, kan de prestaties van een laptop aanzienlijk verbeteren. Dit kan helpen als u een van de volgende fouten ontvangt:
> 
> - Taak afgebroken vanwege een fout in het werkgebied... Kan alleen RDD&#39;s met hetzelfde aantal elementen in elke partitie comprimeren.
> - Externe RPC-client uitgeschakeld en andere geheugenfouten.
> - Slechte prestaties bij het lezen en schrijven van datasets.
> 
> Zie de [ het oplossen van problemengids ](../troubleshooting-guide.md) voor meer informatie.

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Element | Beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `clientContext.getUserToken()`. |
| service-token | Uw service-token dat automatisch wordt opgehaald met `clientContext.getServiceToken()` . |
| ims-org | Uw organisatie-id die automatisch wordt opgehaald met `clientContext.getOrgId()` . |
| api-toets | De API-sleutel die automatisch wordt opgehaald met `clientContext.getApiKey()` . |

>[!TIP]
>
>Herzie de lijsten Scala binnen de [ sectie van de notitieboekjegegevens ](#notebook-data-limits) om te bepalen als `mode` aan `interactive` of `batch` zou moeten worden geplaatst.

U kunt het bovenstaande voorbeeld automatisch genereren bij het aanschaffen van JupyterLab met de volgende methode:

Selecteer het tabblad Gegevenspictogram (hieronder gemarkeerd) in de linkernavigatie van JupyterLab. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie **[!UICONTROL Explore Data in Notebook]** in het vervolgkeuzemenu in de gegevensset die u wilt gebruiken. Onder aan uw laptop wordt een uitvoerbaar code-item weergegeven.
en
- Gebruik **[!UICONTROL Explore Data in Notebook]** om een leescel te genereren.
- Gebruik **[!UICONTROL Write Data in Notebook]** om een schrijfcel te genereren.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Schrijven naar een gegevensset {#scala-write-dataset}

In Scala kunt u `clientContext` importeren om Experience Platform-waarden op te halen en te retourneren. Hierdoor hoeft u geen variabelen zoals `var userToken` te definiëren. In het onderstaande Scala-voorbeeld wordt `clientContext` gebruikt om alle vereiste waarden die nodig zijn voor het schrijven naar een gegevensset te definiëren en te retourneren.

>[!IMPORTANT]
>
> Gegevens in cache plaatsen met `df.cache()` voordat gegevens worden geschreven, kan de prestaties van een laptop aanzienlijk verbeteren. Dit kan helpen als u een van de volgende fouten ontvangt:
> 
> - Taak afgebroken vanwege een fout in het werkgebied... Kan alleen RDD&#39;s met hetzelfde aantal elementen in elke partitie comprimeren.
> - Externe RPC-client uitgeschakeld en andere geheugenfouten.
> - Slechte prestaties bij het lezen en schrijven van datasets.
> 
> Zie de [ het oplossen van problemengids ](../troubleshooting-guide.md) voor meer informatie.

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `clientContext.getUserToken()`. |
| service-token | Uw service-token dat automatisch wordt opgehaald met `clientContext.getServiceToken()` . |
| ims-org | Uw organisatie-id die automatisch wordt opgehaald met `clientContext.getOrgId()` . |
| api-toets | De API-sleutel die automatisch wordt opgehaald met `clientContext.getApiKey()` . |

>[!TIP]
>
>Herzie de lijsten Scala binnen de [ sectie van de notitieboekjegegevens ](#notebook-data-limits) om te bepalen als `mode` aan `interactive` of `batch` zou moeten worden geplaatst.

### een lokaal dataframe maken {#scala-create-dataframe}

SQL-query&#39;s zijn vereist voor het maken van een lokaal dataframe met Scala. Bijvoorbeeld:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filter [!DNL ExperienceEvent] gegevens {#scala-experienceevent}

Als u een [!DNL ExperienceEvent] dataset in een Scala-laptop benadert en filtert, moet u de identiteit van de gegevensset (`{DATASET_ID}`), de IMS-identiteit van uw organisatie en de filterregels die een specifieke tijdreeks definiëren. Een Filtrerende tijdwaaier wordt bepaald door de functie `spark.sql()` te gebruiken, waar de functieparameter een SQL vraagkoord is.

De volgende cellen filteren een [!DNL ExperienceEvent] dataset op gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestaan.

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

In dit document worden de algemene richtlijnen besproken voor toegang tot gegevenssets met JupyterLab-laptops. Voor meer diepgaande voorbeelden bij het vragen van datasets, bezoek de [ Dienst van de Vraag in JupyterLab notitieboekjes ](./query-service.md) documentatie. Voor meer informatie over om uw datasets te onderzoeken en visualiseren, bezoek het document op [ het analyseren van uw gegevens gebruikend laptops ](./analyze-your-data.md).

## Optionele SQL-markeringen voor [!DNL Query Service] {#optional-sql-flags-for-query-service}

In deze tabel staan de optionele SQL-markeringen die kunnen worden gebruikt voor [!DNL Query Service] .

| **Vlag** | **Beschrijving** |
| --- | --- |
| `-h`, `--help` | Help-bericht weergeven en afsluiten. |
| `-n`, `--notify` | Optie in-/uitschakelen voor het melden van queryresultaten. |
| `-a`, `--async` | Als u deze markering gebruikt, wordt de query asynchroon uitgevoerd en kan de kernel vrijkomen terwijl de query wordt uitgevoerd. Wees voorzichtig wanneer u queryresultaten toewijst aan variabelen, omdat deze mogelijk niet gedefinieerd zijn als de query niet volledig is. |
| `-d`, `--display` | Met deze markering voorkomt u dat resultaten worden weergegeven. |
