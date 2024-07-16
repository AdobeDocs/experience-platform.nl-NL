---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor labels
description: Leer hoe u labels voor gegevensgebruik in Experience Platform beheert met de API voor Beleidsservice.
role: Developer
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Labels-eindpunt

Met labels voor gegevensgebruik kunt u gegevens indelen volgens het gebruiksbeleid dat op die gegevens van toepassing kan zijn. Met het `/labels` -eindpunt in de [!DNL Policy Service API] kunt u gegevensgebruikslabels programmatisch beheren in uw ervaringstoepassing.

>[!NOTE]
>
>Het `/labels` eindpunt wordt alleen gebruikt om gegevensgebruikslabels op te halen, te maken en bij te werken. Voor stappen op hoe te om etiketten aan datasets en gebieden toe te voegen die API vraag gebruiken, verwijs naar de gids op [ het beheren van datasetetiketten ](../labels/dataset-api.md).

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt is een deel van [[!DNL Policy Service API] ](https://www.adobe.io/experience-platform-apis/references/policy-service/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Een lijst met labels ophalen {#list}

U kunt alle labels `core` en `custom` weergeven door een aanvraag voor een GET in te dienen bij `/labels/core` respectievelijk `/labels/custom` .

**API formaat**

```http
GET /labels/core
GET /labels/custom
```

**Verzoek**

In het volgende verzoek worden alle aangepaste labels weergegeven die in uw organisatie zijn gemaakt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van douanelabels terug die van het systeem worden teruggewonnen. Aangezien de bovenstaande voorbeeldaanvraag is ingediend bij `/labels/custom` , worden in de onderstaande reactie alleen aangepaste labels weergegeven.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Een label opzoeken {#look-up}

U kunt een specifiek label opzoeken door de eigenschap `name` van dat label op te nemen in het pad van een GET-aanvraag naar de [!DNL Policy Service] API.

**API formaat**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De eigenschap `name` van het aangepaste label dat u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt het aangepaste label `L2` opgehaald, zoals aangegeven in het pad.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Als de reactie is gelukt, worden de details van het aangepaste label geretourneerd.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Een aangepast label maken of bijwerken {#create-update}

Als u een aangepast label wilt maken of bijwerken, moet u een aanvraag voor een PUT indienen bij de API van [!DNL Policy Service] .

**API formaat**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De eigenschap `name` van een aangepast label. Als er geen aangepast label met deze naam bestaat, wordt een nieuw label gemaakt. Als er een label bestaat, wordt dat label bijgewerkt. |

**Verzoek**

In het volgende verzoek wordt een nieuw label `L3` gemaakt dat gegevens beschrijft die informatie bevatten over de geselecteerde betaalplannen van klanten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | Een unieke tekenreeks-id voor het label. Deze waarde wordt gebruikt voor raadplegingsdoeleinden en het toepassen van het etiket op datasets en gebieden, en daarom wordt geadviseerd dat het kort en beknopt is. |
| `category` | De categorie van het etiket. Hoewel u uw eigen categorieën voor douanelabels kunt tot stand brengen, adviseert men sterk dat u `Custom` gebruikt als u het etiket in UI wilt verschijnen. |
| `friendlyName` | Een vriendelijke naam voor het label, dat wordt gebruikt voor weergavedoeleinden. |
| `description` | (Optioneel) Een beschrijving van het label voor verdere context. |

**Reactie**

Een geslaagde reactie retourneert de details van het aangepaste label, met HTTP-code 200 (OK) als een bestaand label is bijgewerkt, of 201 (Gemaakt) als een nieuw label is gemaakt.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Volgende stappen

Deze gids behandelde het gebruik van het `/labels` eindpunt in de Dienst API van het Beleid. Voor stappen op hoe te om etiketten op datasets en gebieden toe te passen, verwijs naar de [ dataset etiketten API gids ](../labels/dataset-api.md).
