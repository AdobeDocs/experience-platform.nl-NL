---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een segment maken
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---


# Een segment maken

Dit document biedt een zelfstudie voor het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie met de [segmentatie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Voor informatie over hoe te om segmenten te bouwen gebruikend het gebruikersinterface, te zien gelieve de gids [van de Bouwer van het](../ui/overview.md)Segment.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het maken van doelsegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Segmenteringsservice](../home.md)Adobe Experience Platform: Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segmentdefinitie ontwikkelen

De eerste stap in segmentatie is een segment te bepalen dat in een constructie wordt vertegenwoordigd genoemd een **segmentdefinitie**. Een segmentdefinitie is een object dat een query inkapselt die is geschreven in PQL (Profile Query Language). Dit object wordt ook wel een **PQL-voorspelling** genoemd. PQL bepaalt de regels voor het segment die op voorwaarden met betrekking tot om het even welke verslag of tijdreeksgegevens worden gebaseerd u aan het Profiel van de Klant in real time verstrekt. Raadpleeg de [PQL-handleiding](../pql/overview.md) voor meer informatie over het schrijven van PQL-query&#39;s.

U kunt een nieuwe segmentdefinitie tot stand brengen door een POST- verzoek aan het `/segment/definitions` eindpunt in Real-time API van het Profiel van de Klant te doen. Het volgende voorbeeld schetst hoe te om een definitieverzoek te formatteren, die welke informatie wordt vereist opdat een segment met succes wordt bepaald.

