---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beleid
topic: developer guide
translation-type: tm+mt
source-git-commit: 2997243622a7483ae23e21487128cea6badecb80

---


# Beleidsevaluatie

Zodra de marketing acties zijn gecreeerd en het beleid is bepaald, kunt u de Dienst API van het Beleid gebruiken om te evalueren of om het even welk beleid door bepaalde acties wordt geschonden. De geretourneerde beperkingen hebben de vorm van een reeks beleidsregels die worden overtreden door de marketingactie te proberen voor de opgegeven gegevens die labels voor gegevensgebruik bevatten.

Door gebrek, **slechts neemt het beleid de waarvan status aan &quot;TOEGELATEN&quot;aan evaluatie** wordt geplaatst deel, nochtans kunt u de vraagparameter gebruiken `?includeDraft=true` om &quot;CONCEPT&quot;beleid in evaluatie te omvatten.

De evaluatieverzoeken kunnen op drie manieren worden ingediend:

1. Overtreedt de actie, gegeven een reeks etiketten van het gegevensgebruik en een marketing actie, om het even welk beleid?
1. Schendt de actie, gezien één of meerdere datasets en een marketing actie, om het even welk beleid?
1. Schendt de actie, gegeven één of meerdere datasets en een ondergroep van één of meerdere gebieden binnen elk van die datasets, om het even welk beleid?

## Beleid evalueren met labels voor gegevensgebruik en een marketingactie

Als u beleidsovertredingen wilt evalueren op basis van de aanwezigheid van labels voor gegevensgebruik, moet u de set labels opgeven die tijdens het verzoek op de gegevens aanwezig zou zijn. Dit wordt gedaan door het gebruik van vraagparameters, waar de etiketten van het gegevensgebruik als komma-gescheiden lijst van waarden, zoals aangetoond in het volgende voorbeeld worden verstrekt.

**API-indeling**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Verzoek**

