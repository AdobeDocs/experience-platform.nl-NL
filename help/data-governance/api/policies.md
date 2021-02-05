---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunt voor beleidsregels
topic: developer guide
description: Het beleid van het gebruik van gegevens is regels uw organisatie goedkeurt die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen Experience Platform mag uitvoeren. Het /policies eindpunt wordt gebruikt voor alle API vraag met betrekking tot het bekijken van, het creëren van, het bijwerken van, of het schrappen van het beleid van het gegevensgebruik.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 0%

---


# Eind beleid

Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform]. Het `/policies` eindpunt in [!DNL Policy Service API] staat u toe om het beleid van het gegevensgebruik voor uw organisatie programmatically te beheren.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Hiermee wordt een lijst met beleidsregels {#list} opgehaald

U kunt alle `core` of `custom` beleid door een verzoek van de GET aan `/policies/core` of `/policies/custom`, respectievelijk te richten.

**API-indeling**

```http
GET /policies/core
GET /policies/custom
```

**Verzoek**

Het volgende verzoek wint een lijst van douanebeleid terug dat door uw organisatie wordt bepaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie omvat een `children` serie die van de details van elk teruggewonnen beleid, met inbegrip van hun `id` waarden een lijst maakt. Met het veld `id` van een bepaald beleid kunt u [lookup](#lookup), [update](#update) en [delete](#delete) verzoeken voor dat beleid uitvoeren.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Eigenschap | Beschrijving |
| --- | --- |
| `_page.count` | Het totale aantal opgehaalde beleidsregels. |
| `name` | De weergavenaam voor een beleid. |
| `status` | De huidige status van een beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED`. Standaard nemen alleen `ENABLED`-beleidsregels deel aan de evaluatie. Zie het overzicht op [beleidsevaluatie](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array die de URI&#39;s van alle toepasselijke marketingacties voor een beleid opsomt. |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | Een voorwerp dat de specifieke etiketten van het gegevensgebruik beschrijft dat de bijbehorende het op de markt brengen actie van een beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [het creëren van een beleid](#create-policy) voor meer informatie over dit bezit. |

## Een beleid opzoeken {#look-up}

U kunt omhoog een specifiek beleid kijken door het `id` bezit van dat beleid in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` van het beleid u omhoog wilt kijken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord geeft de details van het beleid terug.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De weergavenaam voor het beleid. |
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED`. Standaard nemen alleen `ENABLED`-beleidsregels deel aan de evaluatie. Zie het overzicht op [beleidsevaluatie](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array die de URI&#39;s van alle toepasselijke marketingacties voor het beleid opsomt. |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | Een voorwerp dat de specifieke etiketten van het gegevensgebruik beschrijft dat de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [het creëren van een beleid](#create-policy) voor meer informatie over dit bezit. |

## Een aangepast beleid maken {#create-policy}

In de [!DNL Policy Service] API, wordt een beleid bepaald door het volgende:

* Een verwijzing naar een specifieke marketingactie
* Een uitdrukking die de etiketten van het gegevensgebruik beschrijft dat de marketing actie tegen wordt beperkt wordt uitgevoerd

Om aan dit laatste vereiste te voldoen, moeten beleidsdefinities een booleaanse uitdrukking betreffende de aanwezigheid van gegevensgebruikslabels omvatten. Deze uitdrukking wordt genoemd een beleidsuitdrukking.

Beleidsexpressies worden gegeven in de vorm van een eigenschap `deny` binnen elke beleidsdefinitie. Een voorbeeld van een eenvoudig object `deny` dat alleen de aanwezigheid van één label controleert, ziet er als volgt uit:

```json
"deny": {
    "label": "C1"
}
```

In veel beleidsregels worden echter complexere voorwaarden met betrekking tot de aanwezigheid van labels voor gegevensgebruik vastgelegd. Om deze gebruiksgevallen te steunen, kunt u booleaanse verrichtingen ook omvatten om uw beleidsuitdrukkingen te beschrijven. Het beleidsexpressieobject moet een label of een operator en operanden bevatten, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject.

Bijvoorbeeld, om een beleid te bepalen dat een marketing actie verbiedt wordt uitgevoerd op gegevens waar `C1 OR (C3 AND C7)` etiketten aanwezig zijn, zou het `deny` bezit van het beleid als worden gespecificeerd:

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `operator` | Geeft de voorwaardelijke relatie aan tussen de labels in de verwant `operands`-array. Accepteerde waarden zijn: <ul><li>`OR`: De expressie wordt omgezet in true als een van de labels in de  `operands` array aanwezig is.</li><li>`AND`: De expressie wordt alleen omgezet in true als alle labels in de  `operands` array aanwezig zijn.</li></ul> |
| `operands` | Een array van objecten, waarbij elk object één label of een extra paar `operator`- en `operands`-eigenschappen vertegenwoordigt. De aanwezigheid van de labels en/of bewerkingen in een `operands`-array wordt omgezet in true of false op basis van de waarde van de eigenschap `operator` op hetzelfde niveau. |
| `label` | De naam van één gegevensgebruikslabel dat op het beleid van toepassing is. |

U kunt een nieuw douanebeleid tot stand brengen door een verzoek van de POST aan het `/policies/custom` eindpunt te doen.

**API-indeling**

```http
POST /policies/custom
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw beleid dat de marketing actie `exportToThirdParty` van wordt uitgevoerd op gegevens die etiketten `C1 OR (C3 AND C7)` bevatten beperkt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De weergavenaam voor het beleid. |
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED`. Standaard nemen alleen `ENABLED`-beleidsregels deel aan de evaluatie. Zie het overzicht op [beleidsevaluatie](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array die de URI&#39;s van alle toepasselijke marketingacties voor het beleid opsomt. De URI voor een marketingactie wordt gegeven onder `_links.self.href` in de reactie voor [het opzoeken van een marketingactie](./marketing-actions.md#look-up). |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | De beleidsuitdrukking die de specifieke etiketten van het gegevensgebruik beschrijft de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe beleid, inclusief `id`. Deze waarde is alleen-lezen en wordt automatisch toegewezen wanneer het beleid wordt gemaakt.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een aangepast beleid {#update} bijwerken

>[!IMPORTANT]
>
>U kunt alleen aangepast beleid bijwerken. Als u kernbeleid wilt toelaten of onbruikbaar maken, zie de sectie op [het bijwerken van de lijst van toegelaten kernbeleid](#update-enabled-core).

U kunt een bestaand douanebeleid bijwerken door zijn identiteitskaart in de weg van een verzoek van de PUT met een nuttige lading te verstrekken die de bijgewerkte vorm van het beleid in zijn geheel omvat. Met andere woorden, het verzoek van de PUT herschrijft in wezen het beleid.

>[!NOTE]
>
>Zie de sectie over [het bijwerken van een gedeelte van een douanebeleid](#patch) als u slechts één of meerdere gebieden voor een beleid wilt bijwerken, eerder dan het te beschrijven.

**API-indeling**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` van het beleid u wilt bijwerken. |

**Verzoek**

In dit voorbeeld zijn de voorwaarden voor het exporteren van gegevens naar een derde gewijzigd en nu hebt u het beleid nodig dat u hebt gemaakt om deze marketingactie te weigeren als er `C1 AND C5` gegevenslabels aanwezig zijn.

Het volgende verzoek werkt het bestaande beleid bij om de nieuwe beleidsuitdrukking te omvatten. Merk op dat aangezien dit verzoek hoofdzakelijk het beleid herschrijft, alle gebieden in de lading moeten worden omvat, zelfs als sommige van hun waarden niet worden bijgewerkt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De weergavenaam voor het beleid. |
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED`. Standaard nemen alleen `ENABLED`-beleidsregels deel aan de evaluatie. Zie het overzicht op [beleidsevaluatie](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array die de URI&#39;s van alle toepasselijke marketingacties voor het beleid opsomt. De URI voor een marketingactie wordt gegeven onder `_links.self.href` in de reactie voor [het opzoeken van een marketingactie](./marketing-actions.md#look-up). |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | De beleidsuitdrukking die de specifieke etiketten van het gegevensgebruik beschrijft de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [het creëren van een beleid](#create-policy) voor meer informatie over dit bezit. |

**Antwoord**

Een succesvolle reactie keert de details van het bijgewerkte beleid terug.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een gedeelte van een aangepast beleid {#patch} bijwerken

>[!IMPORTANT]
>
>U kunt alleen aangepast beleid bijwerken. Als u kernbeleid wilt toelaten of onbruikbaar maken, zie de sectie op [het bijwerken van de lijst van toegelaten kernbeleid](#update-enabled-core).

Een specifiek gedeelte van een beleid kan worden bijgewerkt gebruikend een verzoek van de PATCH. In tegenstelling tot de verzoeken van de PUT die het beleid herschrijven, werken de verzoeken van PATCH slechts de eigenschappen bij die in het verzoeklichaam worden gespecificeerd. Dit is vooral nuttig wanneer u een beleid wilt toelaten of onbruikbaar maken, aangezien u slechts de weg aan het aangewezen bezit (`/status`) en zijn waarde (`ENABLED` of `DISABLED`) moet verstrekken.

>[!NOTE]
>
>Voor PATCH-aanvragen worden de JSON Patch-opmaak gebruikt. Zie de [handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md) voor meer informatie over de geaccepteerde syntaxis.

De [!DNL Policy Service] API steunt de verrichtingen `add`, `remove`, en `replace`, en staat u toe om verscheidene updates samen in één enkele vraag te combineren, zoals aangetoond in het hieronder voorbeeld.

**API-indeling**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` van het beleid waarvan eigenschappen u wilt bijwerken. |

**Verzoek**

In het volgende verzoek worden twee `replace`-bewerkingen gebruikt om de beleidsstatus te wijzigen van `DRAFT` in `ENABLED` en om het veld `description` bij te werken met een nieuwe beschrijving.

>[!IMPORTANT]
>
>Wanneer het verzenden van veelvoudige PATCH verrichtingen in één enkel verzoek, zullen zij in de orde worden verwerkt waarin zij in de serie verschijnen. Zorg ervoor dat u de aanvragen zo nodig in de juiste volgorde verzendt.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Antwoord**

Een succesvolle reactie keert de details van het bijgewerkte beleid terug.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een aangepast beleid verwijderen {#delete}

U kunt een douanebeleid schrappen door zijn `id` in de weg van een verzoek van de DELETE te omvatten.

>[!WARNING]
>
>Nadat beleidsregels zijn verwijderd, kunnen ze niet meer worden hersteld. Het is beste praktijken om een raadpleging (GET) verzoek ](#lookup) eerst uit te voeren om het beleid te bekijken en het te bevestigen het correcte beleid is u wenst om te verwijderen.[

**API-indeling**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De id van het beleid dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) met een lege hoofdtekst.

U kunt de verwijdering bevestigen door te proberen het beleid opnieuw op te zoeken (GET). Er wordt een HTTP 404-fout (Niet gevonden) weergegeven als het beleid is verwijderd.

## Hiermee wordt een lijst met ingeschakelde kernbeleidsregels opgehaald {#list-enabled-core}

Door gebrek, slechts neemt het toegelaten beleid van het gegevensgebruik aan evaluatie deel. U kunt een lijst van kernbeleid terugwinnen dat momenteel door uw organisatie door een verzoek van de GET aan het `/enabledCorePolicies` eindpunt wordt toegelaten.

**API-indeling**

```http
GET /enabledCorePolicies
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de lijst van toegelaten kernbeleid onder een `policyIds` serie terug.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Werk de lijst van toegelaten kernbeleid {#update-enabled-core} bij

Door gebrek, slechts neemt het toegelaten beleid van het gegevensgebruik aan evaluatie deel. Door een verzoek van de PUT aan het `/enabledCorePolicies` eindpunt te doen, kunt u de lijst van toegelaten kernbeleid voor uw organisatie bijwerken gebruikend één enkele vraag.

>[!NOTE]
>
>Alleen kernbeleid kan door dit eindpunt worden in- of uitgeschakeld. Om douanebeleid toe te laten of onbruikbaar te maken, zie de sectie op [het bijwerken van een gedeelte van een beleid](#patch).

**API-indeling**

```http
PUT /enabledCorePolicies
```

**Verzoek**

Het volgende verzoek werkt de lijst van toegelaten kernbeleid bij dat op IDs wordt gebaseerd die in de lading wordt verstrekt.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `policyIds` | Een lijst van kern beleids IDs die moeten worden toegelaten. Om het even welk kernbeleid dat niet inbegrepen is wordt geplaatst aan `DISABLED` status en zal niet aan evaluatie deelnemen. |

**Antwoord**

Een succesvolle reactie keert de bijgewerkte lijst van toegelaten kernbeleid onder een `policyIds` serie terug.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Volgende stappen

Zodra u nieuw beleid of bijgewerkte bestaande degenen hebt bepaald, kunt u [!DNL Policy Service] API gebruiken om marketing acties tegen specifieke etiketten of datasets te testen en te zien of uw beleid schendingen zoals verwacht teweegbrengt. Zie de gids op [beleidsevaluatie eindpunten](./evaluation.md) voor meer informatie.