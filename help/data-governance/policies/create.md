---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;gegevensgebruiksbeleid
solution: Experience Platform
title: Een beleid voor gegevensbeheer maken in de API
type: Tutorial
description: Leer hoe u een beleid voor gegevensbeheer maakt met de API voor beleidsservice.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Een beleid voor gegevensbeheer maken in de API

De [&#x200B; Dienst API van het Beleid &#x200B;](https://www.adobe.io/experience-platform-apis/references/policy-service/) staat u toe om het beleid van het gegevensbeheer tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die bepaalde etiketten van het gegevensgebruik bevatten.

Dit document bevat een stapsgewijze zelfstudie voor het maken van een beheerbeleid met de API van [!DNL Policy Service] .

>[!NOTE]
>
>Voor stappen op hoe te om tot een beleid van de toegangscontrole te leiden, zie de `/policies` eindpuntgids voor [&#x200B; Controle API van de Toegang &#x200B;](../../access-control/abac/api/policies.md). Leren hoe te om een toestemmingsbeleid tot stand te brengen, zie de [&#x200B; gids van beleid UI &#x200B;](./user-guide.md#consent-policy).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten betrokken bij het creëren en evalueren van beleid:

* [&#x200B; Adobe Experience Platform de Governance van Gegevens &#x200B;](../home.md): Het kader waardoor [!DNL Experience Platform] naleving van het gegevensgebruik afdwingt.
   * [&#x200B; de gebruiksetiketten van Gegevens &#x200B;](../labels/overview.md): De etiketten van het gebruik van gegevens worden toegepast op XDM gegevensgebieden, die beperkingen specificeren voor hoe dat gegeven kan worden betreden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
* [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Alvorens dit leerprogramma te beginnen, te herzien gelieve de [&#x200B; ontwikkelaarsgids &#x200B;](../api/getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan [!DNL Policy Service] API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een marketingactie definiëren {#define-action}

In het kader van gegevensbeheer is een marketingactie een actie die een [!DNL Experience Platform] gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op overtredingen van het gegevensgebruiksbeleid.

De eerste stap bij het creëren van een beleid van het gegevensgebruik is te bepalen welke marketing actie het beleid zal evalueren. U kunt dit op een van de volgende manieren doen:

* [Een bestaande marketingactie opzoeken](#look-up)
* [Nieuwe marketingactie maken](#create-new)

### Een bestaande marketingactie opzoeken {#look-up}

U kunt bestaande marketingacties opzoeken die door uw beleid moeten worden geëvalueerd, door een GET-aanvraag in te dienen bij een van de eindpunten van `/marketingActions` .

**API formaat**

Afhankelijk van of u een marketingactie wilt zoeken die wordt geleverd door [!DNL Experience Platform] of een aangepaste marketingactie die door uw organisatie is gemaakt, gebruikt u respectievelijk de eindpunten `marketingActions/core` of `marketingActions/custom` .

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Verzoek**

Het volgende verzoek gebruikt het `marketingActions/custom` eindpunt, dat een lijst van alle marketing acties haalt die door uw organisatie worden bepaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert het totale aantal gevonden marketingacties (`count`) en geeft de details van de marketingacties zelf weer binnen de array `children` .

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `_links.self.href` | Elk item in de array `children` bevat een URI-id voor de vermelde marketingactie. |

Wanneer u de marketingactie vindt die u wilt gebruiken, neemt u de waarde van de eigenschap `href` op. Deze waarde wordt gebruikt tijdens de volgende stap van [&#x200B; creërend een beleid &#x200B;](#create-policy).

### Nieuwe marketingactie maken {#create-new}

U kunt een nieuwe marketingactie maken door een PUT-aanvraag in te dienen bij het `/marketingActions/custom/` -eindpunt en een naam op te geven voor de marketingactie aan het einde van het aanvraagpad.

**API formaat**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de nieuwe marketingactie die u wilt maken. Deze naam fungeert als de primaire id van de marketingactie en moet daarom uniek zijn. De beste manier is om de marketingactie een beschrijvende maar beknopte naam te geven. |

**Verzoek**

Het volgende verzoek leidt tot een nieuwe douanemarketing actie genoemd &quot;exportToThirdParty&quot;. De waarde `name` in de aanvraaglading is gelijk aan de naam die is opgegeven in het aanvraagpad.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe marketingactie.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
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

Registreer de URI-id van de zojuist gemaakte marketingactie, zoals deze wordt gebruikt in de volgende stap van het maken van een beleid.

## Een beleid maken {#create-policy}

Als u een nieuw beleid wilt maken, moet u de URI-id van een marketingactie opgeven met een expressie van de gebruikslabels die die marketingactie verbiedt.

Deze expressie wordt een beleidsexpressie genoemd en is een object dat (A) een label of (B) een operator en operanden bevat, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject. Een beleid voor het exporteren van gegevens naar een derde kan bijvoorbeeld worden verboden als `C1 OR (C3 AND C7)` -labels aanwezig zijn. Deze expressie wordt opgegeven als:

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

>[!NOTE]
>
>Alleen de operatoren OR en AND worden ondersteund.

Zodra u uw beleidsuitdrukking hebt gevormd, kunt u een nieuw beleid tot stand brengen door een POST- verzoek aan het `/policies/custom` eindpunt te doen.

**API formaat**

```http
POST /policies/custom
```

**Verzoek**

Met het volgende verzoek wordt een beleid gemaakt met de naam &quot;Gegevens exporteren naar derden&quot; door een marketingactie en een beleidsexpressie op te geven in de payload van het verzoek.

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
| `marketingActionRefs` | Een serie die de `href` waarde van een marketing actie bevatten, in de [&#x200B; vorige stap &#x200B;](#define-action) wordt verkregen. In het bovenstaande voorbeeld wordt slechts één marketingactie vermeld, maar er kunnen ook meerdere acties worden uitgevoerd. |
| `deny` | Het beleidsexpressieobject. Definieert de gebruikslabels en -voorwaarden die ertoe leiden dat het beleid de marketingactie waarnaar wordt verwezen in `marketingActionRefs` , afwijst. |

**Reactie**

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
    "imsOrg": "{ORG_ID}",
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
| `id` | Een alleen-lezen, door het systeem gegenereerde waarde die het beleid uniek identificeert. |

Registreer URI identiteitskaart van het onlangs gecreëerde beleid, aangezien het in de volgende stap wordt gebruikt om het beleid toe te laten.

## Het beleid inschakelen

>[!NOTE]
>
>Deze stap is optioneel als u uw beleid de status `DRAFT` wilt geven. U moet echter wel opgeven dat de status van een beleid standaard moet zijn ingesteld op `ENABLED` als u wilt deelnemen aan de evaluatie. Zie de gids op [&#x200B; beleidshandhaving &#x200B;](../enforcement/api-enforcement.md) voor informatie over hoe te om uitzonderingen voor beleid in `DRAFT` status te maken.

Beleid waarvoor de eigenschap `status` is ingesteld op `DRAFT` , neemt standaard niet deel aan de evaluatie. U kunt uw beleid voor evaluatie toelaten door een PATCH- verzoek aan het `/policies/custom/` eindpunt te doen en het unieke herkenningsteken voor het beleid te verstrekken aan het eind van de verzoekweg.

**API formaat**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` waarde van het beleid u wilt toelaten. |

**Verzoek**

In de volgende aanvraag wordt een PATCH-bewerking uitgevoerd op de eigenschap `status` van het beleid, waarbij de waarde wordt gewijzigd van `DRAFT` in `ENABLED` .

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `value` | De nieuwe waarde die moet worden toegewezen aan de eigenschap die is opgegeven in `path` . Deze aanvraag stelt de eigenschap `status` van het beleid in op &quot;ENABLED&quot;. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en de details van het bijgewerkte beleid, waarbij `status` nu is ingesteld op `ENABLED` .

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
    "imsOrg": "{ORG_ID}",
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

Aan de hand van deze zelfstudie hebt u een beleid voor gegevensgebruik voor een marketingactie gemaakt. U kunt nu aan het leerprogramma blijven op [&#x200B; afdwingend beleid van het gegevensgebruik &#x200B;](../enforcement/api-enforcement.md) leren hoe te om beleidsschendingen te controleren en hen te behandelen in uw ervaringstoepassing.

Voor meer informatie over de verschillende beschikbare verrichtingen in [!DNL Policy Service] API, zie de [&#x200B; gids van de ontwikkelaar van de Dienst van het Beleid &#x200B;](../api/getting-started.md). Voor informatie over hoe te om beleid voor [!DNL Real-Time Customer Profile] gegevens af te dwingen, zie het leerprogramma over [&#x200B; afdwingend de naleving van het gegevensgebruik voor publiekssegmenten &#x200B;](../../segmentation/tutorials/governance.md).

Leren hoe te om gebruiksbeleid in het [!DNL Experience Platform] gebruikersinterface te beheren, zie de [&#x200B; gids van de beleidsgebruiker &#x200B;](user-guide.md).
