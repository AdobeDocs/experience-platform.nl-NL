---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInstances
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# MLInstances

Een instantie MLInstance is een huur van een bestaande [Motor](./engines.md) met een aangewezen reeks configuraties die om het even welke trainingsparameters, scoringsparameters, of configuraties van hardwaremiddelen bepaalt.

## Een MLInstance maken {#create-an-mlinstance}

U kunt een instantie tot stand brengen MLI door een POST- verzoek uit te voeren terwijl het verstrekken van een verzoeklading die uit een geldige identiteitskaart van de Motor (`{ENGINE_ID}`) en een aangewezen reeks standaardconfiguraties bestaat.

Als identiteitskaart van de Motor verwijzingen een PySpark of de Motor van de Vonk dan hebt u de capaciteit om de hoeveelheid berekeningsmiddelen zoals het aantal kernen of de hoeveelheid geheugen te vormen. Als er naar een Python-engine wordt verwezen, kunt u kiezen tussen het gebruik van een CPU of GPU voor trainings- en scoringdoeleinden. Raadpleeg de appendix-secties over [PySpark- en Spark-bronconfiguraties](./appendix.md#resource-config) en [Python-CPU- en GPU-configuraties](./appendix.md#cpu-gpu-config) voor meer informatie.

**API-indeling**

```http
POST /mlInstances
```

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "{ENGINE_ID}",
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
| `name` | De gewenste naam voor de MLInstance. Het model dat aan dit MLInstance beantwoordt zal deze waarde erven die in UI als naam van het Model moet worden getoond. |
| `description` | Een optionele beschrijving voor de MLInstance. Het model dat aan dit MLInstance beantwoordt zal deze waarde erven die in UI als beschrijving van het Model moet worden getoond. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde in op een lege tekenreeks. |
| `engineId` | De id van een bestaande engine. |
| `tasks` | Een reeks configuraties voor training, scoring of functiepijpleidingen. |

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van pas gecreëerde MLInstance met inbegrip van zijn uniek herkenningsteken (`id`) bevat.

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

U kunt een lijst van instanties terugwinnen MLInstances door één enkel GET verzoek uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETER}` | Een van de [beschikbare queryparameters](./appendix.md#query) die wordt gebruikt om resultaten te filteren. |
| `{VALUE}` | De waarde voor de voorafgaande vraagparameter. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van instanties MLInstances en hun details terug.

```json
{
    "children": [
        {
            "id": "{MLINSTANCE_ID}",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "{ENGINE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "{MLINSTANCE_ID}",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "{ENGINE_ID}",
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

## Een specifieke MLInstance ophalen {#retrieve-specific}

U kunt de details van een specifieke instantie terugwinnen MLI door een GET verzoek uit te voeren dat identiteitskaart van gewenste MLInstance in de verzoekweg omvat.

**API-indeling**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | De id van de gewenste MLInstance. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord geeft de details van MLInstance terug.

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

## Een MLInstance bijwerken

U kunt een bestaande instantie bijwerken door zijn eigenschappen door een PPUT verzoek te beschrijven die identiteitskaart van doelMLInstance in de verzoekweg omvat en een nuttige lading te verstrekken JSON die bijgewerkte eigenschappen bevat.

>[!TIP] Om ervoor te zorgen dat dit PUT-verzoek succesvol is, wordt u aangeraden eerst een GET-verzoek uit te voeren om de MLInstance door ID [op te](#retrieve-specific)halen. Vervolgens past u het geretourneerde JSON-object aan en werkt u dit bij en past u het gehele gewijzigde JSON-object toe als de payload voor de PUT-aanvraag.

De volgende voorbeeld-API-aanroep werkt de opleidings- en scoringsparameters van een MLInstance bij terwijl deze in eerste instantie beschikken over de volgende eigenschappen:

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

**API-indeling**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Een succesvolle reactie keert een lading terug die de bijgewerkte details van MLInstance bevat.

```json
{
    "id": "{MLINSTANCE_ID}",
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

U kunt alle instanties schrappen MLInstances die de zelfde Motor delen door een verzoek uit te voeren DELETE dat identiteitskaart van de Motor als vraagparameter omvat.

**API-indeling**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENGINE_ID}` | Een geldige engine-id. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId={ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## Een MLInstance verwijderen

U kunt één enkele instantie schrappen MLI door een verzoek uit te voeren DELETE dat identiteitskaart van doelMLInstance in de verzoekweg omvat.

**API-indeling**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```
