---
keywords: Experience Platform;home;popular topics;Policy enforcement;marketing actions api;API-based enforcement;data governance
solution: Experience Platform
title: Marketingacties
topic: developer guide
description: Een marketingactie, in het kader van de Adobe Experience Platform Data Governance, is een actie die een consument van gegevens uit een Experience Platform neemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---


# Eindpunt marketingacties

Een marketingactie in het kader van de Adobe Experience Platform [!DNL Data Governance]is een actie die een [!DNL Experience Platform] gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.

U kunt marketing acties voor uw organisatie beheren door het `/marketingActions` eindpunt in de Dienst API van het Beleid te gebruiken.

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Lees voordat u verdergaat de gids [Aan de](./getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Een lijst met marketingacties ophalen {#list}

U kunt een lijst met basis- of aangepaste marketingacties opvragen door een GET-aanvraag in te dienen bij `/marketingActions/core` of `/marketingActions/custom`.

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert de details voor elke opgehaalde marketingactie, inclusief de `name` en `href`. De `href` waarde wordt gebruikt om de marketing actie te identificeren wanneer het [creëren van een beleid](policies.md#create-policy)van het gegevensgebruik.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `name` | De naam van de marketingactie, die fungeert als unieke id wanneer een specifieke marketingactie [wordt](#lookup)gezocht. |
| `_links.self.href` | Een URI-referentie voor de marketingactie die kan worden gebruikt om de `marketingActionsRefs` array te voltooien wanneer u een beleid voor [gegevensgebruik](policies.md#create-policy)maakt. |

## Een specifieke marketingactie opzoeken {#lookup}

U kijkt omhoog de details van een specifieke marketing actie door het bezit van de marketing actie in de weg van een verzoek van de GET te omvatten. `name`

**API-indeling**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De `name` eigenschap van de marketingactie die u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt een aangepaste marketingactie met de naam `combineData`opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject bevat de details voor de marketingactie, inclusief het pad (`_links.self.href`) dat nodig is om naar de marketingactie te verwijzen bij het [definiëren van een beleid](policies.md#create-policy) voor gegevensgebruik (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
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

**API-indeling**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketingactie die moet worden gemaakt of bijgewerkt. Als het systeem al een marketingactie met de opgegeven naam bevat, wordt die marketingactie bijgewerkt. Als er geen naam bestaat, wordt er een nieuwe marketingactie voor de opgegeven naam gemaakt. |

**Verzoek**

Met het volgende verzoek wordt een nieuwe marketingactie met de naam `crossSiteTargeting`gemaakt, op voorwaarde dat het systeem nog geen marketingactie met dezelfde naam uitvoert. Als een `crossSiteTargeting` marketing actie bestaat, werkt deze vraag in plaats daarvan die marketing actie bij die op de eigenschappen wordt gebaseerd die in de lading worden verstrekt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de marketingactie die moet worden gemaakt of bijgewerkt. <br><br>**BELANGRIJK**: Deze eigenschap moet overeenkomen met de waarde `{MARKETING_ACTION_NAME}` in het pad, anders treedt een HTTP 400-fout (Bad Request) op. Met andere woorden, wanneer een marketingactie is gemaakt, kan de `name` eigenschap ervan niet worden gewijzigd. |
| `description` | Een optionele beschrijving om de context van de marketingactie te verfijnen. |

**Antwoord**

Als de reactie succesvol was, worden de details van de marketingactie geretourneerd. Als een bestaande marketing actie werd bijgewerkt, keert de reactie HTTP status 200 (O.K.) terug. Als een nieuwe marketing actie werd gecreeerd, keert de reactie HTTP status 201 (Gemaakt) terug.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
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

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 200 (OK) met een lege antwoordinstantie.

U kunt de verwijdering bevestigen door te proberen de marketingactie [](#look-up)op te zoeken. Er wordt een HTTP 404-fout (Niet gevonden) weergegeven als de marketingactie van het systeem is verwijderd.
