---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beleid
topic: developer guide
translation-type: tm+mt
source-git-commit: ba9d4b31cfc3b7924879a91bd125f72159e55fc4
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---


# Beleid

Het beleid van het gebruik van gegevens is regels uw organisatie goedkeurt die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen Experience Platform mag uitvoeren.

Het `/policies` eindpunt wordt gebruikt voor alle API-aanroepen met betrekking tot het weergeven, maken, bijwerken of verwijderen van beleidsregels voor gegevensgebruik.

## Alle beleid weergeven

Om een lijst van beleid te bekijken, kan een GET verzoek worden gemaakt aan `/policies/core` of `/policies/custom` dat alle beleid voor de gespecificeerde container terugkeert.

**API-indeling**

```http
GET /policies/core
GET /policies/custom
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie omvat een &quot;telling&quot;die het totale aantal beleid binnen de gespecificeerde container, evenals de details van elk beleid met inbegrip van zijn `id`. Het `id` veld wordt gebruikt om opzoekverzoeken uit te voeren om specifiek beleid weer te geven en om bewerkingen voor bijwerken en verwijderen uit te voeren.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Een beleid opzoeken

Elk beleid bevat een `id` gebied dat kan worden gebruikt om de details van een specifiek beleid te verzoeken. Als het `id` van een beleid onbekend is, kan het worden gevonden gebruikend het lijst (KRIJGEN) verzoek om van alle beleid binnen een specifieke container (`core` of `custom`) een lijst te maken zoals aangetoond in de vorige stap.

**API-indeling**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het antwoord bevat de details van het beleid, met inbegrip van zeer belangrijke gebieden zoals `id` (dit gebied zou moeten aanpassen `id` verzonden in het verzoek), `name`, `status`, en `description`, evenals een verwijzing naar de marketing actie waarop het beleid (`marketingActionRefs`) wordt gebaseerd.

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een beleid maken {#create-policy}

Voor het maken van een beleid moet een marketingactie worden opgenomen met een expressie van de DULE-labels die die marketingactie verbiedt. Beleidsdefinities moeten een `deny` eigenschap bevatten. Dit is een booleaanse expressie met betrekking tot de aanwezigheid van DULE-labels.

Deze expressie wordt een `PolicyExpression` en is een object dat _een label_ of __ een operator en operanden bevat, maar niet beide. Elke operand is op zijn beurt ook een `PolicyExpression` object. Een beleid voor het exporteren van gegevens naar derden kan bijvoorbeeld worden verboden als er `C1 OR (C3 AND C7)` labels aanwezig zijn. Deze expressie wordt opgegeven als:

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

**API-indeling**

```http
POST /policies/custom
```

**Verzoek**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**Antwoord**

Als dit gelukt is, ontvangt u een HTTP Status 201 (Gemaakt) en bevat de responsinstantie de details van het zojuist gemaakte beleid, inclusief de details `id`. Deze waarde is alleen-lezen en wordt automatisch toegewezen wanneer het beleid wordt gemaakt.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een beleid bijwerken

Mogelijk moet u een beleid voor gegevensgebruik bijwerken nadat het is gemaakt. Dit wordt gedaan door een PPUT- verzoek aan het beleid `id` met een lading die de bijgewerkte vorm van het beleid, in zijn geheel omvat. Met andere woorden, het PUT-verzoek is in wezen een _herformulering_ van het beleid, zodat de instantie alle vereiste informatie moet bevatten, zoals in het onderstaande voorbeeld wordt getoond.

**API-indeling**

```http
PUT /policies/custom/{id}
```

**Verzoek**

In dit voorbeeld zijn de voorwaarden voor het exporteren van gegevens naar een derde gewijzigd. U hebt nu het beleid dat u hebt gemaakt nodig om deze marketingactie te weigeren als er `C1 AND (C3 OR C7)` gegevenslabels aanwezig zijn. U zou de volgende vraag gebruiken om het bestaande beleid bij te werken.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Antwoord**

Een succesvol updateverzoek keert een Status 200 van HTTP (O.K.) terug en het reactielichaam zal het bijgewerkte beleid tonen. De gegevens `id` moeten overeenkomen met de gegevens die in de aanvraag zijn `id` verzonden.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een gedeelte van een beleid bijwerken

Een specifiek gedeelte van een beleid kan worden bijgewerkt gebruikend een verzoek van de PATCH. In tegenstelling tot de verzoeken van de ZET om het beleid te _herschrijven_ , werken de verzoeken van de PATCH slechts de weg bij die in het verzoeklichaam wordt gespecificeerd. Dit is vooral nuttig wanneer u een beleid wilt toelaten of onbruikbaar maken, aangezien u slechts de specifieke weg moet verzenden die u wenst bij te werken (`/status`) en zijn waarde (`ENABLE` of `DISABLE`).

De API van de Dienst van het Beleid steunt momenteel &quot;toevoegt&quot;, &quot;vervangt&quot;, en &quot;verwijdert&quot;de verrichtingen van PATCH, en staat u toe om verscheidene updates samen in één enkele vraag te combineren door elk als voorwerp binnen de serie toe te voegen, zoals aangetoond in de volgende voorbeelden.

**API-indeling**

```http
PATCH /policies/custom/{id}
```

**Verzoek**

In dit voorbeeld gebruiken we de bewerking &quot;replace&quot; om de beleidsstatus te wijzigen van &quot;DRAFT&quot; in &quot;ENABLED&quot; en het beschrijvingsveld bij te werken met een nieuwe beschrijving. We hadden het beschrijvingsveld ook kunnen bijwerken door de bewerking &quot;verwijderen&quot; te gebruiken om de beleidsbeschrijving te verwijderen en vervolgens de bewerking &quot;toevoegen&quot; te gebruiken om een nieuwe bewerking één keer toe te voegen, zoals:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Wanneer het verzenden van veelvoudige verrichtingen van de PATCH in één enkel verzoek, herinner dat zij in de orde zullen worden verwerkt waarin zij in de serie verschijnen, zodat zorg ervoor dat u de verzoeken waar nodig in de correcte orde verzendt.

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

Een succesvol updateverzoek zal een Status 200 van HTTP (O.K.) terugkeren en het antwoordlichaam zal het bijgewerkte beleid tonen (&quot;status&quot;is nu &quot;INGESCHAKELD&quot;en &quot;beschrijving&quot;is veranderd). Het beleid `id` moet overeenkomen met het `id` verzonden in het verzoek.


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Een beleid verwijderen

Als u een beleid moet verwijderen dat u hebt gecreeerd, kunt u dit doen door een DELETE verzoek aan de `id` van het beleid uit te geven u wenst om te schrappen. Het is beste praktijken om een raadpleging (GET) verzoek eerst uit te voeren om het beleid te bekijken en het te bevestigen is het correcte beleid u wenst om te verwijderen. **Nadat beleidsregels zijn verwijderd, kunnen ze niet meer worden hersteld.**

**API-indeling**

```http
DELETE /policies/custom/{id}
```

**Verzoek**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als het beleid met succes is geschrapt, zal de reactiekarakter met een Status 200 van HTTP (O.K.) leeg zijn.

U kunt de schrapping bevestigen door te proberen om (KRIJG) het beleid opnieuw te zoeken. U zou een Status 404 van HTTP (niet Gevonden) samen met een &quot;niet Gevonden&quot;foutenmelding moeten ontvangen omdat het beleid is verwijderd.
