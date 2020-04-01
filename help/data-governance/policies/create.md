---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een beleid voor gegevensgebruik maken
topic: policies
translation-type: tm+mt
source-git-commit: 04b2e07ba39df9f530c9c93c4bf1af9e2cf30169

---


# Een beleid voor gegevensgebruik maken

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van het Beleid van de Gegevens van het Platform van de Ervaring van Adobe. De [DULE Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) van het Beleid staat u toe om DULE beleid tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die bepaalde etiketten DULE bevatten.

Dit document verstrekt een geleidelijke zelfstudie voor het creëren van een DULE beleid gebruikend de Dienst API van het Beleid. Voor een uitvoerigere gids voor de verschillende verrichtingen beschikbaar in API, zie de de ontwikkelaarsgids [van de Dienst van het](../api/getting-started.md)Beleid.

## Aan de slag

Dit leerprogramma vereist een werkend inzicht in de volgende belangrijkste concepten betrokken bij het creëren van en het evalueren van DULE beleid:

* [Gegevensbeheer](../home.md): Het kader waardoor Platform naleving van gegevensgebruik afdwingt.
* [Labels](../labels/overview.md)voor gegevensgebruik: Labels voor gegevensgebruik worden toegepast op XDM-gegevensvelden en geven beperkingen op voor de manier waarop die gegevens kunnen worden benaderd.
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Alvorens deze zelfstudie te beginnen, te herzien gelieve de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om vraag aan de DULE Dienst API van het Beleid met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een marketingactie definiëren {#define-action}

In het kader van het gegevensbeheer is een marketingactie een actie die een gebruiker van het ervaringsplatform onderneemt en waarvoor moet worden gecontroleerd op schendingen van het gegevensgebruiksbeleid.

De eerste stap bij het creëren van een DULE beleid is te bepalen welke marketing actie het beleid zal evalueren. U kunt dit op een van de volgende manieren doen:

* [Een bestaande marketingactie opzoeken](#look-up)
* [Nieuwe marketingactie maken](#create-new)

### Een bestaande marketingactie opzoeken {#look-up}

U kunt bestaande marketing acties opzoeken die door uw DULE beleid moeten worden geëvalueerd door een GET verzoek aan één van de `/marketingActions` eindpunten te doen.

**API-indeling**

Afhankelijk van of u een marketing actie zoekt die door het Platform van de Ervaring wordt verstrekt of een douanemarketing actie die door uw organisatie wordt gecreeerd, gebruik respectievelijk de `marketingActions/core` eindpunten of `marketingActions/custom` eindpunten.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Verzoek**

Het volgende verzoek gebruikt het `marketingActions/custom` eindpunt, dat een lijst van alle marketing acties haalt die door uw organisatie IMS worden bepaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert het totale aantal gevonden marketingacties (`count`) en geeft de details van de marketingacties zelf weer binnen de `children` array.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `_links.self.href` | Elk item in de `children` array bevat een URI-id voor de vermelde marketingactie. |

Wanneer u de marketing actie vindt die u wilt gebruiken, registreer de waarde van zijn `href` bezit. Deze waarde wordt gebruikt tijdens de volgende stap van het [creëren van een DULE beleid](#create-policy).

### Nieuwe marketingactie maken {#create-new}

U kunt een nieuwe marketing actie tot stand brengen door een PUT verzoek aan het `/marketingActions/custom/` eindpunt te maken en een naam voor de marketing actie aan het eind van de verzoekweg te verstrekken.

**API-indeling**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de nieuwe marketingactie die u wilt maken. Deze naam fungeert als de primaire id van de marketingactie en moet daarom uniek zijn. De beste manier is om de marketingactie een beschrijvende maar beknopte naam te geven. |

**Verzoek**

Het volgende verzoek leidt tot een nieuwe douanemarketing actie genoemd &quot;exportToThirdParty&quot;. U ziet dat de naam `name` in de aanvraag dezelfde is als de naam in het aanvraagpad.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de marketingactie die u wilt maken. Deze naam moet overeenkomen met de naam die is opgegeven in het aanvraagpad, anders treedt er een fout van 400 (Onjuist verzoek) op. |
| `description` | Een door de mens leesbare beschrijving van de marketingactie. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe marketingactie.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `_links.self.href` | De URI-id van de marketingactie. |

Registreer URI identiteitskaart van de pas gecreëerde marketing actie, aangezien het in de volgende stap van het creëren van een DULE beleid zal worden gebruikt.

## Een DULE-beleid maken {#create-policy}

Als u een nieuw beleid wilt maken, moet u de URI-id van een marketingactie opgeven met een expressie van de DULE-labels die die marketingactie verbieden.

Deze expressie wordt een **beleidsexpressie** genoemd en is een object dat (A) een label DULE bevat, of (B) een operator en operanden, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject. Een beleid voor het exporteren van gegevens naar derden kan bijvoorbeeld worden verboden als er `C1 OR (C3 AND C7)` labels aanwezig zijn. Deze expressie wordt opgegeven als:

```json
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
}
```

>[!NOTE] Alleen de operatoren OR en AND worden ondersteund.

Zodra u uw beleidsuitdrukking hebt gevormd, kunt u een nieuw DULE beleid tot stand brengen door een POST- verzoek aan het `/policies/custom` eindpunt te maken.

**API-indeling**

```http
POST /policies/custom
```

**Verzoek**

Het volgende verzoek leidt tot een DULE beleid genoemd &quot;Gegevens van de Uitvoer aan Derde door een marketing actie en beleidsuitdrukking in de verzoeklading te verstrekken.

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

| Eigenschap | Beschrijving |
| --- | --- |
| `marketingActionRefs` | Een array met de `href` waarde van een marketingactie, verkregen in de [vorige stap](#define-action). In het bovenstaande voorbeeld wordt slechts één marketingactie vermeld, maar er kunnen ook meerdere acties worden uitgevoerd. |
| `deny` | Het beleidsexpressieobject. Bepaalt de etiketten DULE en de voorwaarden die het beleid zouden veroorzaken om de marketing actie te verwerpen in `marketingActionRefs`. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van het nieuwe beleid.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | Een read-only, systeem-geproduceerde waarde die uniek het DULE beleid identificeert. |

Registreer identiteitskaart van URI van het pas gecreëerde DULE beleid, aangezien het in de volgende stap wordt gebruikt om het beleid toe te laten.

## Het DULE-beleid inschakelen

>[!NOTE] Hoewel deze stap facultatief is als u uw DULE beleid in `DRAFT` status wilt verlaten, gelieve te merken dat door gebrek een beleid zijn status moet hebben aan `ENABLED` om aan evaluatie deel te nemen. Zie de zelfstudie over het [afdwingen van DULE-beleid](../enforcement/api-enforcement.md) voor informatie over het maken van uitzonderingen voor beleid in `DRAFT` status.

Door gebrek, DULE beleid dat hun `status` bezit heeft worden geplaatst om `DRAFT` niet aan evaluatie deel te nemen. U kunt uw beleid voor evaluatie toelaten door een verzoek van de PATCH aan het `/policies/custom/` eindpunt te doen en het unieke herkenningsteken voor het beleid aan het eind van de verzoekweg te verstrekken.

**API-indeling**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` waarde van het beleid u wilt toelaten. |

**Verzoek**

Het volgende verzoek voert een verrichting van de PATCH op het `status` bezit van het DULE beleid uit, veranderend zijn waarde van `DRAFT` in `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `op` | Het type PATCH-bewerking dat moet worden uitgevoerd. Deze aanvraag voert een vervangingsbewerking uit. |
| `path` | Het pad naar het veld dat moet worden bijgewerkt. Wanneer u een beleid inschakelt, moet de waarde worden ingesteld op &quot;/status&quot;. |
| `value` | De nieuwe waarde die moet worden toegewezen aan de eigenschap die is opgegeven in `path`. Dit verzoek plaatst het `status` bezit van het beleid aan &quot;ENABLED&quot;. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en de details van het bijgewerkte beleid, met de `status` instelling `ENABLED`.

```json
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
    "createdUser": "{CREATED_USER}",
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
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een beleid DULE voor een marketing actie gecreeerd. U kunt nu doorgaan met de zelfstudie over het [afdwingen van DULE-beleid](../enforcement/api-enforcement.md) om te leren hoe u kunt controleren op beleidsovertredingen en deze kunt afhandelen in uw ervaringstoepassing.

Voor meer informatie over de verschillende beschikbare verrichtingen in de Dienst API van het Beleid, zie de de ontwikkelaarsgids [van de Dienst van het](../api/getting-started.md)Beleid. Voor informatie over hoe te om DULE beleid voor de gegevens van het Profiel van de Klant in real time af te dwingen, zie de zelfstudie over het [afdwingen van de naleving van het gegevensgebruik voor publiekssegmenten](../../segmentation/tutorials/governance.md).