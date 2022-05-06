---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer;testen
solution: Experience Platform
title: Beleid voor gegevensgebruik afdwingen met de API voor beleidsservice
topic-legacy: guide
type: Tutorial
description: Zodra u de etiketten van het gegevensgebruik voor uw gegevens hebt gecreeerd, en gebruiksbeleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u de Dienst API van het Beleid gebruiken om te evalueren of een marketing actie die op een dataset of een willekeurige groep etiketten wordt uitgevoerd een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# Beleid voor gegevensgebruik afdwingen met [!DNL Policy Service] API

Als u gegevensgebruikslabels voor uw gegevens hebt gemaakt en gebruiksbeleid hebt gemaakt voor marketingacties tegen deze labels, kunt u de opdracht [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) om te beoordelen of een marketingactie die op een gegevensset of op een willekeurige groep labels wordt uitgevoerd, een schending van het beleid vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.

>[!NOTE]
>
>Standaard worden alleen beleidsregels waarvan de status is ingesteld op `ENABLED` kan deelnemen aan de evaluatie. Om toe te staan `DRAFT` beleid om aan evaluatie deel te nemen, moet u de vraagparameter omvatten `includeDraft=true` in het aanvraagpad.

In dit document worden de volgende stappen beschreven voor het gebruik van de [!DNL Policy Service] API om te controleren op beleidsovertredingen in verschillende scenario&#39;s.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten die betrokken zijn bij het afdwingen van beleidsregels voor gegevensgebruik:

* [Gegevensbeheer](../home.md): Het kader waarbinnen [!DNL Platform] dwingt gegevensgebruiksnaleving af.
   * [Labels voor gegevensgebruik](../labels/overview.md): De etiketten van het gebruik van gegevens worden toegepast op datasets (en/of individuele gebieden binnen die datasets), die beperkingen specificeren voor hoe die gegevens kunnen worden gebruikt.
   * [Beleid voor gegevensgebruik](../policies/overview.md): Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die voor bepaalde reeksen etiketten van het gegevensgebruik worden toegestaan of beperkt.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Lees voordat u deze zelfstudie start de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan te maken [!DNL Policy Service] API, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Evalueren met labels en een marketingactie

U kunt een beleid evalueren door een marketing actie tegen een reeks etiketten van het gegevensgebruik te testen die hypothetisch binnen een dataset aanwezig zouden zijn. Dit gebeurt via het gebruik van het `duleLabels` queryparameter, waarbij labels worden opgegeven als een door komma&#39;s gescheiden lijst met waarden, zoals in het onderstaande voorbeeld wordt getoond.

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

Het volgende verzoek test de `exportToThirdParty` marketingactie tegen etiketten `C1` en `C3`. Omdat het gegevensgebruiksbeleid dat u eerder in deze zelfstudie hebt gemaakt, het `C1` als een van de `deny` de marketingactie moet leiden tot een schending van het beleid.

>[!NOTE]
>
>Labels voor gegevensgebruik zijn hoofdlettergevoelig. Beleidsovertredingen treden alleen op wanneer de labels die in de beleidsuitdrukkingen worden gedefinieerd, exact overeenkomen. In dit voorbeeld wordt een `C1` label zou een schending veroorzaken, terwijl een `c1` label niet.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de URL voor de marketingactie, de gebruikslabels waarop de actie is getest en een lijst met beleidsregels die zijn overtreden als gevolg van het testen van de actie op die labels. In dit voorbeeld wordt het beleid Gegevens exporteren naar derde partij weergegeven in het dialoogvenster `violatedPolicies` array, die aangeeft dat de marketingactie de verwachte beleidsschending heeft veroorzaakt.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Een array met voorbeelden van beleidsregels die zijn overtreden door de marketingactie te testen (opgegeven in `marketingActionRef`) tegen de verstrekte `duleLabels`. |

## Evalueren met gebruik van gegevenssets

U kunt een beleid van het gegevensgebruik evalueren door een marketing actie tegen één of meerdere datasets te testen waarvan de etiketten kunnen worden verzameld. Dit gebeurt door een POST aan te vragen `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` en het verstrekken van dataset IDs binnen het verzoeklichaam, zoals aangetoond in het voorbeeld hieronder.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die is gekoppeld aan het beleid dat u evalueert. |

**Verzoek**

Het volgende verzoek test de `exportToThirdParty` marketingactie tegen drie verschillende datasets. De datasets worden van verwijzingen voorzien door type en identiteitskaart in een serie die in de nuttige lading wordt verstrekt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityMeta.fields` | (Optioneel) Een array van [JSON-aanwijzer](../../landing/api-fundamentals.md#json-pointer) tekenreeksen, die verwijzen naar specifieke velden in het schema van de gegevensset. Als deze array is opgenomen, nemen alleen de velden in de array deel aan de evaluatie. Schema-velden die niet in de array zijn opgenomen, nemen niet deel aan de evaluatie.<br><br>Als dit gebied niet inbegrepen is, zullen alle gebieden binnen het datasetschema in evaluatie worden omvat. |

**Antwoord**

Een succesvolle reactie keert URL voor de marketing actie, de gebruiksetiketten terug die uit de verstrekte datasets werden verzameld, en een lijst van om het even welk beleid dat als resultaat van het testen van de actie tegen die etiketten werd geschonden. In dit voorbeeld wordt het beleid Gegevens exporteren naar derde partij weergegeven in het dialoogvenster `violatedPolicies` array, die aangeeft dat de marketingactie de verwachte beleidsschending heeft veroorzaakt.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Een array met voorbeelden van beleidsregels die zijn overtreden door de marketingactie te testen (opgegeven in `marketingActionRef`) tegen de verstrekte `duleLabels`. |

## Volgende stappen

Door dit document te lezen, hebt u met succes gecontroleerd op beleidsschendingen wanneer het uitvoeren van een marketing actie op een dataset of een reeks etiketten van het gegevensgebruik. Met de gegevens die in API-reacties worden geretourneerd, kunt u protocollen in uw ervaringstoepassing instellen om beleidsovertredingen op de juiste wijze af te dwingen.

Voor informatie over hoe het Platform automatisch beleidshandhaving voor geactiveerde segmenten verstrekt, zie de gids op [automatische handhaving](./auto-enforcement.md).
