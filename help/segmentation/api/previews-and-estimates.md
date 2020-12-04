---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;previews;estimates;previews and estimates;estimates and previews;api;API;
solution: Experience Platform
title: Voorvertoningen en schattingen van eindpunten
topic: developer guide
description: Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen in Adobe Experience Platform gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het verwachte publiek isoleert.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---


# Voorvertoningen en schattingen van eindpunten

Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen binnen gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het verwachte publiek isoleert. [!DNL Adobe Experience Platform] **De voorproeven** verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, toelatend u om de resultaten tegen te vergelijken wat u verwacht. **Schattingen** verschaffen statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval en de standaardafwijking voor fouten.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Voordat u verdergaat, bekijkt u eerst de gids [](./getting-started.md) Aan de slag voor belangrijke informatie die u moet weten om oproepen naar de API met succes te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Hoe schattingen worden gegenereerd

De manier waarop gegevensbemonstering wordt geactiveerd, is afhankelijk van de innamemethode.

Voor batch-opname wordt de profielopslag automatisch elke 15 minuten gescand om te zien of een nieuwe batch is opgenomen sinds de laatste samplingtaak is uitgevoerd. Als dat het geval is, wordt de profielopslag gescand om te zien of is er minstens een 5% verandering in het aantal verslagen. Als aan deze voorwaarden wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

Voor het stromen opname, wordt de profielopslag automatisch gescand elk uur om te zien of is er minstens een 5% verandering in het aantal verslagen geweest. Als aan deze voorwaarde wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

De voorbeeldgrootte van de scan is afhankelijk van het totale aantal entiteiten in de profielopslag. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

>[!NOTE]
>
>De schattingen duren over het algemeen 10 tot 15 seconden om te werken, te beginnen met een ruwe schatting en verfijning naarmate meer records worden gelezen.

## Een nieuwe voorvertoning maken {#create-preview}

U kunt een nieuwe voorproef tot stand brengen door een verzoek van de POST aan het `/preview` eindpunt te doen.

>[!NOTE]
>
>Er wordt automatisch een geschatte taak gemaakt wanneer een voorbeeldtaak wordt gemaakt. Deze twee taken delen dezelfde id.

**API-indeling**

```http
POST /preview
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `predicateExpression` | De uitdrukking PQL om de gegevens door te vragen. |
| `predicateType` | Het predikaat type voor de vraaguitdrukking onder `predicateExpression`. Momenteel is de enige toegestane waarde voor deze eigenschap `pql/text`. |
| `predicateModel` | De naam van het [!DNL Experience Data Model] (XDM)-schema waarop de profielgegevens zijn gebaseerd. |

**Antwoord**

Een succesvol antwoord retourneert HTTP-status 201 (Gemaakt) met details van de zojuist gemaakte voorvertoning.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `state` | De huidige status van de voorvertoningstaak. Bij het maken wordt de status &quot;NEW&quot; gebruikt. Vervolgens wordt de status &quot;RUNNING&quot; gebruikt totdat de verwerking is voltooid, waarna de status &quot;RESULT_READY&quot; of &quot;FAILED&quot; wordt. |
| `previewId` | De id van de voorvertoningstaak die voor opzoekdoeleinden moet worden gebruikt bij het weergeven van een schatting of voorvertoning, zoals in de volgende sectie wordt beschreven. |

## De resultaten van een specifieke voorvertoning ophalen {#get-preview}

U kunt gedetailleerde informatie over een specifieke voorproef terugwinnen door een verzoek van de GET aan het `/preview` eindpunt te doen en voorproef identiteitskaart in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | De `previewId` waarde van de voorvertoning die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over de opgegeven voorvertoning.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `results` | Een lijst met entiteit-id&#39;s, samen met de bijbehorende id&#39;s. Met de opgegeven koppelingen kunt u de opgegeven entiteiten opzoeken met de [[!DNL Profile Access API]](../../profile/api/entities.md)instructies. |

## De resultaten van een specifieke geschatte taak ophalen {#get-estimate}

Zodra u een voorproefbaan hebt gecreeerd, kunt u zijn `previewId` in de weg van een verzoek van de GET aan het `/estimate` eindpunt gebruiken om statistische informatie over de segmentdefinitie, met inbegrip van geprojecteerde publieksgrootte, betrouwbaarheidsinterval, en foutenstandaardafwijking te bekijken.

**API-indeling**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | Een geschatte taak wordt alleen geactiveerd wanneer een voorvertoningstaak wordt gemaakt en de twee taken dezelfde id-waarde delen voor opzoekdoeleinden. Dit is met name de `previewId` waarde die wordt geretourneerd toen de voorvertoningstaak werd gemaakt. |

**Verzoek**

Het volgende verzoek wint de resultaten van een specifieke ramingstaak terug.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP status 200 met details van de geschatte taak.

```json
{
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `state` | De huidige status van de voorvertoningstaak. Zal &quot;RUNNING&quot;zijn tot de verwerking volledig is, waarbij het &quot;RESULT_READY&quot;of &quot;FAILED&quot;wordt. |
| `_links.preview` | Wanneer de huidige status van de voorvertoningstaak &quot;RESULT_READY&quot; is, geeft dit kenmerk een URL om de schatting weer te geven. |

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u met voorvertoningen en schattingen kunt werken. Lees voor meer informatie over de andere [!DNL Segmentation Service] API-eindpunten het overzicht [van de ontwikkelaar van de](./overview.md)Segmentatieservice.