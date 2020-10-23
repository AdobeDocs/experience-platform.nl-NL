---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance;testing
solution: Experience Platform
title: Beleid voor gegevensgebruik afdwingen met de API voor beleidsservice
topic: enforcement
type: Tutorial
description: Zodra u de etiketten van het gegevensgebruik voor uw gegevens hebt gecreeerd, en gebruiksbeleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u de Dienst API van het Beleid gebruiken om te evalueren of een marketing actie die op een dataset of een willekeurige groep etiketten wordt uitgevoerd een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.
translation-type: tm+mt
source-git-commit: 00688e271b3c1e3ad1a17ceb6045e3316bd65961
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---


# Beleid voor gegevensgebruik afdwingen met de [!DNL Policy Service] API

Zodra u de etiketten van het gegevensgebruik voor uw gegevens hebt gecreeerd, en gebruiksbeleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u gebruiken [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) om te evalueren of een marketing actie die op een dataset of een willekeurige groep etiketten wordt uitgevoerd een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.

>[!NOTE]
>
>Door gebrek, slechts `ENABLED` kan het beleid waarvan status aan evaluatie wordt geplaatst deelnemen. Om `DRAFT` beleid toe te staan om aan evaluatie deel te nemen, moet u de vraagparameter `includeDraft=true` in de verzoekweg omvatten.

Dit document bevat stappen voor het controleren op beleidsovertredingen in verschillende scenario&#39;s met behulp van de [!DNL Policy Service] API.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten die betrokken zijn bij het afdwingen van beleidsregels voor gegevensgebruik:

* [Gegevensbeheer](../home.md): Het kader waarmee de naleving van het gegevensgebruik wordt [!DNL Platform] afgedwongen.
   * [Labels](../labels/overview.md)voor gegevensgebruik: De etiketten van het gebruik van gegevens worden toegepast op datasets (en/of individuele gebieden binnen die datasets), die beperkingen specificeren voor hoe die gegevens kunnen worden gebruikt.
   * [Beleid](../policies/overview.md)voor gegevensgebruik: Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die voor bepaalde reeksen etiketten van het gegevensgebruik worden toegestaan of beperkt.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voordat u deze zelfstudie start, moet u eerst de [ontwikkelaarsgids](../api/getting-started.md) raadplegen voor belangrijke informatie die u moet weten om oproepen naar de [!DNL Policy Service] API te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Evalueren met labels en een marketingactie

U kunt een beleid evalueren door een marketing actie tegen een reeks etiketten van het gegevensgebruik te testen die hypothetisch binnen een dataset aanwezig zouden zijn. Dit wordt gedaan door het gebruik van de `duleLabels` vraagparameter, waar de etiketten als komma-gescheiden lijst van waarden, zoals aangetoond in het hieronder voorbeeld worden verstrekt.

**API-indeling**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die is gekoppeld aan het gegevensgebruiksbeleid dat u evalueert. |
| `{LABEL_1}` | Een label voor gegevensgebruik waarmee de marketingactie wordt getest. Er moet ten minste één etiket worden verstrekt. Wanneer u meerdere labels aanbiedt, moeten deze worden gescheiden door komma&#39;s. |

**Verzoek**

In het volgende verzoek wordt de `exportToThirdParty` marketingactie getest op labels `C1` en `C3`. Aangezien het gegevensgebruiksbeleid u eerder in deze zelfstudie creeerde het `C1` etiket als één van de `deny` voorwaarden in zijn beleidsuitdrukking definieert, zou de marketing actie een beleidsschending moeten teweegbrengen.

>[!NOTE]
>
>Labels voor gegevensgebruik zijn hoofdlettergevoelig. Beleidsovertredingen treden alleen op wanneer de labels die in de beleidsuitdrukkingen worden gedefinieerd, exact overeenkomen. In dit voorbeeld zou een `C1` label een schending veroorzaken, maar een `c1` label niet.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de URL voor de marketingactie, de gebruikslabels waarop de actie is getest en een lijst met beleidsregels die zijn overtreden als gevolg van het testen van de actie op die labels. In dit voorbeeld wordt het beleid Gegevens exporteren naar derde weergegeven in de `violatedPolicies` array om aan te geven dat de marketingactie de verwachte beleidsschending heeft veroorzaakt.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `violatedPolicies` | Een array met alle beleidsregels die zijn overtreden door de marketingactie (opgegeven in `marketingActionRef`) te testen op basis van de opgegeven actie `duleLabels`. |

## Evalueren met gebruik van gegevenssets

U kunt een beleid van het gegevensgebruik evalueren door een marketing actie tegen één of meerdere datasets te testen waarvan de etiketten kunnen worden verzameld. Dit wordt gedaan door een verzoek van de POST aan `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` en het verstrekken van dataset IDs binnen het verzoeklichaam, zoals aangetoond in het hieronder voorbeeld te doen.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die is gekoppeld aan het beleid dat u evalueert. |

**Verzoek**

Het volgende verzoek test de `exportToThirdParty` marketing actie tegen drie verschillende datasets. De datasets worden van verwijzingen voorzien door type en identiteitskaart in een serie die in de nuttige lading wordt verstrekt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `entityType` | Elk item in de payload-array moet het type entiteit aangeven dat wordt gedefinieerd. Voor dit gebruik is de waarde altijd &quot;dataSet&quot;. |
| `entityId` | Elk punt in de ladingsserie moet unieke identiteitskaart voor een dataset verstrekken. |
| `entityMeta.fields` | (Optioneel) Een array met [JSON-aanwijzertekenreeksen](../../landing/api-fundamentals.md#json-pointer) die verwijzen naar specifieke velden in het schema van de gegevensset. Als deze array is opgenomen, nemen alleen de velden in de array deel aan de evaluatie. Schema-velden die niet in de array zijn opgenomen, nemen niet deel aan de evaluatie.<br><br>Als dit gebied niet inbegrepen is, zullen alle gebieden binnen het datasetschema in evaluatie worden omvat. |

**Antwoord**

Een succesvolle reactie keert URL voor de marketing actie, de gebruiksetiketten terug die uit de verstrekte datasets werden verzameld, en een lijst van om het even welk beleid dat als resultaat van het testen van de actie tegen die etiketten werd geschonden. In dit voorbeeld wordt het beleid Gegevens exporteren naar derde weergegeven in de `violatedPolicies` array om aan te geven dat de marketingactie de verwachte beleidsschending heeft veroorzaakt.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `duleLabels` | Een lijst van de etiketten van het gegevensgebruik die uit de datasets werden gehaald die in de verzoeklading worden verstrekt. |
| `discoveredLabels` | Een lijst van de datasets die in de verzoeklading werden verstrekt, tonend de datasetniveau en gebied-vlakke etiketten die in elk werden gevonden. |
| `violatedPolicies` | Een array met alle beleidsregels die zijn overtreden door de marketingactie (opgegeven in `marketingActionRef`) te testen op basis van de opgegeven actie `duleLabels`. |

## Volgende stappen

Door dit document te lezen, hebt u met succes gecontroleerd op beleidsschendingen wanneer het uitvoeren van een marketing actie op een dataset of een reeks etiketten van het gegevensgebruik. Met de gegevens die in API-reacties worden geretourneerd, kunt u protocollen in uw ervaringstoepassing instellen om beleidsovertredingen op de juiste wijze af te dwingen.

Voor stappen op hoe te om het beleid van het gegevensgebruik voor publiekssegmenten in af te dwingen, gelieve te verwijzen naar het volgende [!DNL Real-time Customer Profile]leerprogramma [](../../segmentation/tutorials/governance.md).