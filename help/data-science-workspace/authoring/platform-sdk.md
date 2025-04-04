---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;populaire onderwerpen
solution: Experience Platform
title: Modellen ontwerpen met de Adobe Experience Platform SDK
description: Deze zelfstudie biedt u informatie over het omzetten van data_access_sdk_python in het nieuwe Python platform_sdk in zowel Python als R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Modellen ontwerpen met de Adobe [!DNL Experience Platform] SDK

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie biedt u informatie over het omzetten van `data_access_sdk_python` in de nieuwe Python `platform_sdk` in zowel Python als R. Deze zelfstudie biedt informatie over de volgende bewerkingen:

- [Verificatie opbouwen](#build-authentication)
- [Basislezen van gegevens](#basic-reading-of-data)
- [Basisschrijven van gegevens](#basic-writing-of-data)

## Verificatie opbouwen {#build-authentication}

Verificatie is vereist om aanroepen uit te voeren naar [!DNL Adobe Experience Platform] en bestaat uit API-sleutel, organisatie-id, een gebruikerstoken en een servicetoken.

### Python

Als u Jupyter-laptop gebruikt, gebruikt u de onderstaande code om de `client_context` samen te stellen:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Als u geen Jupyter-laptop gebruikt of als u de organisatie moet wijzigen, gebruikt u het onderstaande codevoorbeeld:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Als u Jupyter-laptop gebruikt, gebruikt u de onderstaande code om de `client_context` samen te stellen:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Als u geen Jupyter-laptop gebruikt of als u een andere organisatie wilt gebruiken, gebruikt u het onderstaande codevoorbeeld:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Basislezen van gegevens {#basic-reading-of-data}

Met de nieuwe [!DNL Experience Platform] SDK is de maximale leesgrootte 32 GB, met een maximale leestijd van 10 minuten.

Als de leestijd te lang duurt, kunt u een van de volgende filteropties gebruiken:

- [Gegevens filteren op offset en limiet](#filter-by-offset-and-limit)
- [Gegevens filteren op datum](#filter-by-date)
- [Gegevens filteren op kolom](#filter-by-selected-columns)
- [Gesorteerde resultaten ophalen](#get-sorted-results)

>[!NOTE]
>
>De organisatie wordt ingesteld binnen de `client_context` .

### Python

Voor het lezen van gegevens in Python gebruikt u het onderstaande codevoorbeeld:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Gebruik het onderstaande codevoorbeeld om gegevens in R te lezen:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filteren op verschuiving en limiet {#filter-by-offset-and-limit}

Omdat filteren op batch-id niet meer wordt ondersteund, moet u `offset` en `limit` gebruiken om het lezen van gegevens in bereik te houden.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filteren op datum {#filter-by-date}

De korreligheid van datum het filtreren wordt nu bepaald door timestamp, eerder dan wordt geplaatst tegen de dag.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

De nieuwe [!DNL Experience Platform] SDK ondersteunt de volgende bewerkingen:

| Bewerking | Functie |
| --------- | -------- |
| Gelijk (`=`) | `eq()` |
| Groter dan (`>`) | `gt()` |
| Groter dan of gelijk aan (`>=`) | `ge()` |
| Kleiner dan (`<`) | `lt()` |
| Kleiner dan of gelijk aan (`<=`) | `le()` |
| En (`&`) | `And()` |
| Of (`|`) | `Or()` |

## Filteren op geselecteerde kolommen {#filter-by-selected-columns}

Als u het lezen van gegevens verder wilt verfijnen, kunt u ook filteren op kolomnaam.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Gesorteerde resultaten ophalen {#get-sorted-results}

De ontvangen resultaten kunnen door gespecificeerde kolommen van de doeldataset en in hun orde (asc/desc) respectievelijk worden gesorteerd.

In het volgende voorbeeld wordt dataframe eerst in oplopende volgorde gesorteerd op &quot;column-a&quot;. Rijen met dezelfde waarden voor &quot;column-a&quot; worden vervolgens in aflopende volgorde gesorteerd op &quot;column-b&quot;.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Basisschrijven van gegevens {#basic-writing-of-data}

>[!NOTE]
>
>De organisatie wordt ingesteld binnen de `client_context` .

Gebruik een van de volgende voorbeelden om gegevens in Python en R te schrijven:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Volgende stappen

Nadat u de gegevenslader van `platform_sdk` hebt geconfigureerd, worden de gegevens voorbereid en vervolgens gesplitst naar de gegevenssets `train` en `val` . Om over gegevensvoorbereiding en eigenschaptechniek te leren gelieve de sectie over [ te bezoeken gegevens voorbereiding en eigenschapengineering ](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) in het leerprogramma voor het creëren van een recept gebruikend [!DNL JupyterLab] laptops.
