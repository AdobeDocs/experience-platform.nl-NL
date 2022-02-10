---
keywords: Experience Platform;Score a model;Data Science Workspace;populaire onderwerpen;sensei machine learning api
solution: Experience Platform
title: Score een model met de Sensei Machine Learning-API
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie laat u zien hoe u de API's voor leren van Sensei Machine Learning kunt gebruiken om een expert en een experimentele run te maken.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 6ae6bbb5af0f007e483145dca5d4d505c388cc2c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Score een model gebruikend [!DNL Sensei Machine Learning API]

Deze zelfstudie laat u zien hoe u de API&#39;s kunt gebruiken om een experimenteerprogramma en een experimentele versie te maken. Raadpleeg voor een lijst met alle eindpunten in de API voor leren van Sensei Machine de koppeling naar [dit document](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Een geplande expert voor scoring maken

Net als voor geplande trainingsexperimenten wordt ook een gepland experiment voor scoring ontwikkeld door een `template` aan de parameter body. Daarnaast worden de `name` veld onder `tasks` in de hoofdtekst wordt ingesteld als `score`.

Hieronder ziet u een voorbeeld van het maken van een experiment dat elke 20 minuten wordt uitgevoerd, te beginnen bij `startTime` en loopt tot `endTime`.

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{JSON_PAYLOAD}`: Experiment Run-object dat moet worden verzonden. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.\
`{MODEL_ID}`: De id die het getrainde model vertegenwoordigt.

Hier volgt de reactie na het maken van het geplande experiment.

**Antwoord**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: De id die het experiment vertegenwoordigt.\
`{INSTANCE_ID}`: De id die de MLInstance vertegenwoordigt.


### Een experimentele score maken

Met het getrainde model kunnen we nu een Experimentele run voor scoring maken. De waarde van de `modelId` parameter is `id` parameter die hierboven in de GET Model-aanvraag is geretourneerd.

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

`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{API_KEY}`: Uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat u als doel wilt instellen. Dit vindt u in het antwoord bij het maken van uw experiment.\
`{JSON_PAYLOAD}`: Te verzenden gegevens. Het voorbeeld dat we in onze zelfstudie gebruiken is:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: De id die overeenkomt met het model.

De reactie van het project Experiment Run wordt hieronder weergegeven:

**Antwoord**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: De id die correspondeert met de Experiment die de Run heeft ondergaan.\
`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de proefversie die u zojuist hebt gemaakt.


### De status Experiment uitvoeren ophalen voor de geplande uitvoering van een experiment

Om de Runs van de Experiment voor geplande Experimenten te krijgen, wordt de vraag hieronder getoond:

**Verzoek**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: De id die correspondeert met de Experiment die de Run heeft ondergaan.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.

Aangezien er meerdere experimentele runtime&#39;s zijn voor een specifiek experiment, heeft het gegeven antwoord een array van run-id&#39;s.

**Antwoord**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de uitvoering van het experiment.\
`{EXPERIMENT_ID}`: De id die correspondeert met de Experiment die de Run heeft ondergaan.

### Een geplande expert stoppen en verwijderen

Als u de uitvoering van een gepland experiment wilt stoppen vóór de uitvoering ervan `endTime`, kan dit worden gedaan door een verzoek van DELETE aan `{EXPERIMENT_ID}`

**Verzoek**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment.\
`{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.\
`{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.

>[!NOTE]
>
>Met de API-aanroep wordt het maken van nieuwe experimentele runtime uitgeschakeld. De uitvoering van reeds uitgevoerde experimentele runtime wordt echter niet gestopt.

Hier volgt de reactie waarbij wordt gemeld dat het experiment is verwijderd.

**Antwoord**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
