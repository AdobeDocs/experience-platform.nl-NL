---
keywords: Experience Platform;trainen en evalueren;Data Science Workspace;populaire onderwerpen;Sensei Machine Learning API
solution: Experience Platform
title: Een model trainen en evalueren met de API voor leren van Sensei Machine
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u een model kunt maken, trainen en evalueren met behulp van API-aanroepen voor leren van Sensei-machines.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Een model trainen en evalueren met de API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

In deze zelfstudie wordt uitgelegd hoe u een model kunt maken, trainen en evalueren met behulp van API-aanroepen. Verwijs naar [ dit document ](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) voor een gedetailleerde lijst van API documentatie.

## Vereisten

Volg de [ Invoer een verpakte Ontvanger gebruikend API ](./import-packaged-recipe-api.md) voor het creëren van een Motor, die wordt vereist om een Model te trainen en te evalueren gebruikend API.

Volg het [ Experience Platform API authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) beginnen API vraag te maken.

In de zelfstudie hebt u nu de volgende waarden:

- `{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.
- `{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.
- `{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.

- Koppeling naar een Docker-afbeelding van een intelligente service

## API-workflow

We gebruiken de API&#39;s om een Experiment Run voor training te maken. Voor deze zelfstudie zullen we ons richten op de eindpunten Engines, MLInstances en Experiments. De volgende grafiek schetst de verhouding tussen drie en introduceert ook het idee van een Looppas en een Model.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>De termen &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; en &quot;Model&quot; worden in de gebruikersinterface aangeduid als verschillende termen. Als u uit UI komt, brengt de volgende lijst de verschillen in kaart.

| UI-term | API-term |
| --- | --- |
| Recipe | Engine |
| Model | MLInstance |
| Trainingsduur | Experimenteer |
| Service | MLService |

### Een MLInstance maken

Het creëren van een MLInstance kan worden gedaan gebruikend het volgende verzoek. U zult `{ENGINE_ID}` gebruiken die toen het creëren van een Motor van [ was teruggekeerd invoert een verpakte Ontvanger gebruikend de API ](./import-packaged-recipe-ui.md) leerprogramma.

**Verzoek**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
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

>[!NOTE]
>
>In `{JSON_PAYLOAD}` definiëren we parameters die worden gebruikt voor training en scoring in de array `tasks` . `{ENGINE_ID}` is de id van de engine die u wilt gebruiken en het veld `tag` is een optionele parameter die wordt gebruikt om de instantie te identificeren.

De reactie bevat `{INSTANCE_ID}` die de gemaakte MLInstance vertegenwoordigt. Er kunnen meerdere model-MLInstances met verschillende configuraties worden gemaakt.

**Reactie**

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

`{ENGINE_ID}`: Deze id die de engine vertegenwoordigt waarop de MLInstance wordt gemaakt.\
`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.

### Een experiment maken

Een Experiment wordt door een gegevenswetenschapper gebruikt om tijdens de opleiding tot een goed presterend model te komen. De veelvoudige Experimenten omvatten veranderende datasets, eigenschappen, het leren parameters, en hardware. Hieronder ziet u een voorbeeld van het maken van een experiment.

**Verzoek**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{JSON_PAYLOAD}` : een experimenteel object dat is gemaakt. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

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

**Reactie**

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

Als u wilt aangeven dat er een gepland experiment moet worden gemaakt, moet u een `template` -sectie toevoegen aan de hoofdtekst van het verzoek. In `template` zijn alle noodzakelijke parameters voor het plannen van runtime opgenomen, zoals `tasks` , die aangeeft welke actie wordt uitgevoerd, en `schedule` , die de timing van de geplande uitvoering aangeeft.

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{JSON_PAYLOAD}`: gegevensset die moet worden gepost. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

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

Wanneer we een experiment maken, moet de hoofdtekst, `{JSON_PAYLOAD}` , de parameter `mlInstanceId` of `mlInstanceQuery` bevatten. In dit voorbeeld wordt elke 20 minuten, ingesteld in de parameter `cron`, door een geplande Experiment een uitvoering aangeroepen die begint op `startTime` tot en met `endTime` .

**Reactie**

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

Als er een entiteit Experiment is gemaakt, kan een trainingrun worden gemaakt en uitgevoerd met de onderstaande oproep. U hebt de instructie `{EXPERIMENT_ID}` nodig en geeft aan wat `mode` u wilt activeren in de hoofdtekst van de aanvraag.

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat u als doel wilt instellen. Dit vindt u in het antwoord bij het maken van uw experiment.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{JSON_PAYLOAD}`: als u een trainingsrun wilt maken, moet u het volgende opnemen in de hoofdtekst:

```JSON
{
    "mode":"Train"
}
```

U kunt de configuratieparameters ook overschrijven door een array `tasks` op te nemen:

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

U krijgt de volgende reactie die u de `{EXPERIMENT_RUN_ID}` en de configuratie onder `tasks` laat weten.

**Reactie**

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

`{EXPERIMENT_RUN_ID}`: De id die de experimentele uitvoering vertegenwoordigt.\
`{EXPERIMENT_ID}`: De id die staat voor het experiment dat onder de Experimentatieronde valt.

### De status Experimentair uitvoeren ophalen

De status van de uitvoering van het experiment kan worden opgevraagd bij de `{EXPERIMENT_RUN_ID}` .

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: De id die het experiment vertegenwoordigt.\
`{EXPERIMENT_RUN_ID}`: De id die de experimentele uitvoering vertegenwoordigt.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.

**Reactie**

De GET-aanroep geeft de status in de parameter `state` zoals hieronder wordt weergegeven:

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

`{EXPERIMENT_RUN_ID}`: De id die de experimentele uitvoering vertegenwoordigt.\
`{EXPERIMENT_ID}`: De id die staat voor het experiment dat onder de Experimentatieronde valt.

Naast de status `DONE` zijn er andere statussen:

- `PENDING`
- `RUNNING`
- `FAILED`

Voor meer informatie kunt u gedetailleerde logboekbestanden vinden onder de parameter `tasklogs` .

### Het getrainde model ophalen

Om het opgeleide model te krijgen hierboven gecreeerd tijdens opleiding, doen wij het volgende verzoek:

**Verzoek**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de uitvoering van het experiment waarop u zich wilt richten. Dit vindt u in het antwoord bij het maken van uw experimentele versie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.

De reactie vertegenwoordigt het opgeleide Model dat werd gecreeerd.

**Reactie**

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
`{EXPERIMENT_ID}`: De id die correspondeert met de Experiment Run is lager.\
`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de proefversie.

### Een geplande expert stoppen en verwijderen

Als u de uitvoering van een gepland experiment vóór de `endTime` ervan wilt stoppen, kunt u dit doen door een DELETE-aanvraag naar de `{EXPERIMENT_ID}` te vragen

**Verzoek**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.

>[!NOTE]
>
>Met de API-aanroep wordt het maken van nieuwe experimentele runtime uitgeschakeld. De uitvoering van reeds uitgevoerde experimentele runtime wordt echter niet gestopt.

Hier volgt de reactie waarbij wordt gemeld dat het experiment is verwijderd.

**Reactie**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Volgende stappen

In deze zelfstudie wordt uitgelegd hoe u de API&#39;s kunt gebruiken voor het maken van een engine, een Experiment, geplande experimentele runtime en getrainde modellen. In de [ volgende oefening ](./score-model-api.md), zult u voorspellingen maken door een nieuwe dataset te scoren gebruikend het hoogste uitvoerend getrainde model.
