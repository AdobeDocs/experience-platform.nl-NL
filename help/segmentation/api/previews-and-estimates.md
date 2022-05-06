---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;voorvertoningen;schattingen;voorvertoningen en ramingen;schattingen en voorvertoningen;api;API;
solution: Experience Platform
title: Voorvertoningen en schattingen van API-eindpunten
topic-legacy: developer guide
description: Terwijl segmentdefinitie wordt ontwikkeld, kunt u met de rastergereedschappen en voorvertoningsgereedschappen in Adobe Experience Platform informatie op overzichtsniveau weergeven, zodat u zeker weet dat u het verwachte publiek isoleert.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 1%

---

# Voorvertoningen en schattingen van eindpunten

Terwijl u een segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen in Adobe Experience Platform gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het publiek dat u verwacht, isoleert.

* **Voorvertoningen** U kunt gepagineerde lijsten met kwalificerende profielen voor een segmentdefinitie opgeven, zodat u de resultaten kunt vergelijken met wat u verwacht.

* **Schattingen** statistische informatie verstrekken over een segmentdefinitie, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval, en fout standaardafwijking.

>[!NOTE]
>
>Als u toegang wilt tot vergelijkbare gegevens met betrekking tot gegevens in realtime klantprofiel, zoals het totale aantal profielfragmenten en samengevoegde profielen binnen specifieke naamruimten of het profielgegevensbestand als geheel, raadpleegt u de [profielvoorbeeld (voorbeeldstatus), eindhulplijn](../../profile/api/preview-sample-status.md), onderdeel van de ontwikkelaarsgids voor profiel API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Hoe schattingen worden gegenereerd

Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 5% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. De manier waarop gegevensbemonstering wordt gestart, hangt af van de wijze van inname:

* **Batchopname:** Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal bij te werken als aan de drempel van 5% voor verhogen of verlagen is voldaan.
* **Streaming opname:** Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om de telling bij te werken.

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

U kunt een nieuwe voorvertoning maken door een POST aan te vragen bij de `/preview` eindpunt.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `predicateExpression` | De uitdrukking PQL om de gegevens door te vragen. |
| `predicateType` | Het predikentype voor de vraaguitdrukking onder `predicateExpression`. Momenteel is de enige toegestane waarde voor deze eigenschap: `pql/text`. |
| `predicateModel` | De naam van de [!DNL Experience Data Model] (XDM) schema-klasse waarop de profielgegevens zijn gebaseerd. |
| `graphType` | Het grafiektype waarvan u de cluster wilt ophalen. De ondersteunde waarden zijn: `none` (voert geen identiteitsstitching uit) en `pdg` (Er wordt identiteitsstitching uitgevoerd op basis van uw persoonlijke identiteitsgrafiek). |

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

U kunt gedetailleerde informatie over een specifieke voorvertoning opvragen door een GET-aanvraag in te dienen bij de `/preview` en het verstrekken van voorproef identiteitskaart in de verzoekweg.

**API-indeling**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | De `previewId` De waarde van de voorvertoning die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `results` | Een lijst met entiteit-id&#39;s, samen met de bijbehorende id&#39;s. Met de opgegeven koppelingen kunt u de opgegeven entiteiten opzoeken met de [API-eindpunt voor profieltoegang](../../profile/api/entities.md). |

## De resultaten van een specifieke geschatte taak ophalen {#get-estimate}

Als u eenmaal een voorbeeldtaak hebt gemaakt, kunt u de bijbehorende taak gebruiken `previewId` op het pad van een verzoek van de GET aan de `/estimate` eindpunt om statistische informatie over de segmentdefinitie, met inbegrip van geprojecteerde publieksgrootte, betrouwbaarheidsinterval, en fout standaardafwijking te bekijken.

**API-indeling**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | Een geschatte taak wordt alleen geactiveerd wanneer een voorvertoningstaak wordt gemaakt en de twee taken dezelfde id-waarde delen voor opzoekdoeleinden. Dit is met name de `previewId` waarde die wordt geretourneerd bij het maken van de voorvertoningstaak. |

**Verzoek**

Het volgende verzoek wint de resultaten van een specifieke ramingstaak terug.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP status 200 met details van de geschatte taak.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Een array met objecten die het aantal profielen in het segment weergeeft, uitgesplitst naar naamruimte van identiteit. Het totale aantal profielen per naamruimte (door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan de metrische waarde van het aantal profielen, omdat één profiel aan meerdere naamruimten kan worden gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd. |
| `state` | De huidige status van de voorvertoningstaak. De status wordt ‘UITGEVOERD’ totdat de verwerking is voltooid, waarna de status ‘RESULT_READY’ of ‘FAILED’ wordt. |
| `_links.preview` | Wanneer de `state` is &quot;RESULT_READY&quot;, verstrekt dit gebied een URL om de schatting te bekijken. |

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u een beter inzicht in hoe u met voorvertoningen en schattingen werkt met de segmentatie-API. Ga naar de [profielvoorvertoning (`/previewsamplestatus`) eindpunthulplijn](../../profile/api/preview-sample-status.md).
