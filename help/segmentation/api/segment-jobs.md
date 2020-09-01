---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;segment jobs;segment job;API;api;
solution: Experience Platform
title: Segmenttaken
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# Eindpunt segmenttaken

Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt. Het verwijst naar een [segmentdefinitie](./segment-definitions.md), evenals om het even welk [fusiebeleid](../../profile/api/merge-policies.md) die controleert hoe de [!DNL Real-time Customer Profile] fusies overlappende attributen over uw profielfragmenten samenvoegen. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over het segment, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen.

Deze handleiding bevat informatie die u helpt segmenttaken beter te begrijpen en voorbeelden van API-aanroepen voor het uitvoeren van basishandelingen met de API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Voordat u verdergaat, bekijkt u eerst de gids [](./getting-started.md) Aan de slag voor belangrijke informatie die u moet weten om oproepen naar de API met succes te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Een lijst met segmenttaken ophalen {#retrieve-list}

U kunt een lijst van alle segmentbanen voor uw IMS Organisatie terugwinnen door een verzoek van de GET tot het `/segment/jobs` eindpunt te richten.

**API-indeling**

Het `/segment/jobs` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle uitvoerbanen beschikbaar voor uw organisatie terugwinnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parameters query**

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving aan voor de geretourneerde segmenttaken. | `start=1` |
| `limit` | Geeft het aantal segmenttaken op dat per pagina wordt geretourneerd. | `limit=20` |
| `status` | Filtert de resultaten op basis van status. De ondersteunde waarden zijn NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELING | `status=NEW` |
| `sort` | Hiermee worden de geretourneerde segmenttaken gesorteerd. Wordt geschreven in de indeling `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Hiermee filtert u segmenttaken en haalt u exacte overeenkomsten op voor het opgegeven filter. Deze kan in een van de volgende indelingen worden geschreven: <ul><li>`[jsonObjectPath]==[value]` - filteren op de objecttoets</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filteren binnen de array</li></ul> | `property=segments~segmentId==workInUS` |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert HTTP status 200 met een lijst van segmentbanen voor de gespecificeerde organisatie IMS als JSON terug. De volgende reactie keert een lijst van alle succesvolle segmentbanen voor de organisatie IMS terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte en geeft alleen de eerste geretourneerde taak weer.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id voor de segmenttaak. |
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCEEDED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |
| `metrics` | Een object dat diagnostische informatie bevat over de segmenttaak. |

## Een nieuwe segmenttaak maken {#create}

U kunt een nieuwe segmentbaan tot stand brengen door een verzoek van de POST aan het `/segment/jobs` eindpunt te doen en in het lichaam identiteitskaart van de segmentdefinitie te omvatten waarvan u een nieuw publiek zou willen tot stand brengen.

**API-indeling**

```http
POST /segment/jobs
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentId` | De id van de segmentdefinitie waarvoor u een segmenttaak wilt maken. Meer informatie over segmentdefinities kan in de gids [van het](./segment-definitions.md)segmentdefinitieeindpunt worden gevonden. |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde segmentbaan terug.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id voor de nieuwe segmenttaak. |
| `status` | De huidige status voor de segmenttaak. Aangezien de segmentbaan nieuw wordt gecreeerd, zal de status altijd &quot;NIEUW&quot;zijn. |
| `segments` | Een object dat informatie bevat over de segmentdefinities waarop deze segmenttaak wordt uitgevoerd. |
| `segments.segment.id` | De id van de segmentdefinitie die u hebt opgegeven. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |

## Een specifieke segmenttaak ophalen {#get}

U kunt gedetailleerde informatie over een specifieke segmentbaan terugwinnen door een verzoek van de GET aan het `/segment/jobs` eindpunt te doen en identiteitskaart van de segmentbaan te verstrekken u in de verzoekweg wenst terug te winnen.

**API-indeling**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | De `id` waarde van de segmentbaan u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde segmentbaan terug.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id voor de segmenttaak. |
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCEEDED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |
| `metrics` | Een object dat diagnostische informatie bevat over de segmenttaak. |

## Ophaalsegmenttaken bulksgewijs opvragen {#bulk-get}

U kunt gedetailleerde informatie over veelvoudige segmentbanen terugwinnen door een verzoek van de POST aan het `/segment/jobs/bulk-get` eindpunt te doen en de `id` waarden van de segmentbanen in het verzoeklichaam te verstrekken.

**API-indeling**

```http
POST /segment/jobs/bulk-get
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**Antwoord**

Een succesvolle reactie keert status 207 van HTTP met de gevraagde segmentbanen terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor ruimte, slechts tonend gedeeltelijke details van elke segmentbaan. De volledige reactie zal de volledige details voor de gevraagde segmentbanen vermelden.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id voor de segmenttaak. |
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCEEDED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |

## Een specifieke segmenttaak annuleren of verwijderen {#delete}

U kunt een specifieke segmentbaan schrappen door een verzoek van DELETE aan het `/segment/jobs` eindpunt te doen en identiteitskaart van de segmentbaan te verstrekken u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>De API-reactie op de verwijderaanvraag is onmiddellijk. Nochtans, is de daadwerkelijke schrapping van de segmentbaan asynchroon. Met andere woorden, er is een tijdverschil tussen wanneer het schrappingsverzoek aan de segmentbaan wordt gemaakt en wanneer het wordt toegepast.

**API-indeling**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | De `id` waarde van de segmenttaak die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 204 met de volgende informatie.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de segmentbanen werken.