---
keywords: Experience Platform;Score a model;Data Science Workspace;populaire onderwerpen;sensei machine learning api
solution: Experience Platform
title: Score een model met de Sensei Machine Learning-API
type: Tutorial
description: Deze zelfstudie laat u zien hoe u de API's voor leren van Sensei Machine Learning kunt gebruiken om een expert en een experimentele run te maken.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Score een model gebruikend [!DNL Sensei Machine Learning API]

Deze zelfstudie laat u zien hoe u de API&#39;s kunt gebruiken om een experimenteerprogramma en een experimentele versie te maken. Voor een lijst van alle eindpunten in de het Leren API van de Machine van Sensei, gelieve te verwijzen naar [ dit document ](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Een geplande expert voor scoring maken

Net als voor geplande trainingsexperimenten wordt het maken van een gepland experiment voor scoring ook uitgevoerd door een `template` -sectie op te nemen in de parameter body. Daarnaast wordt het veld `name` onder `tasks` in de hoofdtekst ingesteld op `score` .

Hieronder ziet u een voorbeeld van het maken van een experiment dat elke 20 minuten start vanaf `startTime` en wordt uitgevoerd tot `endTime` .

**Verzoek**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{JSON_PAYLOAD}`: Experimenteel Run-object dat moet worden verzonden. Het voorbeeld dat wij in onze zelfstudie gebruiken, wordt hier getoond:

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

**Reactie**

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

Met het getrainde model kunnen we nu een Experimentele run voor scoring maken. De waarde van de parameter `modelId` is de `id` -parameter die in de bovenstaande aanvraag voor het model GET is geretourneerd.

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

`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat u als doel wilt instellen. Dit vindt u in het antwoord bij het maken van uw experiment.\
`{JSON_PAYLOAD}`: Gegevens die moeten worden gepost. Het voorbeeld dat we in onze zelfstudie gebruiken is:

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

**Reactie**

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

`{EXPERIMENT_ID}`: De id die correspondeert met het experiment dat de Run uitvoert.\
`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de proefversie die u zojuist hebt gemaakt.


### De status Experiment uitvoeren ophalen voor de geplande uitvoering van een experiment

Om de Runs van de Experiment voor geplande Experimenten te krijgen, wordt de vraag hieronder getoond:

**Verzoek**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: De id die correspondeert met het experiment dat de Run uitvoert.\
`{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.\
`{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.

Aangezien er meerdere experimentele runtime&#39;s zijn voor een specifiek experiment, heeft het gegeven antwoord een array van run-id&#39;s.

**Reactie**

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

`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de proefversie.\
`{EXPERIMENT_ID}`: De id die correspondeert met het experiment dat de Run uitvoert.

### Een geplande expert stoppen en verwijderen

Als u de uitvoering van een gepland experiment vóór de `endTime` ervan wilt stoppen, kunt u dit doen door een verzoek van de DELETE naar de `{EXPERIMENT_ID}` te vragen

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
