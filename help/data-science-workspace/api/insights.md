---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;inzichten;sensei machine learning api
solution: Experience Platform
title: Insights API Endpoint
description: Inzichten bevatten meetgegevens die worden gebruikt om een gegevenswetenschapper in staat te stellen optimale XML-modellen te evalueren en te kiezen door relevante evaluatiemetriek weer te geven.
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Beginpunt

Inzichten bevatten meetgegevens die worden gebruikt om een gegevenswetenschapper in staat te stellen optimale XML-modellen te evalueren en te kiezen door relevante evaluatiemetriek weer te geven.

## Een lijst met inzichten ophalen

U kunt een lijst van Inzichten terugwinnen door één enkel verzoek van GET tot het inzichten eindpunt uit te voeren.  Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [queryparameters voor ophalen van elementen](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert een payload die een lijst met inzichten bevat en elk inzicht heeft een unieke id ( `id` ). Bovendien ontvangt u `context` die de unieke id&#39;s bevat die zijn gekoppeld aan dat bepaalde inzicht dat volgt op de gebeurtenissen Insights en metrische gegevens.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Als u een bepaald inzicht wilt opzoeken, vraagt u een GET aan en geeft u een geldige `{INSIGHT_ID}` in het aanvraagpad. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [queryparameters voor ophalen van elementen](./appendix.md#query).

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
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de unieke id voor inzichten bevat (`id`). Bovendien ontvangt u `context` die de unieke id&#39;s bevat die zijn gekoppeld aan het specifieke inzicht dat volgt op de gebeurtenissen Insights en metrische gegevens.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

U kunt een nieuw Modelinzicht tot stand brengen door een verzoek van de POST en een nuttige lading uit te voeren die context, gebeurtenissen, en metriek voor het nieuwe Modelinzicht verstrekt. Het contextgebied dat wordt gebruikt om een nieuw Model inzicht tot stand te brengen wordt niet vereist om de bestaande diensten in bijlage aan het te hebben maar u kunt verkiezen om het nieuwe Model inzicht met de bestaande diensten tot stand te brengen door één of meerdere overeenkomstige IDs te verstrekken:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Een geslaagde reactie retourneert een lading die een `{INSIGHT_ID}` en alle parameters die u in het oorspronkelijke verzoek hebt opgegeven.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `insightId` | De unieke id die voor dit bepaalde inzicht wordt gemaakt wanneer een POST met succes wordt aangevraagd. |

## Hiermee wordt een lijst met standaardmetriek voor algoritmen opgehaald

U kunt een lijst van al uw algoritme en standaardmetriek terugwinnen door één enkel verzoek van de GET aan het metrieke eindpunt uit te voeren. Om bepaalde metrisch te vragen doe een verzoek van de GET en verstrek geldig `{ALGORITHM}` in het aanvraagpad.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de `algorithm` unieke id en een array van standaardmeetgegevens.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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
