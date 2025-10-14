---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;marketingacties api;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunt voor marketinghandelingen
description: Een marketingactie in het kader van de Adobe Experience Platform Data Governance is een actie die een consument van gegevens uit een Experience Platform neemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.
role: Developer
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# Eindpunt van marketingacties

Een marketingactie, in het kader van de Adobe Experience Platform Data Governance, is een actie die een [!DNL Experience Platform] gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.

U kunt marketing acties voor uw organisatie beheren door het `/marketingActions` eindpunt in de Dienst API van het Beleid te gebruiken.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [[!DNL Policy Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/policy-service/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Een lijst met marketingacties ophalen {#list}

U kunt een lijst met basis- of aangepaste marketingacties opvragen door een GET-aanvraag in te dienen bij respectievelijk `/marketingActions/core` of `/marketingActions/custom` .

**API formaat**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald met aangepaste marketingacties die door uw organisatie worden onderhouden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de details voor elke opgehaalde marketingactie, inclusief de acties `name` en `href` . De `href` waarde wordt gebruikt om de marketing actie te identificeren wanneer [&#x200B; het creëren van een beleid van het gegevensgebruik &#x200B;](policies.md#create-policy).

```json
{
    "_page": {
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `_page.count` | Het totale aantal geretourneerde marketingacties. |
| `children` | Een array met objecten die de details van de opgehaalde marketingacties bevatten. |
| `name` | De naam van de marketing actie, die als zijn uniek herkenningsteken dienst doet wanneer [&#x200B; omhoog een specifieke marketing actie &#x200B;](#lookup) kijkt. |
| `_links.self.href` | Een verwijzing van URI voor de marketing actie, die kan worden gebruikt om de `marketingActionsRefs` serie te voltooien wanneer [&#x200B; het creëren van een beleid van het gegevensgebruik &#x200B;](policies.md#create-policy). |

## Een specifieke marketingactie opzoeken {#lookup}

U kunt de details van een specifieke marketingactie opzoeken door de eigenschap `name` van de marketingactie op te nemen in het pad van een GET-aanvraag.

**API formaat**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De eigenschap `name` van de marketingactie die u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt een aangepaste marketingactie met de naam `combineData` opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Het reactievoorwerp bevat de details voor de marketing actie, met inbegrip van de weg (`_links.self.href`) nodig om de marketing actie te verwijzen wanneer [&#x200B; het bepalen van een beleid van het gegevensgebruik &#x200B;](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Een aangepaste marketingactie maken of bijwerken {#create-update}

U kunt een nieuwe aangepaste marketingactie maken of een bestaande actie bijwerken door de bestaande of beoogde naam van de marketingactie op te nemen in het pad van een aanvraag voor een PUT.

**API formaat**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden gemaakt of bijgewerkt. Als het systeem al een marketingactie met de opgegeven naam bevat, wordt die marketingactie bijgewerkt. Als er geen naam bestaat, wordt er een nieuwe marketingactie voor de opgegeven naam gemaakt. |

**Verzoek**

Met het volgende verzoek wordt een nieuwe marketingactie met de naam `crossSiteTargeting` gemaakt, op voorwaarde dat het systeem nog geen marketingactie met dezelfde naam uitvoert. Als er wel een marketingactie van `crossSiteTargeting` bestaat, wordt die marketingactie bijgewerkt op basis van de eigenschappen die in de payload zijn opgegeven.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de marketingactie die moet worden gemaakt of bijgewerkt. <br><br>**BELANGRIJK**: Dit bezit moet `{MARKETING_ACTION_NAME}` in de weg aanpassen, anders zal een HTTP 400 (Onjuiste Verzoek) fout voorkomen. Met andere woorden, wanneer een marketingactie is gemaakt, kan de eigenschap `name` ervan niet worden gewijzigd. |
| `description` | Een optionele beschrijving om de context van de marketingactie te verfijnen. |

**Reactie**

Als de reactie succesvol was, worden de details van de marketingactie geretourneerd. Als een bestaande marketingactie is bijgewerkt, retourneert de reactie HTTP-status 200 (OK). Als een nieuwe marketing actie werd gecreeerd, keert de reactie HTTP status 201 (Gemaakt) terug.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Een aangepaste marketingactie verwijderen {#delete}

U kunt een aangepaste marketingactie verwijderen door de naam ervan op te nemen in het pad van een DELETE-aanvraag.

>[!NOTE]
>
>Marketing-acties waarnaar wordt verwezen door bestaand beleid, kunnen niet worden verwijderd. Wanneer u probeert een van deze marketingacties te verwijderen, wordt een HTTP 400-fout (Onjuist verzoek) gegenereerd samen met een bericht dat de id&#39;s bevat van alle beleidsvormen die naar de marketingactie verwijzen.

**API formaat**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP Status 200 (OK) met een lege antwoordinstantie.

U kunt de schrapping bevestigen door te proberen [&#x200B; omhoog de marketing actie &#x200B;](#look-up) te kijken. Er wordt een HTTP 404-fout (Niet gevonden) weergegeven als de marketingactie van het systeem is verwijderd.
