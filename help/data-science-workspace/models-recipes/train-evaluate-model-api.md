---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Een model (API) trainen en evalueren
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Een model (API) trainen en evalueren


In deze zelfstudie wordt uitgelegd hoe u een model kunt maken, trainen en evalueren met behulp van API-aanroepen. Raadpleeg [dit document](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) voor een gedetailleerde lijst met API-documentatie.

## Vereisten

Volg de [import van een gecomprimeerde ontvanger met behulp van de API](./import-packaged-recipe-api.md) voor het maken van een engine. Deze is vereist voor het trainen en evalueren van een model met behulp van de API.

Volg deze [zelfstudie](../../tutorials/authentication.md) voor toestemming om API-aanroepen te starten.

In de zelfstudie hebt u nu de volgende waarden:

- `{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.
- `{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.

- Koppeling naar een Docker-afbeelding van een intelligente service

## API-workflow

We gebruiken de API&#39;s om een Experiment Run voor training te maken. Voor deze zelfstudie zullen we ons richten op de eindpunten **Engines**, **MLInstances** en **Experimenten** . De volgende grafiek schetst de verhouding tussen drie en introduceert ook het idee van een Looppas en een Model.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE] De termen &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; en &quot;Model&quot; worden in de gebruikersinterface aangeduid als verschillende termen. Als u uit UI komt, zal de volgende lijst de verschillen in kaart brengen.
> 
> | UI-term | API-term |
> --- | ---
> | Recipe | Engine |
> | Model | MLInstance |
> | Trainingsduur | Experimenteer |
> | Service | MLService |



### Een MLInstance maken

Het creëren van een MLInstance kan worden gedaan gebruikend het volgende verzoek. U gebruikt de inhoud `{ENGINE_ID}` die is geretourneerd bij het maken van een engine van de [importmodule voor een pakketrecept met de API](./import-packaged-recipe-ui.md) -zelfstudie.

**Verzoek**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.\
`{JSON_PAYLOAD}`: De configuratie van onze MLInstance. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE] In de `{JSON_PAYLOAD}`code definiëren we parameters die worden gebruikt voor training en scoring in de `tasks` array. Dit `{ENGINE_ID}` is de id van de engine die u wilt gebruiken en het `tag` veld is een optionele parameter die wordt gebruikt om de instantie te identificeren.

Het antwoord zal bevatten `{INSTANCE_ID}` die MLInstance vertegenwoordigt die wordt gecreeerd. Er kunnen meerdere model-MLInstances met verschillende configuraties worden gemaakt.

**Antwoord**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Deze ID die de Motor vertegenwoordigt wordt MLInstance gecreeerd onder.\
`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.

### Een experiment maken

Een Experiment wordt door een gegevenswetenschapper gebruikt om tijdens de opleiding tot een goed presterend model te komen. De veelvoudige Experimenten omvatten veranderende datasets, eigenschappen, het leren parameters, en hardware. Hieronder ziet u een voorbeeld van het maken van een experiment.

**Verzoek**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Het gemaakte experimentele object. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.

De reactie van het project Experiment ziet er zo uit.

**Antwoord**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: De id die staat voor het experiment dat u zojuist hebt gemaakt.
`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.

### Een gepland experiment voor training maken

Gepland Experimenten worden gebruikt zodat wij niet te hoeven om elke enkele Runs van de Experiment via een API vraag tot stand te brengen. In plaats daarvan, verstrekken wij alle noodzakelijke parameters tijdens de verwezenlijking van de Experiment en elke looppas zal periodiek worden gecreeerd.

