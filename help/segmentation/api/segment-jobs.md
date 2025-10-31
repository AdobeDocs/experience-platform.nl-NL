---
solution: Experience Platform
title: API-eindpunt segmenttaken
description: Het eindpunt van segmentbanen in de API van de Dienst van de Segmentatie van Adobe Experience Platform staat u toe om segmentbanen voor uw organisatie programmatically te beheren.
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# Eindpunt segmenttaken

Een segmentbaan is een asynchroon proces dat tot een publiekssegment op bestelling leidt. Het verwijzingen a [&#x200B; segmentdefinitie &#x200B;](./segment-definitions.md), evenals om het even welk [&#x200B; samenvoegbeleid &#x200B;](../../profile/api/merge-policies.md) controlerend hoe [!DNL Real-Time Customer Profile] overlappende attributen over uw profielfragmenten samenvoegt. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over het segment, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen.

Deze handleiding bevat informatie die u helpt segmenttaken beter te begrijpen en voorbeelden van API-aanroepen voor het uitvoeren van basishandelingen met de API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met segmenttaken ophalen {#retrieve-list}

U kunt een lijst van alle segmentbanen voor uw organisatie terugwinnen door een GET- verzoek aan het `/segment/jobs` eindpunt te doen.

**API formaat**

Het `/segment/jobs` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle uitvoerbanen beschikbaar voor uw organisatie terugwinnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**de parameters van de Vraag**

+++ Een lijst met beschikbare queryparameters.

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving aan voor de geretourneerde segmenttaken. | `start=1` |
| `limit` | Geeft het aantal segmenttaken op dat per pagina wordt geretourneerd. | `limit=20` |
| `status` | Hiermee filtert u de resultaten op basis van de status. De ondersteunde waarden zijn NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELING | `status=NEW` |
| `sort` | Hiermee worden de geretourneerde segmenttaken gesorteerd. | Wordt geschreven in de indeling `[attributeName]:[desc\|asc]` . `sort=creationTime:desc` |
| `property` | Hiermee filtert u segmenttaken en haalt u exacte overeenkomsten op voor het opgegeven filter. Deze kan in een van de volgende indelingen worden geschreven: <ul><li>`[jsonObjectPath]==[value]` - filteren op de objecttoets</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filteren binnen de array</li></ul> | `property=segments~segmentId==workInUS` |

+++

**Verzoek**

+++ Een voorbeeldverzoek om een lijst met segmenttaken weer te geven.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van segmentbanen voor de gespecificeerde organisatie als JSON terug. Een volledige lijst van alle segmentdefinities zal binnen het `children.segments` attribuut worden getoond.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte en geeft alleen de eerste geretourneerde taak weer.

+++ Een voorbeeldreactie bij het ophalen van een lijst met segmenttaken. 

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |
| `metrics` | Een object dat diagnostische informatie bevat over de segmenttaak. |
| `metrics.totalTime` | Een object dat informatie bevat over de tijd waarop de segmentatietaak is gestart en beëindigd en over de totale tijd die is gevergd. |
| `metrics.profileSegmentationTime` | Een object dat informatie bevat over de tijd waarop de segmentatieevaluatie is gestart en beëindigd, en over de totale tijd die is verstreken. |
| `metrics.segmentProfileCounter` | Het aantal profielen dat per segment wordt gekwalificeerd. |
| `metrics.segmentedProfileByNamespaceCounter` | Het aantal profielen dat voor elke identiteitsnaamruimte op een basis van de segmentdefinitie wordt gekwalificeerd. |
| `metrics.segmentProfileByStatusCounter` | Het aantal profielen voor elke status. De volgende drie statussen worden ondersteund: <ul><li>&quot;gerealiseerd&quot; - Het aantal profielen dat in aanmerking komt voor de segmentdefinitie.</li><li>&quot;exited&quot; - Het aantal profielen dat niet meer bestaat in de segmentdefinitie.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Het totale aantal samengevoegde profielen op een per de beleidsbasis van de fusie. |

+++

## Een nieuwe segmenttaak maken {#create}

U kunt een nieuwe segmentbaan tot stand brengen door een POST- verzoek aan het `/segment/jobs` eindpunt en met inbegrip van IDs van de segmentdefinitie in het verzoeklichaam te doen.

**API formaat**

```http
POST /segment/jobs
```

**Verzoek**

+++Een voorbeeldverzoek om een nieuwe segmenttaak te maken

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentId` | De id van de segmentdefinitie die u wilt evalueren. Deze segmentdefinities kunnen tot verschillende samenvoegbeleidsregels behoren. Meer informatie over segmentdefinities kan in de [&#x200B; gids van het eindpunt van de segmentdefinitie &#x200B;](./segment-definitions.md) worden gevonden. |

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw pas gecreëerde segmentbaan terug.

+++ Een voorbeeldreactie bij het maken van een nieuwe segmenttaak.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen-id voor de nieuwe segmenttaak. |
| `status` | De huidige status voor de segmenttaak. Aangezien de segmentbaan nieuw wordt gecreeerd, zal de status altijd &quot;NIEUW&quot;zijn. |
| `segments` | Een object dat informatie bevat over de segmentdefinities waarop deze segmenttaak wordt uitgevoerd. |
| `segments.segment.id` | De id van de segmentdefinitie die u hebt opgegeven. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |

+++

## Een specifieke segmenttaak ophalen {#get}

U kunt gedetailleerde informatie over een specifieke segmentbaan terugwinnen door een GET- verzoek aan het `/segment/jobs` eindpunt te doen en identiteitskaart van de segmentbaan te verstrekken u in de verzoekweg wenst terug te winnen.

**API formaat**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | De `id` -waarde van de segmenttaak die u wilt ophalen. |

**Verzoek**

+++ Een voorbeeldverzoek om een segmenttaak op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde segmentbaan terug. Een volledige lijst van alle segmentdefinities zal binnen het `children.segments` attribuut worden getoond.

+++ Een voorbeeldreactie voor het ophalen van een segmenttaak.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |
| `metrics` | Een object dat diagnostische informatie bevat over de segmenttaak. |

+++

>[!ENDTABS]

## Ophaalsegmenttaken bulksgewijs opvragen {#bulk-get}

U kunt gedetailleerde informatie over veelvoudige segmentbanen terugwinnen door een POST- verzoek aan het `/segment/jobs/bulk-get` eindpunt te doen en de `id` waarden van de segmentbanen in het verzoeklichaam te verstrekken.

**API formaat**

```http
POST /segment/jobs/bulk-get
```

**Verzoek**

+++ Een steekproefverzoek om het bulk te gebruiken wint eindpunt terug.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

+++

**Reactie**

Een succesvolle reactie keert status 207 van HTTP met de gevraagde segmentbanen terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor ruimte, slechts tonend gedeeltelijke details van elke segmentbaan. De volledige reactie zal de volledige details voor de gevraagde segmentbanen vermelden.

+++ Een monsterreactie bij gebruik van de bulkreacties.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
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
| `status` | De huidige status voor de segmenttaak. Mogelijke waarden voor de status zijn &#39;NEW&#39;, &#39;PROCESSING&#39;, &#39;CANCELING&#39;, &#39;CANCELED&#39;, &#39;FAILED&#39; en &#39;SUCCED&#39;. |
| `segments` | Een voorwerp dat informatie over de segmentdefinities bevat die binnen de segmentbaan zijn teruggekeerd. |
| `segments.segment.id` | De id van de segmentdefinitie. |
| `segments.segment.expression` | Een object dat informatie bevat over de expressie van de segmentdefinitie, geschreven in PQL. |

+++

## Een specifieke segmenttaak annuleren of verwijderen {#delete}

U kunt een specifieke segmentbaan schrappen door een DELETE- verzoek aan het `/segment/jobs` eindpunt te doen en identiteitskaart van de segmentbaan te verstrekken u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>De API-reactie op de verwijderaanvraag is onmiddellijk. Nochtans, is de daadwerkelijke schrapping van de segmentbaan asynchroon. Met andere woorden, er is een tijdverschil tussen wanneer het schrappingsverzoek aan de segmentbaan wordt gemaakt en wanneer het wordt toegepast.

**API formaat**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | De `id` -waarde van de segmenttaak die u wilt verwijderen. |

**Verzoek**

+++ Een voorbeeldverzoek om een segmenttaak te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 204 met een lege response body.

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de segmentbanen werken.
