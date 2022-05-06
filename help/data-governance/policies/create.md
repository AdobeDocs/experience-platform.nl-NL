---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevensbeheer;gegevensgebruiksbeleid
solution: Experience Platform
title: Een beleid voor gegevensgebruik maken in de API
topic-legacy: policies
type: Tutorial
description: De dienst API van het Beleid staat u toe om het beleid van het gegevensgebruik tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die bepaalde etiketten van het gegevensgebruik bevatten. Dit document verstrekt een geleidelijke zelfstudie voor het creëren van een beleid gebruikend de Dienst API van het Beleid.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Een beleid voor gegevensgebruik maken in de API

De [Beleidsservice-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) Hiermee kunt u beleid voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde labels voor gegevensgebruik bevatten.

Dit document bevat een stapsgewijze zelfstudie voor het maken van een beleid met de [!DNL Policy Service] API. Voor een uitgebreidere handleiding voor de verschillende bewerkingen die beschikbaar zijn in de API raadpleegt u de [Handleiding voor ontwikkelaars van beleidsservices](../api/getting-started.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten betrokken bij het creëren en evalueren van beleid:

* [Adobe Experience Platform Data Governance](../home.md): Het kader waarbinnen [!DNL Platform] dwingt gegevensgebruiksnaleving af.
   * [Labels voor gegevensgebruik](../labels/overview.md): Labels voor gegevensgebruik worden toegepast op XDM-gegevensvelden en geven beperkingen op voor de manier waarop die gegevens kunnen worden benaderd.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Lees voordat u deze zelfstudie start de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan te maken [!DNL Policy Service] API, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een marketingactie definiëren {#define-action}

In het kader van gegevensbeheer is een marketingactie een actie die [!DNL Experience Platform] gegevens die de consument nodig heeft en waarvoor moet worden gecontroleerd op overtredingen van het beleid inzake gegevensgebruik.

De eerste stap bij het creëren van een beleid van het gegevensgebruik is te bepalen welke marketing actie het beleid zal evalueren. U kunt dit op een van de volgende manieren doen:

* [Een bestaande marketingactie opzoeken](#look-up)
* [Nieuwe marketingactie maken](#create-new)

### Een bestaande marketingactie opzoeken {#look-up}

U kunt bestaande marketingacties opzoeken die door uw beleid moeten worden beoordeeld door een GET-aanvraag in te dienen bij een van de `/marketingActions` eindpunten.

**API-indeling**

Afhankelijk van of u een marketingactie zoekt die wordt geleverd door [!DNL Experience Platform] of een aangepaste marketingactie die door uw organisatie is gemaakt, kunt u de opdracht `marketingActions/core` of `marketingActions/custom` eindpunten.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Verzoek**

In het volgende verzoek wordt het `marketingActions/custom` eindpunt, dat een lijst van alle marketing acties haalt die door uw organisatie IMS worden bepaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie geeft het totale aantal gevonden marketingacties (`count`) en geeft een overzicht van de bijzonderheden van de marketingacties zelf in het kader van de `children` array.

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
| `_links.self.href` | Elk item in de `children` array bevat een URI-id voor de vermelde marketingactie. |

Wanneer u de marketing actie vindt die u wilt gebruiken, registreer de waarde van zijn `href` eigenschap. Deze waarde wordt gebruikt tijdens de volgende stap van [beleid](#create-policy).

### Nieuwe marketingactie maken {#create-new}

U kunt een nieuwe marketingactie maken door een PUT aan te vragen bij de `/marketingActions/custom/` en het verstrekken van een naam voor de marketing actie aan het eind van de verzoekweg.

**API-indeling**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de nieuwe marketingactie die u wilt maken. Deze naam fungeert als de primaire id van de marketingactie en moet daarom uniek zijn. De beste manier is om de marketingactie een beschrijvende maar beknopte naam te geven. |

**Verzoek**

Het volgende verzoek leidt tot een nieuwe douanemarketing actie genoemd &quot;exportToThirdParty&quot;. Let erop dat de `name` in de aanvraag is de payload gelijk aan de naam die is opgegeven in het aanvraagpad.

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

**Antwoord**

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

Deze expressie wordt een beleidsexpressie genoemd en is een object dat (A) een label of (B) een operator en operanden bevat, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject. Een beleid voor het exporteren van gegevens naar derden kan bijvoorbeeld worden verboden als `C1 OR (C3 AND C7)` er zijn labels aanwezig. Deze expressie wordt opgegeven als:

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

Zodra u uw beleidsuitdrukking hebt gevormd, kunt u een nieuw beleid tot stand brengen door een verzoek van de POST aan het `/policies/custom` eindpunt.

**API-indeling**

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
| `marketingActionRefs` | Een array met de `href` de waarde van een actie voor het in de handel brengen, verkregen in de [vorige stap](#define-action). In het bovenstaande voorbeeld wordt slechts één marketingactie vermeld, maar er kunnen ook meerdere acties worden uitgevoerd. |
| `deny` | Het beleidsexpressieobject. Definieert de gebruikslabels en -voorwaarden die ertoe leiden dat het beleid de marketingactie waarnaar wordt verwezen in `marketingActionRefs`. |

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
| `id` | Een alleen-lezen, door het systeem gegenereerde waarde die het beleid op unieke wijze identificeert. |

Registreer URI identiteitskaart van het onlangs gecreëerde beleid, aangezien het in de volgende stap wordt gebruikt om het beleid toe te laten.

## Het beleid inschakelen

>[!NOTE]
>
>Deze stap is optioneel als u uw beleid wilt laten in `DRAFT` status, let wel dat een beleid standaard de status moet hebben ingesteld op `ENABLED` om aan de evaluatie deel te nemen. Zie de handleiding op [beleidshandhaving](../enforcement/api-enforcement.md) voor informatie over de wijze waarop uitzonderingen voor beleid kunnen worden gemaakt in `DRAFT` status.

Beleid dat standaard zijn `status` eigenschap ingesteld op `DRAFT` niet deelnemen aan de evaluatie. U kunt uw beleid voor evaluatie toelaten door een verzoek van de PATCH tot de `/policies/custom/` eindpunt en het verstrekken van het unieke herkenningsteken voor het beleid aan het eind van de verzoekweg.

**API-indeling**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De `id` De waarde van het beleid u wilt toelaten. |

**Verzoek**

De volgende aanvraag voert een PATCH-bewerking uit op de `status` eigenschap van het beleid, waarvan de waarde wordt gewijzigd `DRAFT` tot `ENABLED`.

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
| `value` | De nieuwe waarde die moet worden toegewezen aan de eigenschap die is opgegeven in `path`. Met deze aanvraag worden de beleidsopties ingesteld `status` eigenschap aan &quot;ENABLED&quot;. |

**Antwoord**

Een succesvolle reactie keert HTTP status 200 (O.K.) en de details van het bijgewerkte beleid, met zijn terug `status` nu ingesteld op `ENABLED`.

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

Aan de hand van deze zelfstudie hebt u een beleid voor gegevensgebruik voor een marketingactie gemaakt. U kunt nu doorgaan met de zelfstudie op [gegevensgebruiksbeleid afdwingen](../enforcement/api-enforcement.md) om te leren hoe u kunt controleren op beleidsovertredingen en deze kunt verwerken in uw ervaringstoepassing.

Voor meer informatie over de verschillende beschikbare bewerkingen in de [!DNL Policy Service] API, zie [Handleiding voor ontwikkelaars van beleidsservices](../api/getting-started.md). Voor informatie over hoe beleidsregels kunnen worden afgedwongen voor [!DNL Real-time Customer Profile] gegevens, raadpleeg de zelfstudie over [naleving van gegevensgebruik afdwingen voor publiekssegmenten](../../segmentation/tutorials/governance.md).

Leren hoe u het gebruiksbeleid kunt beheren in het dialoogvenster [!DNL Experience Platform] gebruikersinterface, zie [beleidsgebruikershandleiding](user-guide.md).
