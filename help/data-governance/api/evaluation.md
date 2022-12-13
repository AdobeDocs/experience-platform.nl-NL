---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunten voor beleidsevaluatie
topic-legacy: developer guide
description: Zodra de marketing acties zijn gecreeerd en het beleid is bepaald, kunt u de Dienst API van het Beleid gebruiken om te evalueren of om het even welk beleid door bepaalde acties wordt geschonden. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 0%

---

# Eindpunten van de beleidsevaluatie

Nadat u marketingacties hebt gemaakt en beleid voor gegevensgebruik hebt gedefinieerd, kunt u de opdracht [!DNL Policy Service] API om te beoordelen of beleidsregels worden overtreden door bepaalde handelingen. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.

Standaard worden alleen beleidsregels waarvan de status is ingesteld op `ENABLED` deelnemen aan de evaluatie. U kunt echter wel de queryparameter gebruiken `?includeDraft=true` om `DRAFT` evaluatiebeleid.

De evaluatieverzoeken kunnen op drie manieren worden ingediend:

1. Overtreedt de actie, gegeven een marketing actie en een reeks etiketten van het gegevensgebruik, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie en één of meerdere datasets, om het even welk beleid?
1. Schendt de actie, gegeven een marketing actie, één of meerdere datasets, en een ondergroep van één of meerdere gebieden binnen elk van die datasets, om het even welk beleid?

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Evalueren voor beleidsovertredingen met labels voor gegevensgebruik {#labels}

U kunt overtredingen van het beleid evalueren op basis van de aanwezigheid van een specifieke set labels voor gegevensgebruik met de opdracht `duleLabels` queryparameter in een GET-verzoek.

**API-indeling**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden getest op basis van een set labels voor gegevensgebruik. U kunt een lijst met beschikbare marketingacties ophalen door een [Het verzoek van de GET aan het marketing actiepunten](./marketing-actions.md#list). |
| `{LABELS_LIST}` | Een door komma&#39;s gescheiden lijst met namen van gegevensgebruikslabels om de marketingactie te testen. Bijvoorbeeld: `duleLabels=C1,C2,C3`<br><br>Labelnamen zijn hoofdlettergevoelig. Zorg ervoor dat je de juiste kwestie gebruikt wanneer je ze in het menu `duleLabels` parameter. |

**Verzoek**

In het onderstaande voorbeeldverzoek wordt een marketingactie geëvalueerd op de labels C1 en C3.

>[!IMPORTANT]
>
>Wees op de hoogte van de `AND` en `OR` operatoren in uw beleidsexpressies. In het onderstaande voorbeeld, indien een van de`C1` of `C3`) alleen in het verzoek was verschenen, zou de marketingactie dit beleid niet hebben geschonden. Beide labels zijn nodig (`C1` en `C3`) om het geschonden beleid terug te geven. Zorg ervoor dat u het beleid zorgvuldig evalueert en dat u met gelijke zorg beleidsuitdrukkingen definieert.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie omvat een `violatedPolicies` array, die de details bevat van het beleid dat is geschonden als gevolg van het uitvoeren van de marketingactie tegen de opgegeven labels. Als geen beleid wordt geschonden, `violatedPolicies` array is leeg.

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

U kunt voor beleidsschendingen evalueren die op een reeks van één of meerdere datasets worden gebaseerd waaruit de etiketten van het gegevensgebruik kunnen worden verzameld. Dit wordt gedaan door een verzoek van de POST aan uit te voeren `/constraints` eindpunt voor een specifieke marketing actie en het verstrekken van een lijst van dataset IDs binnen het verzoeklichaam.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The name of the marketing action to test against one or more datasets. U kunt een lijst met beschikbare marketingacties ophalen door een [Het verzoek van de GET aan het marketing actiepunten](./marketing-actions.md#list). |

**Verzoek**

Het volgende verzoek voert het `crossSiteTargeting` marketing actie tegen een reeks van drie datasets om voor om het even welke beleidsschendingen te evalueren.

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
| `entityType` | Het type entiteit waarvan de id op de verwant is aangegeven `entityId` eigenschap. Momenteel is de enige toegestane waarde `dataSet`. |
| `entityId` | De id van een dataset om de marketingactie tegen te testen. Een lijst met gegevensbestanden en de bijbehorende id&#39;s kan worden verkregen door een GET-verzoek in te dienen bij de `/dataSets` in de [!DNL Catalog Service] API. Zie de handleiding op [aanbieding [!DNL Catalog] objecten](../../catalog/api/list-objects.md) voor meer informatie . |

**Antwoord**

Een geslaagde reactie omvat een `violatedPolicies` array, die de details bevat van het beleid dat is geschonden als gevolg van het uitvoeren van de marketingactie op basis van de verstrekte datasets. Als geen beleid wordt geschonden, `violatedPolicies` array is leeg.

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
| `duleLabels` | Het reactieobject bevat een `duleLabels` array die een geconsolideerde lijst bevat met alle labels die worden gevonden in de opgegeven datasets. Deze lijst omvat dataset en gebied-vlakke etiketten op alle gebieden binnen de dataset. |
| `discoveredLabels` | Het antwoord bevat ook een `discoveredLabels` array met objecten voor elke gegevensset, weergeven `datasetLabels` uitgesplitst in labels op gegevensniveau en veldniveau. Op elk label op veldniveau wordt het pad naar het specifieke veld met dat label weergegeven. |

## Evalueren voor beleidsovertredingen gebruikend specifieke datasetgebieden {#fields}

U kunt overtredingen van het beleid evalueren die op een ondergroep van gebieden van binnen één of meerdere datasets worden gebaseerd, zodat slechts de etiketten van het gegevensgebruik die die gebieden worden toegepast worden geëvalueerd.

Houd rekening met het volgende wanneer u beleid beoordeelt met gegevenssetvelden:

* **Veldnamen zijn hoofdlettergevoelig**: Wanneer het verstrekken van gebieden, moeten zij precies worden geschreven zoals zij in de dataset verschijnen (bijvoorbeeld `firstName` vs `firstname`).
* **Overerving gegevenssetlabel**: De individuele gebieden in een dataset erven om het even welke etiketten die op het datasetniveau zijn toegepast. Als uw beleidsevaluaties niet zoals verwacht terugkeren, ben zeker om het even welke etiketten te controleren die van het datasetniveau tot gebieden kunnen zijn geërft, naast die toegepast op het gebiedsniveau.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden uitgevoerd op basis van een subset met gegevenssetvelden. U kunt een lijst met beschikbare marketingacties ophalen door een [Het verzoek van de GET aan het marketing actiepunten](./marketing-actions.md#list). |

**Verzoek**

In het volgende verzoek wordt de marketingactie getest `crossSiteTargeting` op een specifieke reeks velden die tot drie gegevensreeksen behoren. De lading is gelijkaardig aan [evaluatieverzoek dat uitsluitend betrekking heeft op gegevensbestanden](#datasets), het toevoegen van specifieke gebieden voor elke dataset om etiketten van te verzamelen.

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
| `entityType` | Het type entiteit waarvan de id op de verwant is aangegeven `entityId` eigenschap. Momenteel is de enige toegestane waarde `dataSet`. |
| `entityId` | De id van een dataset waarvan gebieden tegen de marketing actie moeten worden geëvalueerd. Een lijst met gegevensbestanden en de bijbehorende id&#39;s kan worden verkregen door een GET-verzoek in te dienen bij de `/dataSets` in de [!DNL Catalog Service] API. Zie de handleiding op [aanbieding [!DNL Catalog] objecten](../../catalog/api/list-objects.md) voor meer informatie . |
| `entityMeta.fields` | Een array van paden naar specifieke velden binnen het schema van de gegevensset, opgegeven in de vorm van JSON-aanwijzertekenreeksen. Zie de sectie over [JSON-aanwijzer](../../landing/api-fundamentals.md#json-pointer) in de handleiding voor API-basisbeginselen voor meer informatie over de geaccepteerde syntaxis voor deze tekenreeksen. |

**Antwoord**

Een geslaagde reactie omvat een `violatedPolicies` array, die de details bevat van het beleid dat is geschonden als gevolg van het uitvoeren van de marketingactie tegen de opgegeven gegevenssetvelden. Als geen beleid wordt geschonden, `violatedPolicies` array is leeg.

De voorbeeldreactie hieronder vergelijken met de [reactie met alleen gegevensreeksen](#datasets)De lijst met verzamelde labels is korter. De `discoveredLabels` voor elke dataset zijn ook verminderd, aangezien zij alleen de velden omvatten die in de aanvraaginstantie zijn gespecificeerd. Bovendien heeft het eerder geschonden beleid `Targeting Ads or Content` beide vereist `C4 AND C6` etiketten die worden aangebracht, en daarom niet meer worden geschonden, zoals aangegeven door de lege `violatedPolicies` array.

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

De `/bulk-eval` het eindpunt staat u toe om veelvoudige evaluatietaken in één enkele API vraag in werking te stellen.

**API-indeling**

```http
POST /bulk-eval
```

**Verzoek**

De lading van een bulkevaluatieverzoek zou een serie van voorwerpen moeten zijn; één voor elke uit te voeren evaluatietaak. Voor banen die op datasets en gebieden evalueren, en `entityList` array moet worden opgegeven. Voor taken die worden geëvalueerd op basis van labels voor gegevensgebruik, voert u een `labels` array moet worden opgegeven.

>[!WARNING]
>
>Als een vermelde evaluatietaak zowel een `entityList` en `labels` -array, er treedt een fout op. Als u dezelfde marketingactie wilt evalueren op basis van zowel gegevenssets als labels, moet u afzonderlijke evaluatietaken voor die marketingactie opnemen.

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
| `includeDraft` | Door gebrek, slechts neemt het toegelaten beleid aan evaluatie deel. Indien `includeDraft` is ingesteld op `true`, beleid in `DRAFT` de status zal ook deelnemen . |
| `labels` | Een array met labels voor gegevensgebruik waarmee de marketingactie wordt getest.<br><br>**BELANGRIJK**: Wanneer u deze eigenschap gebruikt, `entityList` eigenschap mag NIET in hetzelfde object worden opgenomen. Als u dezelfde marketingactie wilt evalueren met behulp van gegevenssets en/of velden, moet u een afzonderlijk object in de payload van de aanvraag opnemen dat een `entityList` array. |
| `entityList` | Een serie van datasets en (facultatief) specifieke gebieden binnen die datasets om de marketing actie tegen te testen.<br><br>**BELANGRIJK**: Wanneer u deze eigenschap gebruikt, `labels` eigenschap mag NIET in hetzelfde object worden opgenomen. Als u dezelfde marketingactie wilt evalueren met specifieke labels voor gegevensgebruik, moet u een afzonderlijk object in de payload van de aanvraag opnemen dat een `labels` array. |
| `entityType` | Het type entiteit waarop de marketingactie moet worden getest. Alleen `dataSet` wordt ondersteund. |
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

## Beleidsevaluatie voor [!DNL Real-time Customer Profile]

De [!DNL Policy Service] API kan ook worden gebruikt om te controleren op beleidsovertredingen waarbij het gebruik van [!DNL Real-time Customer Profile] segmenten. Zie de zelfstudie aan [naleving van gegevensgebruik afdwingen voor publiekssegmenten](../../segmentation/tutorials/governance.md) voor meer informatie .
