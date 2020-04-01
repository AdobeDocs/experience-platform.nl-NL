---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Inzichten
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Inzichten

Inzichten bevatten meetgegevens die worden gebruikt om een gegevenswetenschapper in staat te stellen optimale XML-modellen te evalueren en te kiezen door relevante evaluatiemetriek weer te geven.

## Een lijst met inzichten ophalen

U kunt een lijst van Inzichten terugwinnen door één enkel GET verzoek aan het inzichten eindpunt uit te voeren.  Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /insights
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een lijst met inzichten bevat en elk inzicht een unieke id ( `id` ) heeft. Bovendien, zult u ontvangen `context` die de unieke herkenningstekens bevat die met dat bepaalde inzicht na de gebeurtenissen van Inzichten en metrieke gegevens worden geassocieerd.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | The ID corresponding to the Insight. |
| `experimentId` | Een geldige experimentele id. |
| `experimentRunId` | Een geldige uitvoerings-id voor Experimenten. |
| `modelId` | Een geldige model-id. |

## Een specifiek inzicht ophalen

Om omhoog een bepaald inzicht te zoeken maak een GET verzoek en verstrek een geldig `{INSIGHT_ID}` in de verzoekweg. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /insights/{INSIGHT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{INSIGHT_ID}` | De unieke id van een Sensei-inzicht. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de inzichten als unieke id (`id`) bevat. Bovendien zult u ontvangen `context` die de unieke herkenningstekens bevat die met het bepaalde inzicht na de gebeurtenissen van Inzichten en metrieke gegevens worden geassocieerd.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | The ID corresponding to the Insight. |
| `experimentId` | Een geldige experimentele id. |
| `experimentRunId` | Een geldige uitvoerings-id voor Experimenten. |
| `modelId` | Een geldige model-id. |

## Nieuw modelinzicht toevoegen

U kunt een nieuw Modelinzicht tot stand brengen door een POST- verzoek en een lading uit te voeren die context, gebeurtenissen, en metriek voor het nieuwe Model inzicht verstrekt. Het contextgebied dat wordt gebruikt om een nieuw Model inzicht tot stand te brengen wordt niet vereist om de bestaande diensten in bijlage aan het te hebben maar u kunt verkiezen om het nieuwe Model inzicht met de bestaande diensten tot stand te brengen door één of meerdere overeenkomstige IDs te verstrekken:

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**API-indeling**

```http
POST /insights
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Antwoord**

Een succesvolle reactie zal een lading terugkeren die een `{INSIGHT_ID}` en om het even welke parameters heeft die u in het aanvankelijke verzoek verstrekte.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `insightId` | De unieke id die voor dit bepaalde inzicht wordt gemaakt wanneer een succesvol POST-verzoek wordt gedaan. |

## Hiermee wordt een lijst met standaardmetriek voor algoritmen opgehaald

U kunt een lijst van al uw algoritme en standaardmetriek terugwinnen door één enkele GET verzoek aan het metrieke eindpunt uit te voeren. Om metrisch te vragen maak een GET verzoek en verstrek een geldig `{ALGORITHM}` in de verzoekweg.

**API-indeling**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ALGORITHM}` | The identifier of the algorithm type. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint specifieke metrisch door het algoritmeherkenningsteken te gebruiken terug `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de `algorithm` unieke id en een array van standaardmeetgegevens bevat.

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
