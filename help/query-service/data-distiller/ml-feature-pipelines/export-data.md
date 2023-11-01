---
title: Gegevens exporteren naar externe XML-omgevingen
description: Leer hoe u een voorbereide trainingsdataset, gemaakt met Data Distiller, deelt naar een locatie voor cloudopslag die uw XML-omgeving kan lezen voor training en het scoren van uw model.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# Gegevens exporteren naar externe XML-omgevingen

In dit document wordt uitgelegd hoe u een voorbereide trainingsgegevensset die is gemaakt met Data Distiller, kunt delen met een locatie voor cloudopslag die uw XML-omgeving kan lezen voor training en het scoren van uw model. Het voorbeeld hier exporteert de trainingsdataset naar de [Data Landing Zone (DLZ)](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html). U kunt de opslagbestemming naar wens wijzigen om te werken met de leeromgeving van uw computer.

De [Flow Service voor doelen](https://developer.adobe.com/experience-platform-apis/references/destinations/) wordt gebruikt om de eigenschappijpleiding te voltooien door een dataset van gegevens verwerkte eigenschappen in een aangewezen plaats van de wolkenopslag te landen.

## De bronverbinding maken {#create-source-connection}

De bronverbinding is verantwoordelijk voor het vormen van de verbinding aan uw dataset van Adobe Experience Platform zodat de resulterende stroom precies weet waar te om de gegevens en in welk formaat te zoeken.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Doelverbinding maken {#create-target-connection}

De doelverbinding is verantwoordelijk voor de verbinding met het doelbestandssysteem. Hiervoor moet eerst een basisverbinding met een account voor cloudopslag worden gemaakt (de gegevenslandingszone in dit voorbeeld) en vervolgens een doelverbinding met een specifiek bestandspad met opgegeven compressie- en opmaakopties.

De beschikbare bestemmingen van de wolkenopslag worden elk geïdentificeerd door een identiteitskaart van de verbindingsspecificatie:

| Type cloudopslag | Verbinding - Specificatie-id |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Azure Blob Storage | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Gegevenslandingszone | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google Cloud Storage | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## De gegevensstroom maken {#create-data-flow}

De laatste stap bestaat uit het maken van een gegevensstroom tussen de gegevensset die is opgegeven in de bronverbinding en het pad naar het doelbestand dat is opgegeven in de doelverbinding.

Elk beschikbaar type van de wolkenopslag wordt geïdentificeerd door stroom specificeer identiteitskaart:

| Type cloudopslag | Stroom, specificatie-id |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Azure Blob Storage | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Gegevenslandingszone | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google Cloud Storage | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

De volgende code leidt tot een gegevensstroom met een programma dat wordt geplaatst om ver in de toekomst te beginnen. Hierdoor kunt u ad-hocstromen activeren tijdens de modelontwikkeling. Zodra u een opgeleid model hebt, kunt u het programma van de gegevensstroom bijwerken om de eigenschapdataset op het gewenste programma te delen.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Met de gemaakte gegevensstroom, kunt u een ad hoc stroom nu teweegbrengen om de eigenschapdataset op bestelling te delen:

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Gestroomlijnd delen naar Data Landing Zone

Als u een gegevensset gemakkelijker wilt delen met de gegevenslandingszone, `aepp` bibliotheek biedt een `exportDatasetToDataLandingZone` functie die de bovenstaande stappen uitvoert in één functieaanroep:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Deze code maakt de bronverbinding, de doelverbinding en de gegevensstroom op basis van de opgegeven parameters en voert in één stap een ad-hocuitvoering van de gegevensstroom uit.
