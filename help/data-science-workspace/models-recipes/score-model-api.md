---
keywords: Experience Platform;Score een model;Data Science Workspace;populaire onderwerpen;sensei machine learning API
solution: Experience Platform
title: Score een model met de Sensei Machine Learning API
type: Tutorial
description: In deze zelfstudie leert u hoe u de Sensei Machine Learning-API's kunt gebruiken om een expert en een experimentele run te maken.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Score een model gebruikend [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten voor Data Science Workspace.

Deze zelfstudie laat zien hoe u de API&#39;s kunt gebruiken om een experiment en een experimentele uitvoering te maken. Voor een lijst van alle eindpunten in de het Leren API van de Machine van Sensei, gelieve te verwijzen naar [ dit document ](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Een geplande expert voor scores maken

Net als bij geplande experimenten voor training, wordt het maken van een gepland experiment voor scores ook gedaan door een `template` -sectie op te nemen in de parameter body. Daarnaast wordt het veld `name` onder `tasks` in de hoofdtekst ingesteld op `score` .

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

`{ORG_ID}`: uw organisatiegegevens zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: uw specifieke togertokenwaarde die u na verificatie opgeeft.\
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
`{INSTANCE_ID}`: De id die de instantie MLInstance vertegenwoordigt.


### Een experimentele score maken voor scores

Met het getrainde model kunnen we nu een Experiment Run voor scores maken. De waarde van de parameter `modelId` is de `id` -parameter die in de bovenstaande modelaanvraag is geretourneerd.

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

`{ORG_ID}`: uw organisatiegegevens zijn gevonden in uw unieke Adobe Experience Platform-integratie.\
`{ACCESS_TOKEN}`: uw specifieke togertokenwaarde die u na verificatie opgeeft.\
`{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.\
`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat u als doel wilt instellen. Dit vindt u in het antwoord bij het maken van uw experiment.\
`{JSON_PAYLOAD}`: gegevens die moeten worden gepost. Het voorbeeld dat we in onze zelfstudie gebruiken is:

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

`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat de run uitvoert.\
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
`{ORG_ID}`: uw organisatiegegevens zijn gevonden in uw unieke Adobe Experience Platform-integratie.

Aangezien er meerdere experimentele runtime&#39;s zijn voor een specifieke experiment, heeft de geretourneerde reactie een array van run-id&#39;s.

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

`{EXPERIMENT_RUN_ID}`: De id die overeenkomt met de proefrun.\
`{EXPERIMENT_ID}`: De id die overeenkomt met het experiment dat de run uitvoert.

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
`{ACCESS_TOKEN}`: uw specifieke togertokenwaarde die u na verificatie opgeeft.\
`{ORG_ID}`: uw organisatiegegevens zijn gevonden in uw unieke Adobe Experience Platform-integratie.

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
