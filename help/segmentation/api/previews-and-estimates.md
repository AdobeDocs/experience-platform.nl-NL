---
solution: Experience Platform
title: Voorvertoningen en schattingen van API-eindpunten
description: Terwijl segmentdefinitie wordt ontwikkeld, kunt u met de rastergereedschappen en voorvertoningsgereedschappen in Adobe Experience Platform informatie op overzichtsniveau weergeven, zodat u zeker weet dat u het verwachte publiek isoleert.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: d9fc1fa6a1bbc6b13b2600a5ec9400a0b488056a
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Voorvertoningen en schattingen van eindpunten

Terwijl u een segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen in Adobe Experience Platform gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het publiek dat u verwacht, isoleert.

* **Voorproeven** verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, toestaand u om de resultaten tegen te vergelijken wat u verwacht.

* **Schattingen** verstrekken statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval, en fout standaardafwijking.

>[!NOTE]
>
>Om tot gelijkaardige metriek met betrekking tot de gegevens van het Profiel van de Klant in real time, zoals het totale aantal profielfragmenten en samengevoegde profielen binnen specifieke namespaces of de de gegevensopslag van het Profiel als geheel toegang te hebben, gelieve te verwijzen naar de [ gids van de profielvoorproef (de status van de voorproefsteekproef) ](../../profile/api/preview-sample-status.md), een deel van de de ontwikkelaarsgids van het Profiel API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Hoe schattingen worden gegenereerd

Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 5% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. De manier waarop gegevensbemonstering wordt gestart, hangt af van de wijze van inname:

* **Inname van de Partij:** voor partijingestie, binnen 15 minuten van met succes het opnemen van een partij in de opslag van het Profiel, als de 3% verhoging of dalingsdrempel wordt ontmoet, wordt een baan in werking gesteld om de telling bij te werken.
* **Streaming opname:** voor het stromen gegevenswerkschema&#39;s, wordt een controle gedaan op een uurbasis om te bepalen als de 3% verhoging of dalingsdrempel is voldaan aan. Als dit het geval is, wordt er automatisch een taak geactiveerd om de telling bij te werken.

De voorbeeldgrootte van de scan is afhankelijk van het totale aantal entiteiten in de profielopslag. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in de profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

>[!NOTE]
>
>De schattingen duren over het algemeen 10 tot 15 seconden om te werken, te beginnen met een ruwe schatting en verfijning naarmate meer records worden gelezen.

## Een nieuwe voorvertoning maken {#create-preview}

U kunt een nieuwe voorvertoning maken door een POST-aanvraag in te dienen bij het eindpunt van `/preview` .

>[!NOTE]
>
>Er wordt automatisch een geschatte taak gemaakt wanneer een voorbeeldtaak wordt gemaakt. Deze twee taken delen dezelfde id.

**API formaat**

```http
POST /preview
```

**Verzoek**

+++ Een voorbeeldverzoek om een voorvertoning te maken.

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
| `predicateExpression` | De PQL-expressie waarmee de gegevens worden opgevraagd. |
| `predicateType` | Het predikaat type voor de vraaguitdrukking onder `predicateExpression`. Momenteel is `pql/text` de enige toegestane waarde voor deze eigenschap. |
| `predicateModel` | De naam van de schemaklasse [!DNL Experience Data Model] (XDM) waarop de profielgegevens zijn gebaseerd. |
| `graphType` | Het grafiektype waarvan u de cluster wilt ophalen. De ondersteunde waarden zijn `none` (voert geen identiteitsstitching uit) en `pdg` (voert identiteitsstitching uit op basis van uw persoonlijke identiteitsgrafiek). |

+++

**Reactie**

Een succesvol antwoord retourneert HTTP-status 201 (Gemaakt) met details van de zojuist gemaakte voorvertoning.

+++ Een voorbeeldreactie bij het maken van een voorvertoning.

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
| `state` | De huidige status van de voorvertoningstaak. Bij het maken wordt de status &quot;NIEUW&quot; gebruikt. Vervolgens wordt de status &quot;RUNNING&quot; gebruikt totdat de verwerking is voltooid, waarna de status &quot;RESULT_READY&quot; of &quot;FAILED&quot; wordt. |
| `previewId` | De id van de voorvertoningstaak die voor opzoekdoeleinden moet worden gebruikt bij het weergeven van een schatting of voorvertoning, zoals in de volgende sectie wordt beschreven. |

+++

## De resultaten van een specifieke voorvertoning ophalen {#get-preview}

U kunt gedetailleerde informatie over een specifieke voorvertoning ophalen door een GET-aanvraag in te dienen bij het `/preview` -eindpunt en de voorbeeld-id op te geven in het aanvraagpad.

**API formaat**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | De `previewId` -waarde van de voorvertoning die u wilt ophalen. |

**Verzoek**

+++ Een voorbeeldverzoek om een voorvertoning op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

+++ Een voorbeeldreactie bij het ophalen van een voorvertoning.

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
| `results` | Een lijst met entiteit-id&#39;s, samen met de bijbehorende id&#39;s. De verstrekte verbindingen kunnen worden gebruikt om de gespecificeerde entiteiten omhoog te kijken, gebruikend het [ API eindpunt van de profieltoegang ](../../profile/api/entities.md). |

+++

## De resultaten van een specifieke geschatte taak ophalen {#get-estimate}

Als u een voorvertoningstaak hebt gemaakt, kunt u de `previewId` ervan gebruiken in het pad van een GET-aanvraag naar het `/estimate` -eindpunt om statistische informatie weer te geven over de segmentdefinitie, zoals de geprojecteerde publieksgrootte, het betrouwbaarheidsinterval en de standaardafwijking voor fouten.

**API formaat**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{PREVIEW_ID}` | Een geschatte taak wordt alleen geactiveerd wanneer een voorvertoningstaak wordt gemaakt en de twee taken dezelfde id-waarde delen voor opzoekdoeleinden. Dit is met name de `previewId` -waarde die wordt geretourneerd toen de voorvertoningstaak werd gemaakt. |

**Verzoek**

Het volgende verzoek wint de resultaten van een specifieke ramingstaak terug.

+++ Een voorbeeldverzoek om een geschatte taak op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP status 200 met details van de geschatte taak.

+++ Een voorbeeldreactie bij het ophalen van een geschatte taak.

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
| `estimatedNamespaceDistribution` | Een array met objecten die het aantal profielen binnen de segmentdefinitie weergeeft, uitgesplitst naar naamruimte van identiteit. Het totale aantal profielen per naamruimte (door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan de metrische waarde van het aantal profielen, omdat één profiel aan meerdere naamruimten kan worden gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd. |
| `state` | De huidige status van de voorvertoningstaak. De status wordt ‘UITGEVOERD’ totdat de verwerking is voltooid, waarna de status ‘RESULT_READY’ of ‘FAILED’ wordt. |
| `_links.preview` | Wanneer `state` &quot;RESULT_READY&quot; is, verstrekt dit gebied een URL om de schatting te bekijken. |

+++

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u een beter inzicht in hoe u met voorvertoningen en schattingen werkt met de segmentatie-API. Leer hoe te om tot metriek met betrekking tot uw gegevens van het Profiel van de Klant in real time, zoals het totale aantal profielfragmenten en samengevoegde profielen binnen specifieke namespaces of de gegevensopslag van het Profiel als geheel toegang te hebben, gelieve de [ voorproef van het profielmonster (`/previewsamplestatus`) eindpuntgids ](../../profile/api/preview-sample-status.md) te bezoeken.
