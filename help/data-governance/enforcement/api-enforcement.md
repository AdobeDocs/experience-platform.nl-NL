---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer;testen
solution: Experience Platform
title: Beleid voor gegevensgebruik afdwingen met de API voor beleidsservice
type: Tutorial
description: Zodra u de etiketten van het gegevensgebruik voor uw gegevens hebt gecreeerd, en gebruiksbeleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u de Dienst API van het Beleid gebruiken om te evalueren of een marketing actie die op een dataset of een willekeurige groep etiketten wordt uitgevoerd een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: f8995ff1e460038b0e254cb500a6d23badeaa991
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# Beleid voor gegevensgebruik afdwingen met de API [!DNL Policy Service]

Zodra u de etiketten van het gegevensgebruik voor uw gegevens hebt gecreeerd, en gebruiksbeleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u [[!DNL Policy Service API] gebruiken &#x200B;](https://www.adobe.io/experience-platform-apis/references/policy-service/) om te evalueren of een marketing actie die op een dataset of een willekeurige groep etiketten wordt uitgevoerd een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie.

>[!NOTE]
>
>Standaard kunnen alleen beleidsregels waarvan de status is ingesteld op `ENABLED` deelnemen aan de evaluatie. Als u wilt toestaan dat `DRAFT` -beleid kan deelnemen aan een evaluatie, moet u de queryparameter `includeDraft=true` opnemen in het aanvraagpad.

Dit document bevat stappen voor het gebruik van de API [!DNL Policy Service] om te controleren op beleidsovertredingen in verschillende scenario&#39;s.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten die betrokken zijn bij het afdwingen van beleidsregels voor gegevensgebruik:

* [&#x200B; Beheer van Gegevens &#x200B;](../home.md): Het kader waardoor [!DNL Experience Platform] naleving van het gegevensgebruik afdwingt.
   * [&#x200B; de gebruiksetiketten van Gegevens &#x200B;](../labels/overview.md): De etiketten van het gebruik van gegevens worden toegepast op datasets (en/of individuele gebieden binnen die datasets), die beperkingen specificeren voor hoe die gegevens kunnen worden gebruikt.
   * [&#x200B; het gebruiksbeleid van Gegevens &#x200B;](../policies/overview.md): Het gebruiksbeleid van gegevens is regels die de soorten marketing acties beschrijven die voor bepaalde reeksen etiketten van het gegevensgebruik worden toegestaan of beperkt.
* [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Alvorens dit leerprogramma te beginnen, te herzien gelieve de [&#x200B; ontwikkelaarsgids &#x200B;](../api/getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan [!DNL Policy Service] API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Evalueren met labels en een marketingactie

U kunt een beleid evalueren door een marketing actie tegen een reeks etiketten van het gegevensgebruik te testen die hypothetisch binnen een dataset aanwezig zouden zijn. Dit wordt gedaan door het gebruik van de `duleLabels` vraagparameter, waar de etiketten als komma-gescheiden lijst van waarden, zoals aangetoond in het hieronder voorbeeld worden verstrekt.

**API formaat**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die is gekoppeld aan het gegevensgebruiksbeleid dat u evalueert. |
| `{LABEL_1}` | Een etiket van het gegevensgebruik om de marketing actie tegen te testen. Er moet ten minste één etiket worden verstrekt. Wanneer u meerdere labels aanbiedt, moeten deze worden gescheiden door komma&#39;s. |

**Verzoek**

In het volgende verzoek wordt de marketingactie `exportToThirdParty` getest op labels `C1` en `C3` . Aangezien het gegevensgebruiksbeleid dat u eerder in deze zelfstudie hebt gemaakt het label `C1` definieert als een van de `deny` -voorwaarden in de beleidsexpressie, moet de marketingactie een beleidsovertreding activeren.

>[!NOTE]
>
>Labels voor gegevensgebruik zijn hoofdlettergevoelig. Beleidsovertredingen treden alleen op wanneer de labels die in de beleidsuitdrukkingen worden gedefinieerd, exact overeenkomen. In dit voorbeeld zou een label van het type `C1` een schending veroorzaken, terwijl een label van het type `c1` dat niet doet.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de URL voor de marketingactie, de gebruikslabels waarop de actie is getest en een lijst met beleidsregels die zijn overtreden als gevolg van het testen van de actie op die labels. In dit voorbeeld wordt het beleid Gegevens exporteren naar derden weergegeven in de array `violatedPolicies` , wat aangeeft dat de marketingactie de verwachte beleidsovertreding heeft veroorzaakt.

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
| `violatedPolicies` | Een array met alle beleidsregels die zijn overtreden door de marketingactie (opgegeven in `marketingActionRef` ) te testen op basis van de opgegeven `duleLabels` . |

## Evalueren met gebruik van gegevenssets

>[!WARNING]
>
>Het `/constraints` eindpunt voor gegevensset-based evaluatie is verouderd. Om beleidsschending te evalueren of veelvoudige evaluatietaken uit te voeren, gebruik [&#x200B; bulkevaluatie API (`/bulk-eval`) &#x200B;](../api/evaluation.md#bulk) in plaats daarvan.

U kunt een beleid van het gegevensgebruik evalueren door een marketing actie tegen één of meerdere datasets te testen waarvan de etiketten kunnen worden verzameld. Dit wordt gedaan door een POST- verzoek aan `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` te doen en dataset IDs binnen het verzoeklichaam, zoals aangetoond in het hieronder voorbeeld te verstrekken.

**API formaat**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die is gekoppeld aan het beleid dat u evalueert. |

**Verzoek**

In het volgende verzoek wordt de marketingactie van `exportToThirdParty` getest op basis van drie verschillende gegevenssets. De datasets worden van verwijzingen voorzien door type en identiteitskaart in een serie die in de nuttige lading wordt verstrekt.

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
| `entityMeta.fields` | (Facultatief) een serie van [&#x200B; koorden van de Aanwijzer 0&rbrace; JSON, die specifieke gebieden in het schema van de dataset van verwijzingen voorzien. &#x200B;](../../landing/api-fundamentals.md#json-pointer) Als deze array is opgenomen, nemen alleen de velden in de array deel aan de evaluatie. Schema-velden die niet in de array zijn opgenomen, nemen niet deel aan de evaluatie.<br><br> als dit gebied niet inbegrepen is, zullen alle gebieden binnen het datasetschema in evaluatie worden omvat. |

**Reactie**

Een succesvolle reactie keert URL voor de marketing actie, de gebruiksetiketten terug die uit de verstrekte datasets werden verzameld, en een lijst van om het even welk beleid dat als resultaat van het testen van de actie tegen die etiketten werd geschonden. In dit voorbeeld wordt het beleid Gegevens exporteren naar derden weergegeven in de array `violatedPolicies` , wat aangeeft dat de marketingactie de verwachte beleidsovertreding heeft veroorzaakt.

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
| `violatedPolicies` | Een array met alle beleidsregels die zijn overtreden door de marketingactie (opgegeven in `marketingActionRef` ) te testen op basis van de opgegeven `duleLabels` . |

## Volgende stappen

Door dit document te lezen, hebt u met succes gecontroleerd op beleidsschendingen wanneer het uitvoeren van een marketing actie op een dataset of een reeks etiketten van het gegevensgebruik. Met de gegevens die in API-reacties worden geretourneerd, kunt u protocollen in uw ervaringstoepassing instellen om beleidsovertredingen op de juiste wijze af te dwingen.

Voor informatie over hoe Experience Platform automatisch beleidshandhaving voor geactiveerde segmenten verstrekt, zie de gids op [&#x200B; automatische handhaving &#x200B;](./auto-enforcement.md).
