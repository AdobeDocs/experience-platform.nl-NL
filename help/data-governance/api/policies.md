---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunt voor beleidsregels voor gegevensbeheer
description: Beleid voor gegevensbeheer is regels die uw organisatie toepast en die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens in Experience Platform of waarvan u een beperking hebt ingesteld. Het /policies eindpunt wordt gebruikt voor alle API vraag met betrekking tot het bekijken van, het creëren van, het bijwerken van, of het schrappen van het beleid van het gegevensbeheer.
role: Developer
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 0%

---

# Doel van beleidsregels voor gegevensbeheer

Beleid voor gegevensbeheer is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform] of waarvan u een beperking hebt ingesteld. Met het `/policies` -eindpunt in [!DNL Policy Service API] kunt u het beleid voor gegevensbeheer voor uw organisatie programmatisch beheren.

>[!IMPORTANT]
>
>Het beleid van het bestuur moet niet met toegangsbeheerbeleid worden verward, dat de specifieke gegevensattributen bepaalt die door bepaalde gebruikers van Experience Platform in uw organisatie kunnen worden betreden. Verwijs naar de `/policies` eindpuntgids voor [ Controle API van de Toegang ](../../access-control/abac/api/policies.md) voor details op hoe te om toegangsbeheerbeleid programmatically te beheren.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Policy Service]  API ](https://www.adobe.io/experience-platform-apis/references/policy-service/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Een lijst met beleidsregels ophalen {#list}

U kunt alle `core` - of `custom` -beleidsregels weergeven door een GET-aanvraag in te dienen bij respectievelijk `/policies/core` of `/policies/custom` .

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie bevat een array `children` met de details van elk opgehaald beleid, inclusief de `id` -waarden. U kunt het `id` gebied van een bepaald beleid gebruiken om [ raadpleging ](#lookup) uit te voeren, [ update ](#update), en [ schrapt ](#delete) verzoeken voor dat beleid.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `status` | De huidige status van een beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED` . Standaard nemen alleen beleidsregels van het type `ENABLED` deel aan de evaluatie. Zie het overzicht op [ beleidsevaluatie ](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array met de URI&#39;s van alle toepasselijke marketingacties voor een beleid. |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | Een voorwerp dat de specifieke etiketten van het gegevensgebruik beschrijft dat de bijbehorende het op de markt brengen actie van een beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [ het creëren van een beleid ](#create-policy) voor meer informatie over dit bezit. |

## Een beleid opzoeken {#look-up}

U kunt een specifiek beleid opzoeken door de `id` -eigenschap van dat beleid op te nemen in het pad van een GET-aanvraag.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
    "imsOrg": "{ORG_ID}",
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
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED` . Standaard nemen alleen beleidsregels van het type `ENABLED` deel aan de evaluatie. Zie het overzicht op [ beleidsevaluatie ](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array met de URI&#39;s van alle toepasselijke marketingacties voor het beleid. |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | Een voorwerp dat de specifieke etiketten van het gegevensgebruik beschrijft dat de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [ het creëren van een beleid ](#create-policy) voor meer informatie over dit bezit. |

## Een aangepast beleid maken {#create-policy}

In de [!DNL Policy Service] API wordt een beleid gedefinieerd door het volgende:

* Een verwijzing naar een specifieke marketingactie
* Een uitdrukking die de etiketten van het gegevensgebruik beschrijft dat de marketing actie tegen wordt beperkt wordt uitgevoerd

Om aan dit laatste vereiste te voldoen, moeten beleidsdefinities een booleaanse uitdrukking betreffende de aanwezigheid van gegevensgebruikslabels omvatten. Deze uitdrukking wordt genoemd een beleidsuitdrukking.

Beleidsexpressies worden gegeven in de vorm van een eigenschap `deny` binnen elke beleidsdefinitie. Een voorbeeld van een eenvoudig `deny` -object dat alleen de aanwezigheid van één label controleert, ziet er als volgt uit:

```json
"deny": {
    "label": "C1"
}
```

In veel beleidsregels worden echter complexere voorwaarden met betrekking tot de aanwezigheid van labels voor gegevensgebruik vastgelegd. Om deze gebruiksgevallen te steunen, kunt u booleaanse verrichtingen ook omvatten om uw beleidsuitdrukkingen te beschrijven. Het beleidsexpressieobject moet een label of een operator en operanden bevatten, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject.

Als u bijvoorbeeld een beleid wilt definiëren dat het uitvoeren van een marketingactie verbiedt op gegevens waarin `C1 OR (C3 AND C7)` -labels aanwezig zijn, wordt de eigenschap `deny` van het beleid als volgt opgegeven:

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
| `operator` | Geeft de voorwaardelijke relatie aan tussen de labels in de verwant `operands` -array. Accepteerde waarden zijn: <ul><li>`OR`: de expressie wordt omgezet in true als een van de labels in de array `operands` aanwezig is.</li><li>`AND`: De expressie wordt alleen omgezet in true als alle labels in de array `operands` aanwezig zijn.</li></ul> |
| `operands` | Een array van objecten, waarbij elk object één label of een extra paar `operator` - en `operands` -eigenschappen vertegenwoordigt. De aanwezigheid van de labels en/of bewerkingen in een `operands` -array wordt op basis van de waarde van de eigenschap `operator` sibling omgezet in true of false. |
| `label` | De naam van één gegevensgebruikslabel dat op het beleid van toepassing is. |

U kunt een nieuw douanebeleid tot stand brengen door een POST- verzoek aan het `/policies/custom` eindpunt te doen.

**API formaat**

```http
POST /policies/custom
```

**Verzoek**

Met de volgende aanvraag wordt een nieuw beleid gemaakt dat verhindert dat de marketingactie `exportToThirdParty` wordt uitgevoerd op gegevens die labels bevatten `C1 OR (C3 AND C7)` .

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED` . Standaard nemen alleen beleidsregels van het type `ENABLED` deel aan de evaluatie. Zie het overzicht op [ beleidsevaluatie ](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array met de URI&#39;s van alle toepasselijke marketingacties voor het beleid. URI voor een marketing actie wordt verstrekt onder `_links.self.href` in de reactie voor [ zoekend een marketing actie ](./marketing-actions.md#look-up). |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | De beleidsuitdrukking die de specifieke etiketten van het gegevensgebruik beschrijft de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. |

**Reactie**

Een geslaagde reactie retourneert de details van het nieuwe beleid, inclusief de `id` ervan. Deze waarde is alleen-lezen en wordt automatisch toegewezen wanneer het beleid wordt gemaakt.

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
    "imsOrg": "{ORG_ID}",
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

## Een aangepast beleid bijwerken {#update}

>[!IMPORTANT]
>
>U kunt alleen aangepast beleid bijwerken. Als u wenst om kernbeleid toe te laten of onbruikbaar te maken, zie de sectie bij [ het bijwerken van de lijst van toegelaten kernbeleid ](#update-enabled-core).

U kunt een bestaand douanebeleid bijwerken door zijn identiteitskaart in de weg van een verzoek van PUT met een lading te verstrekken die de bijgewerkte vorm van het beleid in zijn geheel omvat. Met andere woorden, het PUT-verzoek herschrijft in wezen het beleid.

>[!NOTE]
>
>Zie de sectie op [ het bijwerken van een gedeelte van een douanebeleid ](#patch) als u slechts één of meerdere gebieden voor een beleid wilt bijwerken, eerder dan het te beschrijven.

**API formaat**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` van het beleid u wilt bijwerken. |

**Verzoek**

In dit voorbeeld zijn de voorwaarden voor het exporteren van gegevens naar een derde gewijzigd. U hebt nu het beleid dat u hebt gemaakt nodig om deze marketingactie te weigeren als `C1 AND C5` -gegevenslabels aanwezig zijn.

Het volgende verzoek werkt het bestaande beleid bij om de nieuwe beleidsuitdrukking te omvatten. Merk op dat aangezien dit verzoek hoofdzakelijk het beleid herschrijft, alle gebieden in de lading moeten worden omvat, zelfs als sommige van hun waarden niet worden bijgewerkt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | De huidige status van het beleid. Er zijn drie mogelijke statussen: `DRAFT`, `ENABLED` of `DISABLED` . Standaard nemen alleen beleidsregels van het type `ENABLED` deel aan de evaluatie. Zie het overzicht op [ beleidsevaluatie ](../enforcement/overview.md) voor meer informatie. |
| `marketingActionRefs` | Een array met de URI&#39;s van alle toepasselijke marketingacties voor het beleid. URI voor een marketing actie wordt verstrekt onder `_links.self.href` in de reactie voor [ zoekend een marketing actie ](./marketing-actions.md#look-up). |
| `description` | Een optionele beschrijving die een verdere context biedt voor het gebruiksgeval van het beleid. |
| `deny` | De beleidsuitdrukking die de specifieke etiketten van het gegevensgebruik beschrijft de bijbehorende het op de markt brengen actie van het beleid wordt beperkt van wordt uitgevoerd op. Zie de sectie over [ het creëren van een beleid ](#create-policy) voor meer informatie over dit bezit. |

**Reactie**

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
    "imsOrg": "{ORG_ID}",
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

## Een gedeelte van een aangepast beleid bijwerken {#patch}

>[!IMPORTANT]
>
>U kunt alleen aangepast beleid bijwerken. Als u wenst om kernbeleid toe te laten of onbruikbaar te maken, zie de sectie bij [ het bijwerken van de lijst van toegelaten kernbeleid ](#update-enabled-core).

Een specifiek gedeelte van een beleid kan worden bijgewerkt met behulp van een PATCH-aanvraag. In tegenstelling tot PUT-verzoeken om het beleid te herschrijven, werkt PATCH alleen de eigenschappen bij die in de aanvraaginstantie zijn opgegeven. Dit is vooral nuttig wanneer u een beleid wilt toelaten of onbruikbaar maken, aangezien u slechts de weg aan het aangewezen bezit (`/status`) en zijn waarde (`ENABLED` of `DISABLED`) moet verstrekken.

>[!NOTE]
>
>Betalingen voor PATCH-aanvragen volgen de opmaak van JSON Patch. Zie de [ API grondbeginselen gids ](../../landing/api-fundamentals.md) voor meer informatie over de toegelaten syntaxis.

De API van [!DNL Policy Service] ondersteunt de JSON-patchbewerkingen `add` , `remove` en `replace` en stelt u in staat meerdere updates samen te voegen tot één aanroep, zoals in het onderstaande voorbeeld wordt getoond.

**API formaat**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` van het beleid waarvan u de eigenschappen wilt bijwerken. |

**Verzoek**

In de volgende aanvraag worden twee `replace` -bewerkingen gebruikt om de beleidsstatus te wijzigen van `DRAFT` in `ENABLED` en om het veld `description` bij te werken met een nieuwe beschrijving.

>[!IMPORTANT]
>
>Wanneer meerdere PATCH-bewerkingen in één aanvraag worden verzonden, worden deze verwerkt in de volgorde waarin ze in de array voorkomen. Zorg ervoor dat u de aanvragen zo nodig in de juiste volgorde verzendt.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

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
    "imsOrg": "{ORG_ID}",
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

U kunt een aangepast beleid verwijderen door de `id` ervan op te nemen in het pad van een DELETE-aanvraag.

>[!WARNING]
>
>Nadat beleidsregels zijn verwijderd, kunnen ze niet meer worden hersteld. Het is beste praktijken om een raadpleging (GET) verzoek ](#lookup) eerst uit te voeren om het beleid te bekijken en het te bevestigen is het correcte beleid u wenst te verwijderen.[

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 (OK) met een lege hoofdtekst.

U kunt de verwijdering bevestigen door het beleid opnieuw op te zoeken (GET). Er wordt een HTTP 404-fout (Niet gevonden) weergegeven als het beleid is verwijderd.

## Een lijst met ingeschakelde kernbeleidsregels ophalen {#list-enabled-core}

Standaard wordt alleen een beleid voor gegevensbeheer aan de evaluatie toegevoegd. U kunt een lijst van kernbeleid terugwinnen dat momenteel door uw organisatie door een GET verzoek aan het `/enabledCorePolicies` eindpunt wordt toegelaten.

**API formaat**

```http
GET /enabledCorePolicies
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de lijst met ingeschakelde kernbeleidsregels onder een `policyIds` -array.

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
  "imsOrg": "{ORG_ID}",
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

## De lijst met ingeschakelde kernbeleidsregels bijwerken {#update-enabled-core}

Standaard wordt alleen een beleid voor gegevensbeheer aan de evaluatie toegevoegd. Door een PUT-aanvraag naar het `/enabledCorePolicies` -eindpunt in te dienen, kunt u de lijst met ingeschakeld kernbeleid voor uw organisatie bijwerken met behulp van één aanroep.

>[!NOTE]
>
>Alleen kernbeleid kan door dit eindpunt worden in- of uitgeschakeld. Om douanebeleid toe te laten of onbruikbaar te maken, zie de sectie op [ het bijwerken van een gedeelte van een beleid ](#patch).

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | Een lijst van kern beleids IDs die moeten worden toegelaten. Alle kernbeleidsregels die niet in de lijst zijn opgenomen, worden ingesteld op `DISABLED` status en nemen niet deel aan de evaluatie. |

**Reactie**

Een geslaagde reactie retourneert de bijgewerkte lijst van ingeschakelde kernbeleidsregels onder een `policyIds` -array.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

Nadat u nieuwe of bijgewerkte beleidsregels hebt gedefinieerd, kunt u de API van [!DNL Policy Service] gebruiken om marketingacties te testen op specifieke labels of gegevenssets en om te zien of uw beleid schendingen aan de orde stelt zoals u had verwacht. Zie de gids op de [ eindpunten van de beleidsevaluatie ](./evaluation.md) voor meer informatie.
