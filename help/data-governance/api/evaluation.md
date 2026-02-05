---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunten voor beleidsevaluatie
description: Zodra de marketing acties zijn gecreeerd en het beleid is bepaald, kunt u de Dienst API van het Beleid gebruiken om te evalueren of om het even welk beleid door bepaalde acties wordt geschonden. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: f8995ff1e460038b0e254cb500a6d23badeaa991
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---

# Eindpunten van de beleidsevaluatie

Nadat u marketingacties hebt gemaakt en beleid voor gegevensgebruik hebt gedefinieerd, kunt u de API van [!DNL Policy Service] gebruiken om te beoordelen of beleidsregels worden overtreden door bepaalde acties. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.

Standaard nemen alleen beleidsregels waarvan de status is ingesteld op `ENABLED` deel aan de evaluatie. U kunt echter de queryparameter `?includeDraft=true` gebruiken om `DRAFT` -beleid op te nemen in een evaluatie.

De evaluatieverzoeken kunnen op drie manieren worden ingediend:

1. Overtreedt de actie, gegeven een marketing actie en een reeks etiketten van het gegevensgebruik, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie en één of meerdere datasets, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie, één of meerdere datasets, en een ondergroep van één of meerdere gebieden binnen elk van die datasets, om het even welk beleid?

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [[!DNL Policy Service]  API ](https://www.adobe.io/experience-platform-apis/references/policy-service/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Evalueren voor beleidsovertredingen met labels voor gegevensgebruik {#labels}

U kunt op beleidsovertredingen evalueren op basis van de aanwezigheid van een specifieke set labels voor gegevensgebruik door de query-parameter `duleLabels` in een GET-aanvraag te gebruiken.

**API formaat**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden getest op basis van een set labels voor gegevensgebruik. U kunt een lijst van beschikbare marketing acties terugwinnen door het verzoek van a [ GET aan het marketing actiepunten ](./marketing-actions.md#list) te doen. |
| `{LABELS_LIST}` | Een door komma&#39;s gescheiden lijst met namen van gegevensgebruikslabels om de marketingactie te testen. Bijvoorbeeld: `duleLabels=C1,C2,C3`<br><br> Merk op dat de etiketnamen case-sensitive zijn. Zorg ervoor dat u het juiste hoofdlettergebruik gebruikt wanneer u deze opsomt in de parameter `duleLabels` . |

**Verzoek**

In het onderstaande voorbeeldverzoek wordt een marketingactie geëvalueerd op de labels C1 en C3.

>[!IMPORTANT]
>
>Let op de operatoren `AND` en `OR` in uw beleidsexpressies. Als een van de labels (`C1` of `C3` ) alleen in het verzoek was weergegeven in het onderstaande voorbeeld, zou de marketingactie dit beleid niet hebben geschonden. Het kost beide labels (`C1` en `C3` ) om het overtreden beleid te retourneren. Zorg ervoor dat u het beleid zorgvuldig evalueert en dat u met gelijke zorg beleidsuitdrukkingen definieert.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie omvat een array `violatedPolicies` met daarin de details van het beleid dat is overtreden als gevolg van het uitvoeren van de marketingactie op de opgegeven labels. Wanneer geen beleid wordt overtreden, is de array `violatedPolicies` leeg.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Evalueren voor beleidsovertredingen die datasets gebruiken {#datasets}

>[!WARNING]
>
>Het `/constraints` eindpunt voor gegevensset-based evaluatie is verouderd. Om beleidsschending te evalueren of veelvoudige evaluatietaken uit te voeren, gebruik [ bulkevaluatie API (`/bulk-eval`) ](#bulk) in plaats daarvan.

U kunt voor beleidsschendingen evalueren die op een reeks van één of meerdere datasets worden gebaseerd waaruit de etiketten van het gegevensgebruik kunnen worden verzameld. Dit wordt gedaan door een POST- verzoek aan het `/constraints` eindpunt voor een specifieke marketing actie uit te voeren en een lijst van dataset IDs binnen het verzoeklichaam te verstrekken.

**API formaat**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The name of the marketing action to test against one or more datasets. U kunt een lijst van beschikbare marketing acties terugwinnen door het verzoek van a [ GET aan het marketing actiepunten ](./marketing-actions.md#list) te doen. |

**Verzoek**

Het volgende verzoek voert de `crossSiteTargeting` marketing actie tegen een reeks drie datasets uit om voor om het even welke beleidsschendingen te evalueren.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | Het type entiteit waarvan de id wordt aangegeven in de eigenschap sibling `entityId` . Momenteel is de enige toegestane waarde `dataSet` . |
| `entityId` | De id van een dataset om de marketingactie tegen te testen. Een lijst met gegevenssets en de bijbehorende id&#39;s kunt u verkrijgen door een GET-aanvraag in te dienen bij het eindpunt `/dataSets` in de [!DNL Catalog Service] API. Zie de gids op [ van de lijst  [!DNL Catalog]  voorwerpen ](../../catalog/api/list-objects.md) voor meer informatie. |

**Reactie**

Een geslaagde reactie omvat een array `violatedPolicies` die de details bevat van het beleid dat is overtreden als gevolg van het uitvoeren van de marketingactie op basis van de opgegeven datasets. Wanneer geen beleid wordt overtreden, is de array `violatedPolicies` leeg.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | Het reactieobject bevat een array `duleLabels` die een geconsolideerde lijst bevat met alle labels die worden gevonden in de opgegeven datasets. Deze lijst omvat dataset en gebied-vlakke etiketten op alle gebieden binnen de dataset. |
| `discoveredLabels` | De reactie omvat ook een `discoveredLabels` -array met objecten voor elke gegevensset, met daarin `datasetLabels` opgedeeld in labels op gegevensset- en veldniveau. Op elk label op veldniveau wordt het pad naar het specifieke veld met dat label weergegeven. |

## Evalueren voor beleidsovertredingen die specifieke datasetgebieden gebruiken {#fields}

U kunt overtredingen van het beleid evalueren die op een ondergroep van gebieden van binnen één of meerdere datasets worden gebaseerd, zodat slechts de etiketten van het gegevensgebruik die die gebieden worden toegepast worden geëvalueerd.

Houd rekening met het volgende wanneer u beleid beoordeelt met gegevenssetvelden:

* **de namen van het Gebied zijn gevoelig geval**: Wanneer het verstrekken van gebieden, moeten zij precies worden geschreven zoals zij in de dataset (bijvoorbeeld, `firstName` vs `firstname`) verschijnen.
* **het etiketovererving van de Dataset**: De individuele gebieden in een dataset erven om het even welke etiketten over die op het datasetniveau zijn toegepast. Als uw beleidsevaluaties niet zoals verwacht terugkeren, ben zeker om het even welke etiketten te controleren die van het datasetniveau tot gebieden kunnen zijn geërft, naast die toegepast op het gebiedsniveau.

**API formaat**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden uitgevoerd op basis van een subset met gegevenssetvelden. U kunt een lijst van beschikbare marketing acties terugwinnen door het verzoek van a [ GET aan het marketing actiepunten ](./marketing-actions.md#list) te doen. |

**Verzoek**

In het volgende verzoek wordt de marketingactie `crossSiteTargeting` getest voor een specifieke set velden die tot drie gegevenssets behoren. De nuttige lading is gelijkaardig aan een [ evaluatieverzoek die slechts datasets ](#datasets) impliceert, toevoegend specifieke gebieden voor elke dataset om etiketten van te verzamelen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | Het type entiteit waarvan de id wordt aangegeven in de eigenschap sibling `entityId` . Momenteel is de enige toegestane waarde `dataSet` . |
| `entityId` | De id van een dataset waarvan gebieden tegen de marketing actie moeten worden geëvalueerd. Een lijst met gegevenssets en de bijbehorende id&#39;s kunt u verkrijgen door een GET-aanvraag in te dienen bij het eindpunt `/dataSets` in de [!DNL Catalog Service] API. Zie de gids op [ van de lijst  [!DNL Catalog]  voorwerpen ](../../catalog/api/list-objects.md) voor meer informatie. |
| `entityMeta.fields` | Een array van paden naar specifieke velden binnen het schema van de gegevensset, opgegeven in de vorm van JSON-aanwijzertekenreeksen. Zie de sectie op [ Aanwijzer JSON ](../../landing/api-fundamentals.md#json-pointer) in de API grondbeginselen gids voor details op de toegelaten syntaxis voor deze koorden. |

**Reactie**

Een geslaagde reactie omvat een array `violatedPolicies` die de details bevat van het beleid dat is overtreden als gevolg van het uitvoeren van de marketingactie op de opgegeven gegevenssetvelden. Wanneer geen beleid wordt overtreden, is de array `violatedPolicies` leeg.

Vergelijkend de voorbeeldreactie hieronder aan de [ reactie die slechts datasets ](#datasets) impliceert, merk op dat de lijst van verzamelde etiketten korter is. De waarde `discoveredLabels` voor elke gegevensset is ook verminderd, omdat deze alleen de velden bevat die zijn opgegeven in de aanvraaginstantie. Bovendien vereist het eerder overtreden beleid `Targeting Ads or Content` dat beide `C4 AND C6` -labels aanwezig zijn en wordt deze daarom niet meer overtreden, zoals wordt aangegeven door de lege `violatedPolicies` -array.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

Met het `/bulk-eval` -eindpunt kunt u meerdere evaluatietaken uitvoeren in één API-aanroep.

**API formaat**

```http
POST /bulk-eval
```

**Verzoek**

De lading van een bulkevaluatieverzoek zou een serie van voorwerpen moeten zijn; voor elke uit te voeren evaluatietaak. Voor taken die worden geëvalueerd op basis van gegevenssets en velden, moet een `entityList` -array worden opgegeven. Voor taken die worden geëvalueerd op basis van labels voor gegevensgebruik, moet een `labels` -array worden opgegeven.

>[!WARNING]
>
>Als een vermelde evaluatietaak zowel een array `entityList` als een array `labels` bevat, treedt er een fout op. Als u dezelfde marketingactie wilt evalueren op basis van zowel gegevenssets als labels, moet u afzonderlijke evaluatietaken voor die marketingactie opnemen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `includeDraft` | Door gebrek, slechts neemt het toegelaten beleid aan evaluatie deel. Als `includeDraft` is ingesteld op `true` , wordt ook deelgenomen aan beleid dat de status `DRAFT` heeft. |
| `labels` | Een array met labels voor gegevensgebruik waarmee de marketingactie wordt getest.<br><br>**BELANGRIJK**: Wanneer het gebruiken van dit bezit, moet een `entityList` bezit NIET in het zelfde voorwerp worden omvat. Als u dezelfde marketingactie wilt evalueren met behulp van gegevenssets en/of velden, moet u een afzonderlijk object in de aanvraaglading opnemen dat een array `entityList` bevat. |
| `entityList` | Een serie van datasets en (facultatief) specifieke gebieden binnen die datasets om de marketing actie tegen te testen.<br><br>**BELANGRIJK**: Wanneer het gebruiken van dit bezit, moet een `labels` bezit NIET in het zelfde voorwerp worden omvat. Als u dezelfde marketingactie wilt evalueren met gebruik van specifieke labels voor gegevensgebruik, moet u een afzonderlijk object in de payload van de aanvraag opnemen dat een array `labels` bevat. |
| `entityType` | Het type entiteit waarop de marketingactie moet worden getest. Momenteel wordt alleen `dataSet` ondersteund. |
| `entityId` | De id van een dataset om de marketingactie tegen te testen. |
| `entityMeta.fields` | (Optioneel) Een lijst met specifieke velden in de gegevensset waarop de marketingactie moet worden getest. |

**Reactie**

Een succesvolle reactie keert een serie van evaluatieresultaten terug; voor elke baan van de beleidsevaluatie die in het verzoek wordt verzonden.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
          "imsOrg": "{ORG_ID}",
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

## Beleidsevaluatie voor [!DNL Real-Time Customer Profile]

De API van [!DNL Policy Service] kan ook worden gebruikt om te controleren op beleidsovertredingen waarbij [!DNL Real-Time Customer Profile] -segmenten worden gebruikt. Zie het leerprogramma op [ afdwingend de naleving van het gegevensgebruik voor publiekssegmenten ](../../segmentation/tutorials/governance.md) voor meer informatie.
