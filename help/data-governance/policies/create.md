---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevensbeheer;gegevensgebruiksbeleid
solution: Experience Platform
title: Een beleid voor gegevensgebruik maken in de API
topic: policies
type: Tutorial
description: De dienst API van het Beleid staat u toe om het beleid van het gegevensgebruik tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die bepaalde etiketten van het gegevensgebruik bevatten. Dit document verstrekt een geleidelijke zelfstudie voor het creëren van een beleid gebruikend de Dienst API van het Beleid.
translation-type: tm+mt
source-git-commit: 55a54463e918fc62378c660ef17f36e2ede471e0
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---


# Een beleid voor gegevensgebruik maken in de API

Met de [Beleidsservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) kunt u beleid voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde labels voor gegevensgebruik bevatten.

Dit document bevat een stapsgewijze zelfstudie voor het maken van een beleid met de API [!DNL Policy Service]. Voor een uitvoerigere gids voor de verschillende verrichtingen beschikbaar in API, zie [de de ontwikkelaarsgids van de Dienst van het Beleid](../api/getting-started.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende belangrijke concepten betrokken bij het creëren en evalueren van beleid:

* [Adobe Experience Platform Data Governance](../home.md): Het kader waardoor de naleving van het gegevensgebruik wordt  [!DNL Platform] afgedwongen.
   * [Labels](../labels/overview.md) voor gegevensgebruik: Labels voor gegevensgebruik worden toegepast op XDM-gegevensvelden en geven beperkingen op voor de manier waarop die gegevens kunnen worden benaderd.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.
* [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voordat u deze zelfstudie start, raadpleegt u de [ontwikkelaarshandleiding](../api/getting-started.md) voor belangrijke informatie die u moet weten om oproepen naar de [!DNL Policy Service] API te kunnen uitvoeren, inclusief vereiste headers en hoe u voorbeeld-API-aanroepen kunt lezen.

## Een marketingactie definiëren {#define-action}

In het [!DNL Data Governance] kader, is een marketing actie een actie die een [!DNL Experience Platform] gegevensconsument neemt, waarvoor er een behoefte is om op schendingen van het beleid van het gegevensgebruik te controleren.

De eerste stap bij het creëren van een beleid van het gegevensgebruik is te bepalen welke marketing actie het beleid zal evalueren. U kunt dit op een van de volgende manieren doen:

* [Een bestaande marketingactie opzoeken](#look-up)
* [Nieuwe marketingactie maken](#create-new)

### Bestaande marketingactie opzoeken {#look-up}

U kunt bestaande marketing acties opzoeken die door uw beleid moeten worden geëvalueerd door een verzoek van de GET aan één van `/marketingActions` eindpunten te richten.

**API-indeling**

Afhankelijk van of u een marketingactie opzoekt die wordt geleverd door [!DNL Experience Platform] of een aangepaste marketingactie die door uw organisatie is gemaakt, gebruikt u respectievelijk de `marketingActions/core`- of `marketingActions/custom`-eindpunten.

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

Een succesvolle reactie retourneert het totale aantal gevonden marketingacties (`count`) en geeft de details van de marketingacties zelf weer binnen de `children`-array.

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
| `_links.self.href` | Elk item in de array `children` bevat een URI-id voor de vermelde marketingactie. |

Wanneer u de marketing actie vindt die u wilt gebruiken, registreer de waarde van zijn `href` bezit. Deze waarde wordt gebruikt tijdens de volgende stap van [het creëren van een beleid](#create-policy).

### Nieuwe marketingactie maken {#create-new}

U kunt een nieuwe marketing actie tot stand brengen door een verzoek van de PUT aan het `/marketingActions/custom/` eindpunt te doen en een naam voor de marketing actie aan het eind van de verzoekweg te verstrekken.

**API-indeling**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de nieuwe marketingactie die u wilt maken. Deze naam fungeert als de primaire id van de marketingactie en moet daarom uniek zijn. De beste manier is om de marketingactie een beschrijvende maar beknopte naam te geven. |

**Verzoek**

Het volgende verzoek leidt tot een nieuwe douanemarketing actie genoemd &quot;exportToThirdParty&quot;. Merk op dat `name` in de verzoeklading het zelfde is als de naam die in de verzoekweg wordt verstrekt.

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

Registreer de URI-id van de zojuist gemaakte marketingactie, zoals deze wordt gebruikt in de volgende stap van het maken van een beleid.

## Een beleid maken {#create-policy}

Als u een nieuw beleid wilt maken, moet u de URI-id van een marketingactie opgeven met een expressie van de gebruikslabels die die marketingactie verbiedt.

Deze expressie wordt een beleidsexpressie genoemd en is een object dat (A) een label of (B) een operator en operanden bevat, maar niet beide. Elke operand is op zijn beurt ook een beleidsexpressieobject. Een beleid voor het exporteren van gegevens naar een derde kan bijvoorbeeld worden verboden als er `C1 OR (C3 AND C7)`-labels aanwezig zijn. Deze expressie wordt opgegeven als:

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

Zodra u uw beleidsuitdrukking hebt gevormd, kunt u een nieuw beleid tot stand brengen door een verzoek van de POST aan het `/policies/custom` eindpunt te doen.

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
| `marketingActionRefs` | Een array met de `href`-waarde van een marketingactie, verkregen in de [vorige stap](#define-action). In het bovenstaande voorbeeld wordt slechts één marketingactie vermeld, maar er kunnen ook meerdere acties worden uitgevoerd. |
| `deny` | Het beleidsexpressieobject. Bepaalt de gebruiksetiketten en de voorwaarden die het beleid zouden veroorzaken om de marketing actie te verwerpen die in `marketingActionRefs` van verwijzingen wordt voorzien. |

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
| `id` | Een alleen-lezen, door het systeem gegenereerde waarde die het beleid op unieke wijze identificeert. |

Registreer URI identiteitskaart van het onlangs gecreëerde beleid, aangezien het in de volgende stap wordt gebruikt om het beleid toe te laten.

## Het beleid inschakelen

>[!NOTE]
>
>Hoewel deze stap optioneel is als u uw beleid in `DRAFT` status wilt verlaten, gelieve te merken dat door gebrek een beleid zijn status moet hebben aan `ENABLED` om aan evaluatie deel te nemen. Zie de gids op [beleidshandhaving](../enforcement/api-enforcement.md) voor informatie over hoe te om uitzonderingen voor beleid in `DRAFT` status te maken.

Door gebrek, nemen het beleid dat hun `status` bezit heeft die aan `DRAFT` wordt geplaatst niet aan evaluatie deel. U kunt uw beleid voor evaluatie toelaten door een verzoek van PATCH aan het `/policies/custom/` eindpunt te doen en het unieke herkenningsteken voor het beleid aan het eind van de verzoekweg te verstrekken.

**API-indeling**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{POLICY_ID}` | De waarde `id` van het beleid u wilt toelaten. |

**Verzoek**

Het volgende verzoek voert een PATCH verrichting op het `status` bezit van het beleid uit, veranderend zijn waarde van `DRAFT` in `ENABLED`.

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

Een geslaagde reactie retourneert HTTP-status 200 (OK) en de details van het bijgewerkte beleid, waarbij `status` nu is ingesteld op `ENABLED`.

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

Aan de hand van deze zelfstudie hebt u een beleid voor gegevensgebruik voor een marketingactie gemaakt. U kunt nu doorgaan met de zelfstudie over [beleidsregels voor gegevensgebruik afdwingen](../enforcement/api-enforcement.md) om te leren hoe u kunt controleren op beleidsovertredingen en deze kunt afhandelen in uw ervaringstoepassing.

Zie [Handleiding voor ontwikkelaars van beleidsservices](../api/getting-started.md) voor meer informatie over de verschillende beschikbare bewerkingen in de [!DNL Policy Service]-API. Voor informatie over hoe te om beleid voor [!DNL Real-time Customer Profile] gegevens af te dwingen, zie de zelfstudie over [het afdwingen van de naleving van het gegevensgebruik voor publiekssegmenten](../../segmentation/tutorials/governance.md).

Meer informatie over het beheren van gebruiksbeleid in de [!DNL Experience Platform] gebruikersinterface vindt u in de [beleidsgebruikershandleiding](user-guide.md).