Segmentdefinities kunnen op twee manieren worden geëvalueerd: batchsegmentatie en streamingsegmentatie. De segmentatie van de partij evalueert segmenten die op een vooraf ingesteld programma worden gebaseerd of wanneer de evaluatie manueel teweeggebracht wordt, terwijl het stromen segmentatie segmenten evalueert zodra de gegevens in Platform worden opgenomen. Deze zelfstudie gebruikt **batchsegmentatie**. Lees het [overzicht over streamingsegmentatie](../api/streaming-segmentation.md)voor meer informatie over streamingsegmentatie.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe segmentdefinitie voor een schema genoemd &quot;MyProfile&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Eigenschap | Beschrijving |
| --------- | ------------ | 
| `name` | **Vereist.** Een unieke naam waarmee naar het segment moet worden verwezen. |
| `schema` | **Vereist.** Het schema dat is gekoppeld aan de entiteiten in het segment. Bestaat uit een `id` of een `name` veld. |
| `expression` | **Vereist.** Een entiteit die veldinformatie over de segmentdefinitie bevat. |
| `expression.type` | Geeft het expressietype aan. Momenteel wordt alleen &quot;PQL&quot; ondersteund. |
| `expression.format` | Geeft de structuur van de expressie in waarde aan. Momenteel wordt de volgende indeling ondersteund: <ul><li>`pql/text`: Een tekstuele representatie van een segmentdefinitie, volgens de gepubliceerde PQL-grammatica.  Bijvoorbeeld, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Een expressie die overeenkomt met het type dat wordt aangegeven in `expression.format`. |
| `mergePolicyId` | De id van het samenvoegbeleid dat moet worden gebruikt voor de geëxporteerde gegevens. Lees voor meer informatie het configuratiedocument [voor](../../profile/api/merge-policies.md)samenvoegingsbeleid. |
| `description` | Een door mensen leesbare beschrijving van de definitie. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde segmentdefinitie, met inbegrip van zijn systeem-geproduceerde, read-only `id` terug die later in dit leerprogramma zal worden gebruikt.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Een publiek schatten en voorvertonen {#estimate-and-preview-an-audience}

Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsprogramma&#39;s in Real-time klantprofiel gebruiken om informatie op overzichtsniveau weer te geven om ervoor te zorgen dat u het verwachte publiek isoleert. Schattingen verschaffen statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte en het betrouwbaarheidsinterval. De voorproeven verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht.

Door uw publiek te schatten en te previewing, kunt u uw predikaten testen en optimaliseren PQL tot zij een wenselijk resultaat veroorzaken, waar zij dan in een bijgewerkte segmentdefinitie kunnen worden gebruikt.

Er zijn twee vereiste stappen om een voorvertoning van uw segment te bekijken of een schatting van uw segment te krijgen:

1. [Een voorbeeldtaak maken](#create-a-preview-job)
2. [Raming of voorvertoning](#view-an-estimate-or-preview) weergeven met de id van de voorvertoningstaak

### Hoe schattingen worden gegenereerd

Gegevenssteekproeven worden gebruikt om segmenten te evalueren en het aantal kwalificerende profielen te schatten. De nieuwe gegevens worden geladen in geheugen elke ochtend (tussen 12AM-2AM PT, die 7-9AM UTC is), en alle segmenteringsvragen worden geschat gebruikend de steekproefgegevens van die dag. Bijgevolg zullen nieuwe toegevoegde velden of verzamelde aanvullende gegevens de volgende dag in schattingen worden weergegeven.

De voorbeeldgrootte is afhankelijk van het totale aantal entiteiten in het profielarchief. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

De schattingen lopen over het algemeen over 10-15 seconden, beginnend met een ruwe schatting en raffinage aangezien meer verslagen worden gelezen.

### Een voorbeeldtaak maken

U kunt een nieuwe voorproefbaan tot stand brengen door een POST- verzoek aan het `/preview` eindpunt te doen.

**API-indeling**

```http
POST /preview
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe voorbeeldtaak gemaakt. Het verzoeklichaam bevat de vraaginformatie met betrekking tot het segment.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `predicateExpression` | De uitdrukking PQL om de gegevens door te vragen. |
| `predicateModel` | De naam van het XDM-schema waarop de profielgegevens zijn gebaseerd. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe voorvertoningstaak, inclusief de id en de huidige verwerkingsstatus.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `state` | De huidige status van de voorvertoningstaak. Het zal in de &quot;RUNNING&quot;staat zijn tot de verwerking volledig is, waarbij het &quot;RESULT_READY&quot;of &quot;FAILED&quot;wordt. |
| `previewId` | De id van de voorvertoningstaak die voor opzoekdoeleinden moet worden gebruikt bij het weergeven van een schatting of voorvertoning, zoals in de volgende sectie wordt beschreven. |

### Een schatting of voorvertoning weergeven

De schattings- en voorvertoningsprocessen worden asynchroon uitgevoerd, omdat verschillende query&#39;s verschillende tijdsduur kunnen duren. Nadat een query is gestart, kunt u API-aanroepen gebruiken om de huidige status van de schatting of voorvertoning op te halen terwijl deze vordert.

Met de realtime-API voor klantprofiel kunt u de huidige status van een voorbeeldtaak opzoeken aan de hand van de bijbehorende id. Als de status &quot;RESULT_READY&quot; is, kunt u de resultaten bekijken. Afhankelijk van het feit of u een schatting of voorvertoning wilt bekijken, heeft elk een eigen eindpunt in de API. Hieronder vindt u voorbeelden voor beide.

### Een schatting weergeven

**API-indeling**

```http
GET /estimate/{PREVIEW_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{PREVIEW_ID}` | De id van de voorbeeldtaak die u wilt weergeven. |

**Verzoek**

Het volgende verzoek wint een schatting terug, gebruikend de `previewId` gecreeerde in de vorige stap.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert de details van de schatting.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `state` | De huidige status van de voorvertoningstaak. Zal &quot;RUNNING&quot;zijn tot de verwerking volledig is, waarbij het &quot;RESULT_READY&quot;of &quot;MISLUKT&quot;wordt. |
| `_links.preview` | Wanneer de huidige status van de voorvertoningstaak &quot;RESULT_READY&quot; is, geeft dit kenmerk een URL om de schatting weer te geven. |

### Een voorvertoning weergeven

**API-indeling**

```http
GET /preview/{PREVIEW_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{PREVIEW_ID}` | De id van de voorbeeldtaak die u wilt weergeven. |

**Verzoek**

Met het volgende verzoek wordt een voorvertoning opgehaald, waarbij de in de vorige stap `previewId` gemaakte methode wordt gebruikt.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als de reactie succesvol was, worden details van de voorvertoning geretourneerd.

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
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Volgende stappen

Nadat u de segmentdefinitie hebt ontwikkeld, getest en opgeslagen, kunt u een segmenttaak maken om een publiek op te bouwen met de Real-Time Customer Profile API. Zie de zelfstudie over het [evalueren van en de toegang tot van segmentresultaten](./evaluate-a-segment.md) voor gedetailleerde stappen over hoe te om dit te verwezenlijken.