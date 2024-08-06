---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;mlinstances;sensei machine learning api
solution: Experience Platform
title: XMLInstances API Endpoint
description: Een MLInstance is een huur van een bestaande Motor met een aangewezen reeks configuraties die om het even welke trainingsparameters, het scoren parameters, of configuraties van hardwaremiddelen bepalen.
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# MLInstances-eindpunt

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Een instantie MLInstance is het verpakken van een bestaande [ Motor ](./engines.md) met een aangewezen reeks configuraties die om het even welke opleidingsparameters, het scoren parameters, of configuraties van het hardwaremiddel bepaalt.

## Een MLInstance maken {#create-an-mlinstance}

U kunt een instantie tot stand brengen MLI door een verzoek van de POST uit te voeren terwijl het verstrekken van een verzoeklading die uit geldige identiteitskaart van de Motor (`{ENGINE_ID}`) en een aangewezen reeks standaardconfiguraties bestaat.

Als identiteitskaart van de Motor verwijzingen een PySpark of de Motor van de Vonk dan hebt u de capaciteit om de hoeveelheid berekeningsmiddelen zoals het aantal kernen of de hoeveelheid geheugen te vormen. Als er naar een Python-engine wordt verwezen, kunt u kiezen tussen het gebruik van een CPU of GPU voor trainings- en scoringdoeleinden. Verwijs naar de appendix secties op [ PySpark en de het middelconfiguraties van de Vonk ](./appendix.md#resource-config) en [ Pypthon cpu en GPU configuraties ](./appendix.md#cpu-gpu-config) voor meer informatie.

**API Formaat**

```http
POST /mlInstances
```

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De gewenste naam voor de instantie. Het model dat overeenkomt met deze instantie neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als de naam van het model. |
| `description` | Een optionele beschrijving voor de MLInstance. Het model dat overeenkomt met deze instantie neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als de beschrijving van het model. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde ervan in op een lege tekenreeks. |
| `engineId` | De id van een bestaande engine. |
| `tasks` | Een set configuraties voor training, scores of functiepijplijnen. |

**Reactie**

Een succesvolle reactie keert een lading terug die de details van pas gecreëerde MLInstance met inbegrip van zijn uniek herkenningsteken (`id`) bevat.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Een lijst met MLInstances ophalen

U kunt een lijst van instanties terugwinnen MLInstances door één enkel verzoek van de GET uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de appendix sectie op [ vraagparameters voor activaherwinning ](./appendix.md#query).

**API Formaat**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETER}` | Één van de [ beschikbare vraagparameters ](./appendix.md#query) die aan filterresultaten wordt gebruikt. |
| `{VALUE}` | De waarde voor de voorafgaande vraagparameter. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van instanties MLInstances en hun details terug.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Hiermee wordt een specifieke MLInstance opgehaald {#retrieve-specific}

U kunt de details van een specifieke instantie terugwinnen door een verzoek uit te voeren van de GET dat identiteitskaart van gewenste MLInstance in de verzoekweg omvat.

**API Formaat**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | De id van de gewenste instantie. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie retourneert de details van de MLInstance.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Een MLInstance bijwerken

U kunt een bestaande HTMLInstance bijwerken door zijn eigenschappen door een verzoek van de PUT te beschrijven dat identiteitskaart van doelMLInstance in de verzoekweg omvat en een nuttige lading JSON verstrekt die bijgewerkte eigenschappen bevat.

>[!TIP]
>
>om het succes van dit verzoek van de PUT te verzekeren, wordt gesuggereerd dat eerst u een verzoek van de GET om [ uitvoert MLInstance door identiteitskaart ](#retrieve-specific) terug te winnen. Vervolgens past u het geretourneerde JSON-object aan en werkt u het bij en past u het gehele gewijzigde JSON-object toe als de payload voor het verzoek om PUT.

De volgende voorbeeld-API-aanroep werkt de trainings- en scoringsparameters van een instantie bij terwijl deze eigenschappen in eerste instantie worden gebruikt:

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API Formaat**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Reactie**

Een succesvolle reactie keert een lading terug die de bijgewerkte details van MLInstance bevat.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## MLInstances by Engine ID verwijderen

U kunt alle instanties schrappen die de zelfde Motor delen door een verzoek uit te voeren van de DELETE dat identiteitskaart van de Motor als vraagparameter omvat.

**API Formaat**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENGINE_ID}` | Een geldige engine-id. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## Een MLInstance verwijderen

U kunt één enkele instantie schrappen MLI door een verzoek uit te voeren van de DELETE dat doelID MLInstance in de verzoekweg omvat.

**API Formaat**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```
