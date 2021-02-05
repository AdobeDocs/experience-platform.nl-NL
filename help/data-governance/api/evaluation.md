---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunten voor beleidsevaluatie
topic: developer guide
description: Zodra de marketing acties zijn gecreeerd en het beleid is bepaald, kunt u de Dienst API van het Beleid gebruiken om te evalueren of om het even welk beleid door bepaalde acties wordt geschonden. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Eindpunten van de beleidsevaluatie

Nadat u marketingacties hebt gemaakt en beleid hebt gedefinieerd, kunt u de [!DNL Policy Service] API gebruiken om te evalueren of een beleid wordt overtreden door bepaalde acties. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.

Door gebrek, slechts neemt het beleid de waarvan status aan `ENABLED` wordt geplaatst aan evaluatie deel. Nochtans, kunt u de vraagparameter `?includeDraft=true` gebruiken om `DRAFT` beleid in evaluatie te omvatten.

De evaluatieverzoeken kunnen op drie manieren worden ingediend:

1. Overtreedt de actie, gegeven een marketing actie en een reeks etiketten van het gegevensgebruik, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie en één of meerdere datasets, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie, één of meerdere datasets, en een ondergroep van één of meerdere gebieden binnen elk van die datasets, om het even welk beleid?

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Evalueren voor beleidsovertredingen met labels voor gegevensgebruik {#labels}

U kunt voor beleidsschendingen evalueren die op de aanwezigheid van een specifieke reeks etiketten van het gegevensgebruik worden gebaseerd door de `duleLabels` vraagparameter in een verzoek van de GET te gebruiken.

**API-indeling**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden getest op basis van een set labels voor gegevensgebruik. U kunt een lijst van beschikbare marketing acties terugwinnen door een [verzoek van de GET aan het marketing actieseindpunt ](./marketing-actions.md#list) te doen. |
| `{LABELS_LIST}` | Een door komma&#39;s gescheiden lijst met namen van gegevensgebruikslabels om de marketingactie te testen. Bijvoorbeeld: `duleLabels=C1,C2,C3`<br><br>Namen van labels zijn hoofdlettergevoelig. Zorg ervoor dat u het juiste geval gebruikt wanneer u hen in de `duleLabels` parameter opsomt. |

**Verzoek**

In het onderstaande voorbeeldverzoek wordt een marketingactie geëvalueerd op de labels C1 en C3.

>[!IMPORTANT]
>
>Houd rekening met de operatoren `AND` en `OR` in uw beleidsexpressies. Als in het onderstaande voorbeeld een label (`C1` of `C3`) alleen in het verzoek was weergegeven, zou de marketingactie dit beleid niet hebben geschonden. Het vergt beide etiketten (`C1` en `C3`) om het geschonden beleid terug te keren. Zorg ervoor dat u het beleid zorgvuldig evalueert en dat u met gelijke zorg beleidsuitdrukkingen definieert.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie omvat een `violatedPolicies` serie, die de details van het beleid bevat die als resultaat van het uitvoeren van de marketing actie tegen de verstrekte etiketten werden overtreden. Als geen beleid wordt overtreden, zal `violatedPolicies` serie leeg zijn.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Evalueren voor beleidsovertredingen met behulp van datasets {#datasets}

U kunt voor beleidsschendingen evalueren die op een reeks van één of meerdere datasets worden gebaseerd waaruit de etiketten van het gegevensgebruik kunnen worden verzameld. Dit wordt gedaan door een verzoek van de POST aan het `/constraints` eindpunt voor een specifieke marketing actie uit te voeren en een lijst van dataset IDs binnen het verzoeklichaam te verstrekken.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The name of the marketing action to test against one or more datasets. U kunt een lijst van beschikbare marketing acties terugwinnen door een [verzoek van de GET aan het marketing actieseindpunt ](./marketing-actions.md#list) te doen. |

**Verzoek**

Het volgende verzoek voert de `crossSiteTargeting` marketing actie tegen een reeks drie datasets uit om voor om het even welke beleidsschendingen te evalueren.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `entityType` | Het type entiteit waarvan id wordt aangegeven in de eigenschap `entityId` op hetzelfde niveau. Momenteel is de enige toegestane waarde `dataSet`. |
| `entityId` | De id van een dataset om de marketingactie tegen te testen. Een lijst van datasets en hun overeenkomstige IDs kan worden verkregen door een verzoek van de GET aan het `/dataSets` eindpunt in [!DNL Catalog Service] API te richten. Zie de handleiding bij [vermelding [!DNL Catalog] objecten](../../catalog/api/list-objects.md) voor meer informatie. |

**Antwoord**

Een succesvolle reactie omvat een `violatedPolicies` serie, die de details van het beleid bevat die als resultaat van het uitvoeren van de marketing actie tegen de verstrekte datasets werden geschonden. Als geen beleid wordt overtreden, zal `violatedPolicies` serie leeg zijn.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `duleLabels` | Het reactieobject bevat een `duleLabels`-array die een geconsolideerde lijst bevat met alle labels die worden gevonden in de opgegeven datasets. Deze lijst omvat dataset en gebied-vlakke etiketten op alle gebieden binnen de dataset. |
| `discoveredLabels` | De reactie omvat ook een `discoveredLabels` serie die voorwerpen voor elke dataset bevat, die `datasetLabels` in dataset en gebied-vlakke etiketten uitgesplitst tonen. Op elk label op veldniveau wordt het pad naar het specifieke veld met dat label weergegeven. |

## Evalueren voor beleidsovertredingen die specifieke datasetgebieden {#fields} gebruiken

U kunt overtredingen van het beleid evalueren die op een ondergroep van gebieden van binnen één of meerdere datasets worden gebaseerd, zodat slechts de etiketten van het gegevensgebruik die die gebieden worden toegepast worden geëvalueerd.

Houd rekening met het volgende wanneer u beleid beoordeelt met gegevenssetvelden:

* **Veldnamen zijn hoofdlettergevoelig**: Wanneer het verstrekken van gebieden, moeten zij precies worden geschreven zoals zij in de dataset (bijvoorbeeld,  `firstName` vs  `firstname`) verschijnen.
* **Overerving** van datumlabel: De individuele gebieden in een dataset erven om het even welke etiketten die op het datasetniveau zijn toegepast. Als uw beleidsevaluaties niet zoals verwacht terugkeren, ben zeker om het even welke etiketten te controleren die van het datasetniveau tot gebieden kunnen zijn geërft, naast die toegepast op het gebiedsniveau.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden uitgevoerd op basis van een subset met gegevenssetvelden. U kunt een lijst van beschikbare marketing acties terugwinnen door een [verzoek van de GET aan het marketing actieseindpunt ](./marketing-actions.md#list) te doen. |

**Verzoek**

In het volgende verzoek wordt de marketingactie `crossSiteTargeting` getest op een specifieke set velden die tot drie gegevenssets behoren. De nuttige lading is gelijkaardig aan een [evaluatieverzoek die slechts datasets](#datasets) impliceert, toevoegend specifieke gebieden voor elke dataset om etiketten van te verzamelen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `entityType` | Het type entiteit waarvan id wordt aangegeven in de eigenschap `entityId` op hetzelfde niveau. Momenteel is de enige toegestane waarde `dataSet`. |
| `entityId` | De id van een dataset waarvan gebieden tegen de marketing actie moeten worden geëvalueerd. Een lijst van datasets en hun overeenkomstige IDs kan worden verkregen door een verzoek van de GET aan het `/dataSets` eindpunt in [!DNL Catalog Service] API te richten. Zie de handleiding bij [vermelding [!DNL Catalog] objecten](../../catalog/api/list-objects.md) voor meer informatie. |
| `entityMeta.fields` | Een array van paden naar specifieke velden binnen het schema van de gegevensset, opgegeven in de vorm van JSON-aanwijzertekenreeksen. Zie de sectie over [JSON-aanwijzer](../../landing/api-fundamentals.md#json-pointer) in de handleiding voor API-basisbeginselen voor meer informatie over de geaccepteerde syntaxis voor deze tekenreeksen. |

**Antwoord**

Een succesvolle reactie omvat een `violatedPolicies` serie, die de details van het beleid bevat dat als resultaat van het uitvoeren van de marketing actie tegen de verstrekte datasetgebieden werd geschonden. Als geen beleid wordt overtreden, zal `violatedPolicies` serie leeg zijn.

Wanneer u de voorbeeldreactie hieronder vergelijkt met de [reactie waarbij alleen datasets](#datasets) betrokken zijn, ziet u dat de lijst met verzamelde labels korter is. De `discoveredLabels` voor elke dataset is ook verminderd, aangezien zij slechts de gebieden omvatten die in het verzoeklichaam worden gespecificeerd. Daarnaast vereist het eerder overtreden beleid `Targeting Ads or Content` dat beide `C4 AND C6` labels aanwezig zijn en wordt daarom niet meer overtreden, zoals aangegeven door de lege `violatedPolicies` array.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Beleid bulksgewijs evalueren {#bulk}

Het `/bulk-eval` eindpunt staat u toe om veelvoudige evaluatietaken in één enkele API vraag in werking te stellen.

**API-indeling**

```http
POST /bulk-eval
```

**Verzoek**

De lading van een bulkevaluatieverzoek zou een serie van voorwerpen moeten zijn; één voor elke uit te voeren evaluatietaak. Voor banen die op datasets en gebieden evalueren, moet een `entityList` serie worden verstrekt. Voor taken die worden geëvalueerd op basis van labels voor gegevensgebruik, moet een `labels`-array worden opgegeven.

>[!WARNING]
>
>Als een vermelde evaluatietaak zowel een `entityList` als een `labels` array bevat, zal een fout resulteren. Als u dezelfde marketingactie wilt evalueren op basis van zowel gegevenssets als labels, moet u afzonderlijke evaluatietaken voor die marketingactie opnemen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `evalRef` | De URI van de marketingactie voor het testen op labels of gegevenssets voor beleidsovertredingen. |
| `includeDraft` | Door gebrek, slechts neemt het toegelaten beleid aan evaluatie deel. Als `includeDraft` wordt geplaatst aan `true`, zal het beleid dat in `DRAFT` status is ook deelnemen. |
| `labels` | Een array met labels voor gegevensgebruik waarmee de marketingactie wordt getest.<br><br>**BELANGRIJK**: Wanneer u deze eigenschap gebruikt, mag een  `entityList` eigenschap NIET in hetzelfde object worden opgenomen. Als u dezelfde marketingactie wilt evalueren met behulp van gegevenssets en/of velden, moet u een afzonderlijk object in de aanvraaglading opnemen dat een `entityList`-array bevat. |
| `entityList` | Een serie van datasets en (facultatief) specifieke gebieden binnen die datasets om de marketing actie tegen te testen.<br><br>**BELANGRIJK**: Wanneer u deze eigenschap gebruikt, mag een  `labels` eigenschap NIET in hetzelfde object worden opgenomen. Als u dezelfde marketingactie wilt evalueren met gebruik van specifieke labels voor gegevensgebruik, moet u een afzonderlijk object in de payload van de aanvraag opnemen dat een `labels`-array bevat. |
| `entityType` | Het type entiteit waarop de marketingactie moet worden getest. Momenteel wordt alleen `dataSet` ondersteund. |
| `entityId` | De id van een dataset om de marketingactie tegen te testen. |
| `entityMeta.fields` | (Optioneel) Een lijst met specifieke velden in de gegevensset waarop de marketingactie moet worden getest. |

**Antwoord**

Een succesvolle reactie retourneert een array met evaluatieresultaten. één voor elke beleidsevaluatietaak die in het verzoek wordt verzonden.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Beleidsevaluatie voor [!DNL Real-time Customer Profile]

De [!DNL Policy Service] API kan ook worden gebruikt om beleidsschendingen te controleren die het gebruik van [!DNL Real-time Customer Profile] segmenten impliceren. Zie de zelfstudie over [naleving van gegevensgebruik afdwingen voor publiekssegmenten](../../segmentation/tutorials/governance.md) voor meer informatie.