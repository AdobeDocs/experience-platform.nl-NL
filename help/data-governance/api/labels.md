---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor labels
topic-legacy: developer guide
description: Leer hoe u labels voor gegevensgebruik in Experience Platform beheert met de API voor beleidsservice.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Labels-eindpunt

Met labels voor gegevensgebruik kunt u gegevens indelen volgens het gebruiksbeleid dat op die gegevens van toepassing kan zijn. De `/labels` in de [!DNL Policy Service API] kunt u gegevensgebruikslabels programmatisch beheren binnen uw ervaringstoepassing.

>[!NOTE]
>
>De `/labels` het eindpunt wordt slechts gebruikt om, gegevensgebruiksetiketten terug te winnen tot stand te brengen en bij te werken. Voor stappen op hoe te om etiketten aan datasets en gebieden toe te voegen gebruikend API vraag, verwijs naar de gids op [gegevenssetlabels beheren](../labels/dataset-api.md).

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Een lijst met labels ophalen {#list}

U kunt alle `core` of `custom` etiketten door een verzoek van de GET aan `/labels/core` of `/labels/custom`, respectievelijk.

**API-indeling**

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

**Antwoord**

Een succesvolle reactie keert een lijst van douanelabels terug die van het systeem worden teruggewonnen. Aangezien de voorbeeldaanvraag hierboven is ingediend op `/labels/custom`In de onderstaande reactie worden alleen aangepaste labels weergegeven.

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

U kunt een specifiek label opzoeken door dat label op te nemen `name` eigenschap in het pad van een aanvraag van een GET naar de [!DNL Policy Service] API.

**API-indeling**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De `name` eigenschap van het aangepaste label dat u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt het aangepaste label opgehaald `L2`, zoals aangegeven in het pad.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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

Als u een aangepast label wilt maken of bijwerken, moet u de PUT [!DNL Policy Service] API.

**API-indeling**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De `name` eigenschap van een aangepast label. Als er geen aangepast label met deze naam bestaat, wordt een nieuw label gemaakt. Als er een label bestaat, wordt dat label bijgewerkt. |

**Verzoek**

Met de volgende aanvraag wordt een nieuw label gemaakt. `L3`, waarin gegevens worden beschreven die informatie bevatten over de geselecteerde betalingsplannen van klanten.

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
| `category` | De categorie van het etiket. Hoewel u uw eigen categorieën voor douanelabels kunt tot stand brengen, wordt het sterk geadviseerd om te gebruiken `Custom` als u het label in de gebruikersinterface wilt weergeven. |
| `friendlyName` | Een vriendelijke naam voor het label, dat wordt gebruikt voor weergavedoeleinden. |
| `description` | (Optioneel) Een beschrijving van het label voor verdere context. |

**Antwoord**

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

In deze handleiding wordt ingegaan op het gebruik van het `/labels` eindpunt in de Dienst API van het Beleid. Voor stappen op hoe te om etiketten op datasets en gebieden toe te passen, verwijs naar [API-handleiding voor gegevenssetlabels](../labels/dataset-api.md).
