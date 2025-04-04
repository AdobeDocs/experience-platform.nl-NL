---
keywords: Experience Platform;home;populaire onderwerpen;monitor dataflows;flow service api;Flow Service
solution: Experience Platform
title: Brongegevens controleren met behulp van de Flow Service API
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens voor stroomuitvoering op volledigheid, fouten en metriek met behulp van de Flow Service API.
exl-id: 5b7d1aa4-5e6d-48f4-82bd-5348dc0e890d
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Bronnen controleren met behulp van de Flow Service API

Dit leerprogramma behandelt de stappen voor de gegevens van de controlestroom in werking stellen voor volledigheid, fouten, en metriek gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Voor deze zelfstudie moet u beschikken over de id-waarde van een geldige gegevensstroom. Als u geen geldige dataflow identiteitskaart hebt, selecteer uw schakelaar van keus van het [ overzicht van bronnen ](../../home.md) en volg de stappen die worden geschetst om een dataflow tot stand te brengen alvorens dit leerprogramma te proberen.

## Aan de slag

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../landing/api-guide.md).

## Dataflows bewaken

Als u de status van uw gegevensstroom wilt zien, vraagt u een GET-aanvraag naar de [!DNL Flow Service] API en geeft u de overeenkomstige stroom-id van uw gegevensstroom op.

**API formaat**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de gegevensstroom die u wilt controleren. |

**Verzoek**

Het volgende verzoek wint de specificaties voor een bestaande gegevensstroom terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert details betreffende uw stroomlooppas, met inbegrip van informatie over zijn aanmaakdatum, bron en doelverbindingen, evenals uniek herkenningsteken van de stroomlooppas (`id`) terug.

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "c9cef9cb-c934-4467-8ef9-cbc934546741",
            "etag": "\"b8003af1-0000-0200-0000-5f2b09f10000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `items` | Bevat één enkele lading meta-gegevens verbonden aan uw specifieke stroomlooppas. |
| `metrics` | Bepaalt kenmerken van de gegevens in de stroomlooppas. |
| `activities` | Hiermee definieert u hoe de gegevens worden getransformeerd. |
| `durationSummary` | Definieert de begin- en eindtijd van de flowuitvoering. |
| `sizeSummary` | Definieert het volume van de gegevens in bytes. |
| `recordSummary` | Hiermee definieert u het recordaantal van de gegevens. |
| `fileSummary` | Hiermee definieert u het aantal bestanden van de gegevens. |
| `statusSummary` | Bepaalt of de stroomlooppas een succes of een mislukking is. |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u metrische gegevens en foutgegevens over uw gegevensstroom opgehaald met de API [!DNL Flow Service] . U kunt nu uw gegevensstroom blijven controleren, afhankelijk van uw innameschema, om zijn status en innamesnelheden te volgen. Voor informatie over hoe te om de zelfde taken uit te voeren gebruikend het gebruikersinterface, zie het leerprogramma op [ controledata gebruikend het gebruikersinterface ](../ui/monitor.md)