Om aan te geven dat er een geprogrammeerd experiment moet worden opgezet, moeten we een `template` gedeelte van het verzoek toevoegen. In `template`, zijn alle noodzakelijke parameters voor het plannen van looppas inbegrepen zoals `tasks`, die wijzen op welke actie, en `schedule`, die op de timing van de geplande looppas wijst.

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Te posten gegevensset. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Wanneer wij een Experiment creëren, zou het lichaam, `{JSON_PAYLOAD}`, of de `mlInstanceId` of `mlInstanceQuery` parameter moeten bevatten. In dit voorbeeld wordt elke 20 minuten door een geplande Experiment een uitvoering aangeroepen, die in de `cron` parameter wordt ingesteld, te beginnen vanaf de `startTime` tot aan de `endTime`.

**Antwoord**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: De id die het experiment vertegenwoordigt.\
`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.


### Een experimentele training maken

Als er een entiteit Experiment is gemaakt, kan een trainingrun worden gemaakt en uitgevoerd met de onderstaande oproep. U zult het nodig hebben `{EXPERIMENT_ID}` en specificeren wat `mode` u in het verzoeklichaam wilt teweegbrengen.

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat u als doel wilt instellen. Dit vindt u in het antwoord bij het maken van uw experiment.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Als u een trainingsrun wilt maken, moet u het volgende opnemen in het hoofdgedeelte:

```JSON
{
    "mode":"Train"
}
```

U kunt de configuratieparameters ook overschrijven door een `tasks` array op te nemen:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

U zult de volgende reactie krijgen die u de `{EXPERIMENT_RUN_ID}` en configuratie onder zal laten kennen `tasks`.

**Antwoord**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:  De id die staat voor de proefrun.\
`{EXPERIMENT_ID}`: De id die staat voor het experiment dat onder de Experimentenrun valt.

### De status Experimentair uitvoeren ophalen

De status van de uitvoering van het experiment kan worden opgevraagd bij de `{EXPERIMENT_RUN_ID}`.

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: De id die het experiment vertegenwoordigt.\
`{EXPERIMENT_RUN_ID}`: De id die staat voor de proefrun.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.

**Antwoord**

De GET vraag zal de status in de `state` parameter zoals hieronder getoond verstrekken:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`:  De id die staat voor de proefrun.\
`{EXPERIMENT_ID}`: De id die staat voor het experiment dat onder de Experimentenrun valt.

Naast de `DONE` staat zijn onder andere de volgende staten:
- `PENDING`
- `RUNNING`
- `FAILED`

Voor meer informatie kunt u gedetailleerde logboekbestanden vinden onder de `tasklogs` parameter.

### Het getrainde model ophalen

Om het opgeleide model te krijgen hierboven gecreeerd tijdens opleiding, doen wij het volgende verzoek:

**Verzoek**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de uitvoering van het experiment waarop u zich wilt richten. Dit vindt u in het antwoord bij het maken van uw experimentele versie.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.

De reactie vertegenwoordigt het opgeleide Model dat werd gecreeerd.

**Antwoord**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: De id die overeenkomt met het model.\
`{EXPERIMENT_ID}`:  De id die correspondeert met de Experiment Run is lager.\
`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de uitvoering van het experiment.

### Een geplande expert stoppen en verwijderen

Als u de uitvoering van een gepland experiment vóór de uitvoering wilt stoppen `endTime`, kunt u dit doen door een DELETE-verzoek naar de `{EXPERIMENT_ID}`

**Verzoek**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  De id die overeenkomt met het experiment.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.

>[!NOTE] Met de API-aanroep wordt het maken van nieuwe experimentele runtime uitgeschakeld. De uitvoering van reeds uitgevoerde experimentele runtime wordt echter niet gestopt.

Hier volgt de reactie waarbij wordt gemeld dat het experiment is verwijderd.

**Antwoord**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Volgende stappen

In deze zelfstudie wordt uitgelegd hoe u de API&#39;s kunt gebruiken voor het maken van een engine, een Experiment, geplande experimentele runtime en getrainde modellen. In de [volgende oefening](./score-model-api.md), zult u voorspellingen maken door een nieuwe dataset te scoren gebruikend het best presterende getrainde model.