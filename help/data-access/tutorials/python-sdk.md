---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Python Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 49aa2e2664fe658d89b6279d1f869eb30c48ccad
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---


# Secure Python [!DNL Data Access] SDK

De Secure Python [!DNL Data Access] SDK is een softwareontwikkelingskit waarmee gegevens van het Adobe Experience Platform kunnen worden gelezen en geschreven.

## Aan de slag

U moet het [authentificatieleerprogramma](../../tutorials/authentication.md) hebben voltooid om toegang tot de waarden te hebben om vraag aan Secure Python [!DNL Data Access] SDK te maken:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor het gebruik van de [!DNL Python] SDK zijn de naam en de id van de sandbox vereist waarin de bewerking plaatsvindt:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

## Omgevingsinstelling

Door gebrek, worden de de diensteindpunten geplaatst aan de eindpunten van het integratiemilieu. Als u dus naar de productie wilt wijzen, stelt u de volgende omgevingsvariabelen in op de volgende waarden:

| Variabele | Endpoint |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Bovendien kunnen uw referenties worden toegevoegd als omgevingsvariabelen.

| Variabele | Waarde |
| -------- | ----- |
| `ORG_ID` | Je `{IMS_ORG}` id. |
| `SERVICE_API_KEY` | Uw `{API_KEY}` waarde. |
| `USER_TOKEN` | Uw `{ACCESS_TOKEN}` waarde. |
| `SERVICE_TOKEN` | Uw `{SERVICE_TOKEN}`, die u kan backchannel verzoeken tussen de diensten moeten goedkeuren. |
| `SANDBOX_ID` | De `{SANDBOX_ID}` waarde van de sandbox. |
| `SANDBOX_NAME` | De `{SANDBOX_NAME}` waarde van de sandbox. |

## Installatie

Alle pakketten worden uitgevoerd aan `./dist` na de bouw.

### Wiel

```python
python3 setup.py bdist_wheel --universal
```

Laad het wiel vanuit de projectdirectory naar uw Python 3-omgeving.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Eibestand

```python
python3 setup.py bdist_egg
```

## Een gegevensset lezen

Nadat u de omgevingsvariabelen hebt ingesteld en de installatie hebt voltooid, kan de gegevensset nu worden gelezen in het dataframe van pandas.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### Kolommen SELECTEREN uit de gegevensset

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Informatie over partitionering ophalen:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT, component

Met de component DISTINCT kunt u alle afzonderlijke waarden op rij-/kolomniveau ophalen, waarbij alle dubbele waarden uit de reactie worden verwijderd.

Hieronder ziet u een voorbeeld van het gebruik van de `distinct()` functie:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE-component

De [!DNL Python] SDK ondersteunt bepaalde operatoren om de dataset te filteren.

>[!NOTE] De functies die worden gebruikt voor filteren zijn hoofdlettergevoelig.

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

Met de ORDER BY-component kunnen ontvangen resultaten worden gesorteerd met een opgegeven kolom in een bepaalde volgorde (oplopend of aflopend). In de Python SDK gebeurt dit met behulp van de `sort()` functie.

Hieronder ziet u een voorbeeld van het gebruik van de `sort()` functie:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-component

De clausule LIMIT staat gebruikers toe om het aantal verslagen te beperken die van de dataset worden ontvangen.

Hieronder ziet u een voorbeeld van het gebruik van de `limit()` functie:

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-clausule

Met de OFFSET-component kunnen gebruikers rijen vanaf het begin overslaan en vanaf een later punt beginnen met het retourneren van rijen. In combinatie met LIMIT, kan dit worden gebruikt om rijen in blokken te herhalen.

Hieronder ziet u een voorbeeld van het gebruik van de `offset()` functie:

```python
df = dataset_reader.offset(100).read()
```

## Een gegevensset schrijven

De [!DNL Python] SDK ondersteunt het schrijven van gegevenssets. Gebruikers moeten het dataframe van pandas opgeven dat naar de gegevensset moet worden geschreven.

### Het schrijven van het dataframe van de panda&#39;s

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Gebruikersruimtedirectory (controlepunt)

Voor langere taken die worden uitgevoerd, moeten gebruikers mogelijk tussenliggende stappen opslaan. In dergelijke gevallen biedt de [!DNL Python] SDK de gebruiker de mogelijkheid om te lezen van en te schrijven naar een gebruikersruimte.

>!![NOTE] Paden naar de gegevens worden **niet** opgeslagen door de SDK. Gebruikers moeten het bijbehorende pad naar hun respectievelijke gegevens opslaan.

### Schrijven naar gebruikersruimte

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lezen uit gebruikersruimte

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
