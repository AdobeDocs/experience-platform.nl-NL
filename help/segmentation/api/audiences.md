---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;publiek;publiek;API;api;
title: API-eindpunt voor soorten publiek
topic-legacy: developer guide
description: Het publiek eindpunt in de API van de Dienst van de Segmentatie van Adobe Experience Platform staat u toe om publiek voor uw organisatie programmatically te beheren.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: f4ec5b82a14579de5bf228011d14a849898be9f5
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 0%

---

# Eind publiek

>[!IMPORTANT]
>
>Het publiekseindpunt is momenteel in bèta en is niet beschikbaar aan alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Een publiek is een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze verzamelingen mensen kunnen worden gegenereerd met Adobe Experience Platform of met externe bronnen. U kunt de `/audiences` eindpunt in de Segmentatie API, die u toestaat om publiek programmatically terug te winnen, tot stand te brengen bij te werken en te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met soorten publiek ophalen {#list}

U kunt een lijst van alle soorten publiek voor uw organisatie terugwinnen door een verzoek van de GET aan te dienen `/audiences` eindpunt.

**API-indeling**

De `/audiences` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle publiek beschikbaar voor uw organisatie worden teruggewonnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

De volgende vraagparameters kunnen worden gebruikt wanneer het terugwinnen van een lijst van publiek:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving voor het geretourneerde publiek aan. | `start=5` |
| `limit` | Hiermee geeft u het maximale aantal bezoekers op dat per pagina wordt geretourneerd. | `limit=10` |
| `sort` | Hiermee geeft u de volgorde op waarin de resultaten moeten worden gesorteerd. Dit is geschreven in de indeling `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Een filter waarmee u een publiek kunt opgeven dat **exact** komt overeen met de waarde van een kenmerk. Dit is geschreven in de indeling `property=` | `property=audienceId==test-audience-id` |
| `name` | Een filter waarmee u een publiek kunt opgeven waarvan de namen **bevatten** de opgegeven waarde. Deze waarde is niet hoofdlettergevoelig. | `name=Sample` |
| `description` | Een filter waarmee u een publiek kunt opgeven waarvan de beschrijvingen **bevatten** de opgegeven waarde. Deze waarde is niet hoofdlettergevoelig. | `description=Test Description` |
| `withMetrics` | Een filter dat de metriek naast het publiek terugkeert. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Voor het publiek worden meetgegevens geretourneerd onder de `metrics` en bevat informatie over het aantal profielen, het maken en bijwerken van tijdstempels.

**Geen metriek**

Het volgende verzoek/reactiepaar wordt gebruikt wanneer `withMetrics` queryparameter is niet aanwezig.

**Verzoek**

Het volgende verzoek wint de laatste vijf publiek terug dat in uw organisatie wordt gecreeerd.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Antwoord** {#no-metrics}

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van soorten publiek die in uw organisatie als JSON zijn gemaakt.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte, en toont slechts het eerste teruggekeerde publiek.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
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
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Eigenschap | Type publiek | Beschrijving |
| -------- | ------------- | ----------- | 
| `id` | Beide | Een door het systeem gegenereerde alleen-lezen id voor het publiek. |
| `audienceId` | Beide | Als het publiek een publiek is dat door een Platform wordt gegenereerd, is dit dezelfde waarde als de `id`. Als het publiek extern wordt gegenereerd, wordt deze waarde door de client opgegeven. |
| `schema` | Beide | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `imsOrgId` | Beide | De id van de organisatie waartoe het publiek behoort. |
| `sandbox` | Beide | Informatie over de sandbox waartoe het publiek behoort. Meer informatie over sandboxen vindt u in de [sandboxen, overzicht](../../sandboxes/home.md). |
| `name` | Beide | De naam van het publiek. |
| `description` | Beide | Een beschrijving van het publiek. |
| `expression` | Door Platform gegenereerd | De PQL-expressie (Profile Query Language) van het publiek. Meer informatie over PQL-expressies vindt u in het gedeelte [Hulplijn voor PQL-expressies](../pql/overview.md). |
| `mergePolicyId` | Door Platform gegenereerd | De id van het samenvoegbeleid waaraan het publiek is gekoppeld. Meer informatie over het samenvoegbeleid vindt u in het gedeelte [handleiding voor samenvoegbeleid](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Door Platform gegenereerd | Toont hoe het publiek zal worden geëvalueerd. Mogelijke evaluatiemethoden zijn batch, streaming of edge. Meer informatie over de evaluatiemethoden vindt u in de [segmentatieoverzicht](../home.md) |
| `dependents` | Beide | Een array met gebruikers-id&#39;s die afhankelijk zijn van het huidige publiek. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `dependencies` | Beide | Een array met publiek-id&#39;s waarvan het publiek afhankelijk is. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `type` | Beide | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het Platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalAudience`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalAudience` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `createdBy` | Beide | De id van de gebruiker die het publiek heeft gemaakt. |
| `labels` | Beide | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `namespace` | Beide | De naamruimte waartoe het publiek behoort. Mogelijke waarden zijn `AAM`, `AAMSegments`, `AAMTraits`, en `AEPSegments`. |
| `audienceMeta` | Extern | Extern gemaakte metagegevens van het extern gemaakte publiek. |

**Met metriek**

Het volgende verzoek/reactiepaar wordt gebruikt wanneer `withMetrics` queryparameter is aanwezig.

**Verzoek**

Het volgende verzoek wint de laatste vijf publiek, met metriek terug, dat in uw organisatie wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van soorten publiek, met meetwaarden, voor de opgegeven organisatie als JSON.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte, en toont slechts het eerste teruggekeerde publiek.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

De volgende lijst bevat eigenschappen **exclusief** aan de `withMetrics` reactie. Als u de standaardpubliekseigenschappen wilt kennen, gelieve te lezen [vorige sectie](#no-metrics).

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `metrics.imsOrgId` | De organisatie-id van het publiek. |
| `metrics.sandbox` | De sandboxinformatie voor het publiek. |
| `metrics.jobId` | De id van de segmenttaak die het publiek verwerkt. |
| `metrics.type` | Het type segmenttaak. Dit kan `export` of `batch_segmentation`. |
| `metrics.id` | De publieksidentiteitskaart |
| `metrics.data` | Metriek die verwant zijn aan het publiek. Dit omvat informatie zoals het totale aantal profielen inbegrepen in het publiek, het totale aantal profielen op een per-namespacebasis, en het totale aantal profielen op een per-statusbasis. |
| `metrics.createEpoch` | Een tijdstempel dat aangeeft wanneer het publiek is gemaakt. |
| `metrics.updateEpoch` | Een tijdstempel dat aangeeft wanneer het publiek voor het laatst is bijgewerkt. |

## Een nieuw publiek maken {#create}

U kunt een nieuw publiek tot stand brengen door een verzoek van de POST aan `/audiences` eindpunt.

**API-indeling**

```http
POST /audiences
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `name` | De naam van het publiek. |
| `description` | Een beschrijving van het publiek. |
| `type` | Een veld waarin wordt weergegeven of het publiek door Platforms wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalAudience`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalAudience` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `expression` | De PQL-expressie (Profile Query Language) van het publiek. Meer informatie over PQL-expressies vindt u in het gedeelte [Hulplijn voor PQL-expressies](../pql/overview.md). |
| `schema` | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

**Antwoord**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Een bepaald publiek opzoeken {#get}

U kunt gedetailleerde informatie over een specifiek publiek opzoeken door een verzoek van de GET aan het `/audiences` eindpunt en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg terug te winnen.

**API-indeling**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parameter | Beschrijving |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | De id van het publiek dat u probeert op te halen. |
| `property=withmetrics==true` | Een optionele queryparameter die u kunt gebruiken als u een opgegeven publiek wilt ophalen met de publieksmeetgegevens. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over het gespecificeerde publiek terug. De reactie is anders, afhankelijk van of het publiek wordt gegenereerd met Adobe Experience Platform of externe bronnen.

**Door Platform gegenereerd**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Extern gegenereerd**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Een veld bijwerken voor een publiek {#update-field}

U kunt de velden van specifieke doelgroepen bijwerken door een PATCH-aanvraag in te dienen bij de `/audiences` en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg bij te werken.

**API-indeling**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | Voor het bijwerken van soorten publiek is deze waarde altijd `add`. |
| `path` | Het pad van het veld dat u wilt bijwerken. |
| `value` | De waarde waaraan u het veld wilt bijwerken. |

**Antwoord**

Een geslaagde reactie geeft HTTP status 200 met informatie over uw onlangs bijgewerkte publiek terug.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Een publiek bijwerken {#put}

U kunt een specifiek publiek bijwerken (overschrijven) door een verzoek van de PUT aan het `/audiences` en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg bij te werken.

**API-indeling**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Verzoek**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `audienceId` | De id van het publiek. Dit wordt gebruikt door externe doelgroepen |
| `name` | De naam van het publiek. |
| `namespace` |  |
| `description` | Een beschrijving van het publiek. |
| `type` | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het Platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalAudience`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalAudience` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `lifecycle` | De status van het publiek. Mogelijke waarden zijn `draft`, `published`, `inactive`, en `archived`. `draft` vertegenwoordigt wanneer het publiek wordt gecreëerd; `published` wanneer het publiek wordt gepubliceerd; `inactive` wanneer het publiek niet langer actief is, en `archived` als het publiek wordt verwijderd. |
| `datasetId` | De id van de dataset die de publieksgegevens kunnen worden gevonden. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details over uw onlangs bijgewerkte publiek. Houd er rekening mee dat de details van uw publiek verschillen, afhankelijk van het publiek dat door een Platform wordt gegenereerd of een publiek dat extern wordt gegenereerd.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Een publiek verwijderen {#delete}

U kunt een specifiek publiek verwijderen door een DELETE-aanvraag in te dienen bij de `/audiences` eindpunt en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP status 204 zonder bericht.
