---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;marketingacties api;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: API-eindpunt voor marketinghandelingen
topic: developer guide
description: Een marketingactie, in het kader van de Adobe Experience Platform Data Governance, is een actie die een consument van gegevens uit een Experience Platform neemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Eindpunt marketingacties

Een marketingactie in de context van de Adobe Experience Platform [!DNL Data Governance] is een actie die een [!DNL Experience Platform]-gegevensconsument onderneemt, waarvoor het nodig is te controleren op overtredingen van het beleid voor gegevensgebruik.

U kunt marketing acties voor uw organisatie beheren door het `/marketingActions` eindpunt in de Dienst API van het Beleid te gebruiken.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Een lijst met marketingacties ophalen {#list}

U kunt een lijst van kern of douanemarketing acties terugwinnen door een verzoek van de GET aan `/marketingActions/core` of `/marketingActions/custom`, respectievelijk te richten.

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

Een geslaagde reactie retourneert de details voor elke opgehaalde marketingactie, inclusief `name` en `href`. De waarde `href` wordt gebruikt om de marketing actie te identificeren wanneer [het creëren van een beleid van het gegevensgebruik](policies.md#create-policy).

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
| `name` | De naam van de marketingactie, die fungeert als unieke id wanneer [een specifieke marketingactie](#lookup) wordt opgezocht. |
| `_links.self.href` | Een URI-referentie voor de marketingactie die kan worden gebruikt om de `marketingActionsRefs`-array te voltooien wanneer [een beleid voor gegevensgebruik maakt](policies.md#create-policy). |

## Een specifieke marketingactie opzoeken {#lookup}

U kijkt omhoog de details van een specifieke marketing actie door het bezit `name` van de marketing actie in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De eigenschap `name` van de marketingactie die u wilt opzoeken. |

**Verzoek**

Het volgende verzoek wint een douanemarketing actie genoemd `combineData` terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject bevat de details voor de marketingactie, inclusief het pad (`_links.self.href`) dat nodig is om naar de marketingactie te verwijzen wanneer [een beleid voor gegevensgebruik definiëren](policies.md#create-policy) (`marketingActionsRefs`).

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

Het volgende verzoek leidt tot een nieuwe marketing actie genoemd `crossSiteTargeting`, op voorwaarde dat een marketing actie van de zelfde naam nog niet in het systeem bestaat. Als een `crossSiteTargeting` marketing actie bestaat, werkt deze vraag in plaats daarvan die marketing actie bij die op de eigenschappen wordt gebaseerd die in de nuttige lading worden verstrekt.

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
| `name` | De naam van de marketingactie die moet worden gemaakt of bijgewerkt. <br><br>**BELANGRIJK**: Deze eigenschap moet overeenkomen met de  `{MARKETING_ACTION_NAME}` in het pad, anders treedt een HTTP 400-fout (Bad Request) op. Met andere woorden, wanneer een marketingactie is gemaakt, kan de eigenschap `name` van de actie niet meer worden gewijzigd. |
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

## Een aangepaste marketingactie {#delete} verwijderen

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

U kunt de schrapping bevestigen door te proberen om [de marketing actie](#look-up) op te zoeken. Er wordt een HTTP 404-fout (Niet gevonden) weergegeven als de marketingactie van het systeem is verwijderd.
