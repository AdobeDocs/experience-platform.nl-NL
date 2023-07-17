---
solution: Experience Platform
title: Segment Definition API Endpoint
description: Het eindpunt van segmentdefinities in de Dienst API van de Segmentatie van Adobe Experience Platform staat u toe om segmentdefinities voor uw organisatie programmatically te beheren.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# Definitieeindpunt van segment

Met Adobe Experience Platform kunt u segmentdefinities maken die een groep specifieke kenmerken of gedragingen definiëren op basis van een groep profielen. Een segmentdefinitie is een object waarin een query is opgenomen [!DNL Profile Query Language] (PQL). Segmentdefinities worden toegepast op profielen om een publiek te maken. Dit object (segmentdefinitie) wordt ook wel een PQL-voorspelling genoemd. PQL bepaalt de regels voor de segmentdefinitie die op voorwaarden met betrekking tot om het even welke verslag of tijdreeksgegevens wordt gebaseerd u verstrekt aan [!DNL Real-Time Customer Profile]. Zie de [PQL-hulplijn](../pql/overview.md) voor meer informatie over het schrijven van vragen PQL.

Deze gids verstrekt informatie om u te helpen segmentdefinities beter begrijpen en omvat steekproefAPI vraag voor het uitvoeren van basisacties gebruikend API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met segmentdefinities ophalen {#list}

U kunt een lijst van alle segmentdefinities voor uw organisatie terugwinnen door een verzoek van de GET tot de `/segment/definitions` eindpunt.

**API-indeling**

De `/segment/definitions` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle segmentdefinities beschikbaar voor uw organisatie terugwinnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parameters query**

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving aan voor de gesegmenteerde definities die worden geretourneerd. | `start=4` |
| `limit` | Geeft het aantal segmentdefinities op dat per pagina wordt geretourneerd. | `limit=20` |
| `page` | Geeft aan vanaf welke pagina de resultaten van segmentdefinities moeten beginnen. | `page=5` |
| `sort` | Hiermee geeft u aan op welk veld de resultaten moeten worden gesorteerd. Wordt geschreven in de volgende indeling: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Geeft aan of de segmentdefinitie streaming-ingeschakeld is. | `evaluationInfo.continuous.enabled=true` |

**Verzoek**

Het volgende verzoek zal de laatste twee segmentdefinities terugwinnen die binnen uw organisatie worden gepost.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met een lijst van segmentdefinities voor de gespecificeerde organisatie als JSON terug.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Een nieuwe segmentdefinitie maken {#create}

U kunt een nieuwe segmentdefinitie tot stand brengen door een verzoek van de POST aan `/segment/definitions` eindpunt.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een unieke naam waarmee naar de segmentdefinitie moet worden verwezen. |
| `description` | (Optioneel.) Een beschrijving van de segmentdefinitie die u maakt. |
| `evaluationInfo` | (Optioneel.) Het type segmentdefinitie dat u maakt. Als u een batchsegment wilt maken, stelt u `evaluationInfo.batch.enabled` om waar te zijn. Als u een streaming segment wilt maken, stelt u `evaluationInfo.continuous.enabled` om waar te zijn. Als u een randsegment wilt maken, stelt u `evaluationInfo.synchronous.enabled` om waar te zijn. Als deze optie leeg blijft, wordt de segmentdefinitie gemaakt als een **partij** segment. |
| `schema` | Het schema dat is gekoppeld aan de entiteiten in het segment. Bestaat uit een van de `id` of `name` veld. |
| `expression` | Een entiteit die veldinformatie over de segmentdefinitie bevat. |
| `expression.type` | Geeft het expressietype aan. Momenteel wordt alleen &quot;PQL&quot; ondersteund. |
| `expression.format` | Geeft de structuur van de expressie in waarde aan. Momenteel wordt de volgende indeling ondersteund: <ul><li>`pql/text`: Een tekstuele representatie van een segmentdefinitie, volgens de gepubliceerde PQL-grammatica.  Bijvoorbeeld, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Een expressie die overeenkomt met het type dat wordt aangegeven in `expression.format`. |

<!-- >[!NOTE]
>
>A segment definition expression may also reference a computed attribute. To learn more, please refer to the [computed attribute API endpoint guide](../../profile/computed-attributes/ca-api.md)
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change. -->

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde segmentdefinitie terug.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde id van de zojuist gemaakte segmentdefinitie. |
| `evaluationInfo` | Een object dat aangeeft welk type evaluatie de segmentdefinitie zal ondergaan. Het kan batch-, streaming- (ook wel doorlopend genoemd) of randsegmentatie (ook wel synchroon genoemd) zijn. |

## Een specifieke segmentdefinitie ophalen {#get}

U kunt gedetailleerde informatie over een specifieke segmentdefinitie terugwinnen door een verzoek van de GET tot de `/segment/definitions` eindpunt en het verstrekken van identiteitskaart van de segmentdefinitie u wenst om in de verzoekweg terug te winnen.

**API-indeling**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SEGMENT_ID}` | De `id` waarde van de segmentdefinitie u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde segmentdefinitie terug.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id van de segmentdefinitie. |
| `name` | Een unieke naam waarmee naar de segmentdefinitie moet worden verwezen. |
| `schema` | Het schema dat is gekoppeld aan de entiteiten in het segment. Bestaat uit een van de `id` of `name` veld. |
| `expression` | Een entiteit die veldinformatie over de segmentdefinitie bevat. |
| `expression.type` | Geeft het expressietype aan. Momenteel wordt alleen &quot;PQL&quot; ondersteund. |
| `expression.format` | Geeft de structuur van de expressie in waarde aan. Momenteel wordt de volgende indeling ondersteund: <ul><li>`pql/text`: Een tekstuele representatie van een segmentdefinitie, volgens de gepubliceerde PQL-grammatica.  Bijvoorbeeld, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Een expressie die overeenkomt met het type dat wordt aangegeven in `expression.format`. |
| `description` | Een door mensen leesbare beschrijving van de definitie. |
| `evaluationInfo` | Een object dat aangeeft welk type evaluatie, batch, streaming (ook wel doorlopend genoemd) of rand (ook wel synchroon genoemd), de segmentdefinitie wordt uitgevoerd. |

## Bulk haalt segmentdefinities op {#bulk-get}

U kunt gedetailleerde informatie over veelvoudige gespecificeerde segmentdefinities terugwinnen door een verzoek van de POST aan `/segment/definitions/bulk-get` en het verstrekken van `id` waarden van de segmentdefinities in de aanvraaginstantie.

**API-indeling**

```http
POST /segment/definitions/bulk-get
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Antwoord**

Een succesvolle reactie keert status 207 van HTTP met de gevraagde segmentdefinities terug.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id van de segmentdefinitie. |
| `name` | Een unieke naam waarmee naar de segmentdefinitie moet worden verwezen. |
| `schema` | Het schema dat is gekoppeld aan de entiteiten in het segment. Bestaat uit een van de `id` of `name` veld. |
| `expression` | Een entiteit die veldinformatie over de segmentdefinitie bevat. |
| `expression.type` | Geeft het expressietype aan. Momenteel wordt alleen &quot;PQL&quot; ondersteund. |
| `expression.format` | Geeft de structuur van de expressie in waarde aan. Momenteel wordt de volgende indeling ondersteund: <ul><li>`pql/text`: Een tekstuele representatie van een segmentdefinitie, volgens de gepubliceerde PQL-grammatica.  Bijvoorbeeld, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Een expressie die overeenkomt met het type dat wordt aangegeven in `expression.format`. |
| `description` | Een door mensen leesbare beschrijving van de definitie. |
| `evaluationInfo` | Een object dat aangeeft welk type evaluatie, batch, streaming (ook wel doorlopend genoemd) of rand (ook wel synchroon genoemd), de segmentdefinitie wordt uitgevoerd. |

## Een specifieke segmentdefinitie verwijderen {#delete}

U kunt verzoeken om een specifieke segmentdefinitie te schrappen door een verzoek van de DELETE tot de `/segment/definitions` eindpunt en het verstrekken van identiteitskaart van de segmentdefinitie u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
> Een segmentdefinitie die wordt gebruikt in een doelactivering **kan** worden geschrapt.

**API-indeling**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SEGMENT_ID}` | De `id` waarde van de segmentdefinitie die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 zonder bericht.

## Een specifieke segmentdefinitie bijwerken

U kunt een specifieke segmentdefinitie bijwerken door een PATCH-verzoek in te dienen bij de `/segment/definitions` eindpunt en het verstrekken van identiteitskaart van de segmentdefinitie u wenst om in de verzoekweg bij te werken.

**API-indeling**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SEGMENT_ID}` | De `id` waarde van de segmentdefinitie u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek wordt het land van het werkadres van de VS naar Canada bijgewerkt.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs bijgewerkte segmentdefinitie terug. U ziet hoe het werkadresland is bijgewerkt van de VS (VS) naar Canada (CA).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Segmentdefinitie omzetten

U kunt een segmentdefinitie omzetten tussen `pql/text` en `pql/json` of `pql/json` tot `pql/text` door een POST aan de `/segment/conversion` eindpunt.

**API-indeling**

```http
POST /segment/conversion
```

**Verzoek**

Met het volgende verzoek wordt de indeling van de segmentdefinitie gewijzigd van `pql/text` tot `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs omgezette segmentdefinitie terug.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de segmentdefinities werken. Lees voor meer informatie over het maken van een segment de [een segment maken](../tutorials/create-a-segment.md) zelfstudie.