In het onderstaande voorbeeldverzoek wordt een marketingactie geëvalueerd op de labels C1 en C3. Houd rekening met het volgende wanneer u beleid evalueert met labels voor gegevensgebruik:
* **Labels voor gegevensgebruik zijn hoofdlettergevoelig.** Het hierboven getoonde verzoek keert een geschonden beleid terug, terwijl het doen van het zelfde verzoek gebruikend kleine letters etiketten (b.v. `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) niet.
* **Let op de`AND`en`OR`operatoren in uw beleidsexpressies.** In dit voorbeeld, als één van beide etiket (`C1` of `C3`) in het verzoek alleen verscheen, zou de marketing actie dit beleid niet geschonden hebben. Beide labels (`C1 AND C3`) zijn nodig om het overtreden beleid te retourneren. Zorg ervoor dat u het beleid zorgvuldig evalueert en dat u met gelijke zorg beleidsuitdrukkingen definieert.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject bevat een `duleLabels` array die moet overeenkomen met de labels die in de aanvraag worden verzonden. Als het uitvoeren van de opgegeven marketingactie op de labels voor gegevensgebruik een beleid schendt, bevat de `violatedPolicies` array de details van het beleid (of het beleid) waarop deze betrekking heeft. Als geen beleid wordt overtreden, zal de `violatedPolicies` serie leeg (`[]`) verschijnen.

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

## Beleid evalueren met behulp van gegevenssets en een marketingactie

U kunt beleidsschendingen ook evalueren door identiteitskaart van één of meerdere datasets te specificeren waarvan de etiketten van het gegevensgebruik kunnen worden verzameld. Dit wordt gedaan door een verzoek van de POST aan of het kern of douaneeindpunt voor een marketing actie uit te voeren en dataset IDs binnen het verzoeklichaam te specificeren, zoals hieronder getoond. `/constraints`

**API-indeling**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Verzoek**

De aanvraaginstantie bevat een array met een object voor elke id van de gegevensset. Aangezien u een verzoeklichaam verzendt, &quot;Content-Type: application/json&quot;verzoekkopbal wordt vereist, zoals aangetoond in het volgende voorbeeld.

```SHELL
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

**Antwoord**

Het reactieobject bevat een `duleLabels` array die een geconsolideerde lijst bevat met alle labels die worden gevonden in de opgegeven datasets. Deze lijst omvat dataset en gebied-vlakke etiketten op alle gebieden binnen de dataset.

De reactie omvat ook een `discoveredLabels` serie die voorwerpen voor elke dataset bevat, die `datasetLabels` uitgesplitst in dataset en gebied-vlakke etiketten toont. Op elk label op veldniveau wordt het pad naar het specifieke veld met dat label weergegeven.

Als de opgegeven marketingactie een beleid schendt dat betrekking heeft op de `duleLabels` binnen de datasets, bevat de `violatedPolicies` array de details van het beleid (of het beleid) waarop deze actie betrekking heeft. Als geen beleid wordt overtreden, zal de `violatedPolicies` serie leeg (`[]`) verschijnen.

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

## Evalueer beleid gebruikend datasets, gebieden, en een marketing actie

Naast het verstrekken van één of meer dataset-id&#39;s kan ook een subset van velden uit elke dataset worden gespecificeerd, die aangeeft dat alleen de gegevensgebruikslabels op die velden moeten worden geëvalueerd. Net als het POST-verzoek dat alleen gegevenssets betreft, voegt dit verzoek specifieke velden voor elke gegevensset toe aan de aanvraaginstantie.

Houd rekening met het volgende wanneer u beleid beoordeelt met gegevenssetvelden:

* **Veldnamen zijn hoofdlettergevoelig.** Wanneer het verstrekken van gebieden, moeten zij precies worden geschreven zoals zij in de dataset (bijvoorbeeld, `firstName` vs `firstname`) verschijnen.
* **Overerving van gegevenssetlabels.** de etiketten van het gegevensgebruik kunnen op veelvoudige niveaus worden toegepast en onderaan overgeërfd. Als uw beleidsevaluaties niet de manier terugkeren u dacht zij, zeker zijn om de geërfte etiketten van datasets neer aan gebieden naast die te controleren die op het gebiedsniveau worden toegepast.

**API-indeling**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Verzoek**

Het aanvraaglichaam bevat een serie met een voorwerp voor elke dataset ID en de ondergroep van gebieden binnen die dataset die voor evaluatie zou moeten worden gebruikt. Aangezien u een verzoeklichaam verzendt, &quot;Content-Type: application/json&quot;verzoekkopbal wordt vereist, zoals aangetoond in het volgende voorbeeld.

```SHELL
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

**Antwoord**

Het reactieobject bevat een `duleLabels` array die de geconsolideerde lijst met labels bevat die in de opgegeven velden wordt gevonden. Herinner dat dit ook datasetetiketten omvat, aangezien zij neer aan gebieden worden geërft.

Als een beleid wordt geschonden door de gespecificeerde marketing actie op de gegevens op de verstrekte gebieden uit te voeren, zal de `violatedPolicies` serie de details van het beleid (of het beleid) bevatten beïnvloedt. Als geen beleid wordt overtreden, zal de `violatedPolicies` serie leeg (`[]`) verschijnen.

In het antwoord hieronder, kunt u zien dat de lijst van `duleLabels` nu korter is, zoals `discoveredLabels` voor elke dataset aangezien het slechts de gebieden omvat die in het verzoeklichaam worden gespecificeerd. U zult ook opmerken dat het eerder overtreden beleid, &quot;het richten van Advertenties of Inhoud&quot;, beide `C4 AND C6` etiketten vereiste, zodat wordt het niet meer geschonden en de `violatedPolicies` serie lijkt leeg.

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

## Beleidsevaluatie voor realtime klantprofiel

De API van de Dienst van het Beleid kan ook worden gebruikt om beleidsschendingen te controleren die het gebruik van de segmenten van het Profiel van de Klant in real time impliceren. Zie de zelfstudie over het [afdwingen van naleving van gegevensgebruik voor publiekssegmenten](../../segmentation/tutorials/governance.md) voor meer informatie.