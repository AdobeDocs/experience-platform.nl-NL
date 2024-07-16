---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevenstoegang;python sdk;gegevenstoegang api;read python;write python
solution: Experience Platform
title: Toegang verkrijgen tot gegevens met Python in Data Science Workspace
type: Tutorial
description: Het volgende document bevat voorbeelden over hoe u toegang kunt krijgen tot gegevens in Python voor gebruik in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Toegang verkrijgen tot gegevens met Python in Data Science Workspace

Het volgende document bevat voorbeelden over hoe u toegang kunt krijgen tot gegevens met Python voor gebruik in Data Science Workspace. Voor informatie bij de toegang tot van gegevens die laptops gebruiken JupyterLab, bezoek de [ JupyterLab toegang van notitieboekjes tot ](../jupyterlab/access-notebook-data.md) documentatie.

## Een gegevensset lezen

Nadat u de omgevingsvariabelen hebt ingesteld en de installatie hebt voltooid, kunt u uw gegevensset nu lezen in het dataframe van pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### Kolommen SELECTEREN uit de gegevensset

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Informatie over partitionering ophalen:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT, component

Met de component DISTINCT kunt u alle afzonderlijke waarden op rij-/kolomniveau ophalen, waarbij alle dubbele waarden uit de reactie worden verwijderd.

Hieronder ziet u een voorbeeld van het gebruik van de functie `distinct()` :

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE-component

U kunt bepaalde operatoren in Python gebruiken om uw gegevensset te filteren.

>[!NOTE]
>
>De functies die worden gebruikt voor filteren zijn hoofdlettergevoelig.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Hieronder ziet u een voorbeeld van het gebruik van deze filterfuncties:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-component

Met de ORDER BY-component kunnen ontvangen resultaten worden gesorteerd met een opgegeven kolom in een bepaalde volgorde (oplopend of aflopend). Dit wordt gedaan door de functie `sort()` te gebruiken.

Hieronder ziet u een voorbeeld van het gebruik van de functie `sort()` :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-component

De clausule LIMIT staat u toe om het aantal verslagen te beperken die van de dataset worden ontvangen.

Hieronder ziet u een voorbeeld van het gebruik van de functie `limit()` :

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-clausule

Met de component OFFSET kunt u rijen vanaf het begin overslaan en vanaf een later punt beginnen met het retourneren van rijen. In combinatie met LIMIT, kan dit worden gebruikt om rijen in blokken te herhalen.

Hieronder ziet u een voorbeeld van het gebruik van de functie `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Een gegevensset schrijven

Om aan een dataset te schrijven, moet u het pandas dataframe aan uw dataset leveren.

### Schrijven van het dataframe van de panda&#39;s

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Gebruikersruimtedirectory (controlepunt)

Voor langere actieve taken moet u mogelijk tussenliggende stappen opslaan. In dergelijke gevallen kunt u lezen en schrijven naar een gebruikersruimte.

>[!NOTE]
>
>De wegen aan de gegevens worden **niet** opgeslagen. U moet het overeenkomstige pad naar de desbetreffende gegevens opslaan.

### Schrijven naar gebruikersruimte

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lezen uit gebruikersruimte

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Volgende stappen

Adobe Experience Platform Data Science Workspace levert een recept-voorbeeld waarin de bovenstaande codevoorbeelden worden gebruikt voor het lezen en schrijven van gegevens. Als u meer over wilt leren hoe te om Python voor de toegang tot van uw gegevens te gebruiken, te herzien gelieve de [ Gegevens Wetenschap Workspace Python GitHub Bewaarplaats ](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
