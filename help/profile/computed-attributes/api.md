---
title: Computed Attributes API Endpoint
description: Leer hoe u berekende kenmerken kunt maken, weergeven, bijwerken en verwijderen met de realtime-API voor klantprofiel.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# API-eindpunt van berekende kenmerken

>[!IMPORTANT]
>
>De toegang tot de API is beperkt. Neem contact op met de Adobe Support voor meer informatie over het verkrijgen van toegang tot de API voor berekende kenmerken.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Deze handleiding bevat voorbeeld-API-aanroepen voor het uitvoeren van standaard-CRUD-bewerkingen met behulp van het `/attributes` -eindpunt.

Meer over gegevens verwerkte attributen leren, gelieve te beginnen door [ gegevens verwerkt attributenoverzicht ](overview.md) te lezen.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [ Real-Time API van het Profiel van de Klant ](https://www.adobe.com/go/profile-apis-en).

Alvorens verder te gaan, te herzien gelieve [ Profiel API die begonnen gids ](../api/getting-started.md) voor verbindingen aan geadviseerde documentatie wordt begonnen, een gids aan het lezen van de steekproefAPI vraag die in dit document verschijnen, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

Raadpleeg ook de documentatie bij de volgende service:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
   - {de Registratie van 0} Schema die begonnen gids [&#128279;](../../xdm/api/getting-started.md#know-your-tenant_id) wordt: De informatie over uw `{TENANT_ID}`, die in reacties door deze gids verschijnt, wordt verstrekt.

## Een lijst met berekende kenmerken ophalen {#list}

U kunt een lijst van alle gegevens verwerkte attributen voor uw organisatie terugwinnen door een verzoek van de GET aan het `/attributes` eindpunt te doen.

**API formaat**

Het `/attributes` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle gegevens verwerkte attributen beschikbaar voor uw organisatie worden teruggewonnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

De volgende queryparameters kunnen worden gebruikt bij het ophalen van een lijst met berekende kenmerken:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `limit` | Een parameter die het maximumaantal punten specificeert die als deel van de reactie worden teruggekeerd. De minimumwaarde van deze parameter is 1 en de maximumwaarde is 40. Als deze parameter niet is opgenomen, worden standaard 20 items geretourneerd. | `limit=20` |
| `offset` | Een parameter die het aantal punten specificeert om over te slaan alvorens de punten terug te keren. | `offset=5` |
| `sortBy` | Een parameter die de orde specificeert waarin de teruggekeerde punten worden gesorteerd. Beschikbare opties zijn `name` , `status` , `updateEpoch` en `createEpoch` . U kunt ook kiezen of u in oplopende of aflopende volgorde wilt sorteren door geen `-` vóór de sorteeroptie op te nemen of op te nemen. Standaard worden de items door `updateEpoch` in aflopende volgorde gesorteerd. | `sortBy=name` |
| `property` | Een parameter waarmee u op verschillende berekende kenmerkvelden kunt filteren. Tot de ondersteunde eigenschappen behoren `name` , `createEpoch` , `mergeFunction.value` , `updateEpoch` en `status` . De ondersteunde bewerkingen zijn afhankelijk van de vermelde eigenschap. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Verzoek**

Het volgende verzoek wint de laatste drie gegevens verwerkte attributen terug die in uw organisatie werden bijgewerkt.

+++ Een voorbeeldverzoek om een lijst met berekende kenmerken op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 200 met een lijst van de laatste 3 bijgewerkte berekende kenmerken die bij uw organisatie en sandbox horen.

+++ Een voorbeeldreactie voor het ophalen van een lijst met berekende kenmerken.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `_links` | Een object dat de pagineringsinformatie bevat die nodig is voor toegang tot de laatste pagina met resultaten, de volgende pagina met resultaten, de vorige pagina met resultaten of de huidige pagina met resultaten. |
| `computedAttributes` | Een array die de berekende kenmerken bevat op basis van de queryparameters. Meer informatie over de gegevens verwerkte attributenserie kan in [ worden gevonden wint een specifieke gegevens verwerkte attributensectie ](#get) terug. |
| `_page` | Een object dat metagegevens bevat over de geretourneerde resultaten. Dit omvat informatie over de huidige verschuiving, het aantal geretourneerde berekende kenmerken, het totale aantal berekende kenmerken en de limiet van geretourneerde berekende kenmerken. |

+++

## Een berekend kenmerk maken {#create}

Om een gegevens verwerkt attribuut tot stand te brengen, begin door een verzoek van de POST aan het `/attributes` eindpunt met een verzoeklichaam te doen dat de details van het gegevens verwerkte attribuut bevat dat u wenst om tot stand te brengen.

**API formaat**

```http
POST /attributes
```

**Verzoek**

+++ Een voorbeeldverzoek om een nieuw berekend kenmerk te maken.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van het berekende kenmerkveld, als een tekenreeks. De naam van het berekende kenmerk kan alleen bestaan uit alfanumerieke tekens zonder spaties of onderstrepingstekens. Deze waarde **moet** onder alle gegevens verwerkte attributen uniek zijn. Deze naam is de beste manier om een camelCase-versie van de instructie `displayName` te gebruiken. |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat dit anderen binnen uw organisatie helpt te bepalen welk kenmerk correct moet worden berekend. |
| `displayName` | De weergavenaam voor het berekende kenmerk. Dit is de naam die wordt weergegeven wanneer u uw berekende kenmerken weergeeft in de gebruikersinterface van Adobe Experience Platform. |
| `expression` | Een object dat de query-expressie vertegenwoordigt van het berekende kenmerk dat u probeert te maken. |
| `expression.type` | Het type van de expressie. Momenteel wordt alleen PQL ondersteund. |
| `expression.format` | De indeling van de expressie. Momenteel wordt alleen `pql/text` ondersteund. |
| `expression.value` | De waarde van de expressie. |
| `keepCurrent` | Een Booleaanse waarde die bepaalt of de waarde van het berekende kenmerk up-to-date wordt gehouden met de functie voor snel vernieuwen. Deze waarde moet momenteel worden ingesteld op `false` . |
| `duration` | Een object dat de terugzoekperiode voor het berekende kenmerk vertegenwoordigt. De terugkijkperiode vertegenwoordigt hoe ver terug kan worden gezocht om de gegevens verwerkte attributen te berekenen. |
| `duration.count` | Een getal dat de duur van de terugzoekperiode vertegenwoordigt. De mogelijke waarden zijn afhankelijk van de waarde van het veld `duration.unit` . <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Een tekenreeks die de tijdseenheid vertegenwoordigt die voor de terugzoekperiode wordt gebruikt. Mogelijke waarden zijn: `HOURS` , `DAYS` , `WEEKS` en `MONTHS` . |
| `status` | De status van het berekende kenmerk. Mogelijke waarden zijn `DRAFT` en `NEW` . |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met informatie over het nieuwe berekende kenmerk.

+++ Een voorbeeldreactie bij het maken van een nieuw berekend kenmerk.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De door het systeem gegenereerde id van het nieuwe berekende kenmerk. |
| `status` | De status van het berekende kenmerk. Dit kan `DRAFT` of `NEW` zijn. |
| `createEpoch` | De tijd waarop het berekende attribuut werd gecreeerd, in seconden. |
| `updateEpoch` | Het tijdstip waarop het berekende kenmerk voor het laatst is bijgewerkt, in seconden. |
| `createdBy` | De id van de gebruiker die het berekende kenmerk heeft gemaakt. |

+++

## Hiermee wordt een specifiek berekend kenmerk opgehaald {#get}

U kunt gedetailleerde informatie over een specifiek gegevens verwerkt attribuut terugwinnen door een verzoek van de GET aan het `/attributes` eindpunt te doen en identiteitskaart van de gegevens verwerkte attributen te verstrekken u in de verzoekweg wenst terug te winnen.

**API formaat**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Verzoek**

+++ Een steekproefverzoek om een specifiek gegevens verwerkt attribuut terug te winnen.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over het opgegeven berekende kenmerk.

+++ Een voorbeeldreactie bij het ophalen van een specifiek berekend kenmerk.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde id die kan worden gebruikt voor het verwijzen naar het berekende kenmerk tijdens andere API-bewerkingen. |
| `type` | Een tekenreeks die aangeeft dat het geretourneerde object een berekend kenmerk is. |
| `name` | The name for the computed attribute. |
| `displayName` | De weergavenaam voor het berekende kenmerk. Dit is de naam die wordt weergegeven wanneer u uw berekende kenmerken weergeeft in de gebruikersinterface van Adobe Experience Platform. |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat dit anderen binnen uw organisatie helpt te bepalen welk kenmerk correct moet worden berekend. |
| `imsOrgId` | De id van de organisatie waartoe het berekende kenmerk behoort. |
| `sandbox` | Het sandboxobject bevat details van de sandbox waarin het berekende kenmerk is geconfigureerd. Deze informatie wordt getekend vanuit de sandboxheader die in de aanvraag wordt verzonden. Voor meer informatie, te zien gelieve het [ overzicht van zandbakken ](../../sandboxes/home.md). |
| `path` | The `path` to the computed attribute. |
| `keepCurrent` | Een Booleaanse waarde die bepaalt of de waarde van het berekende kenmerk up-to-date wordt gehouden met de functie voor snel vernieuwen. |
| `expression` | Een object dat de expressie van het berekende kenmerk bevat. |
| `mergeFunction` | Een object dat de samenvoegfunctie voor het berekende kenmerk bevat. Deze waarde is gebaseerd op de corresponderende aggregatieparameter binnen de berekende expressie van het kenmerk. Mogelijke waarden zijn `SUM` , `MIN` , `MAX` en `MOST_RECENT` . |
| `status` | De status van het berekende kenmerk. Dit kan een van de volgende waarden zijn: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` of `DISABLED` . |
| `schema` | Een object dat informatie bevat over het schema waarin de expressie wordt geëvalueerd. Momenteel wordt alleen `_xdm.context.profile` ondersteund. |
| `lastEvaluationTs` | Een tijdstempel die aangeeft wanneer het berekende kenmerk voor het laatst is geëvalueerd. |
| `createEpoch` | De tijd waarop het berekende attribuut werd gecreeerd, in seconden. |
| `updateEpoch` | Het tijdstip waarop het berekende kenmerk voor het laatst is bijgewerkt, in seconden. |
| `createdBy` | De id van de gebruiker die het berekende kenmerk heeft gemaakt. |

+++

## Een specifiek berekend kenmerk verwijderen {#delete}

U kunt een specifiek gegevens verwerkt attribuut schrappen door een verzoek van DELETE aan het `/attributes` eindpunt te doen en identiteitskaart van de gegevens verwerkte attributen te verstrekken u in de verzoekweg wenst te schrappen.

>[!IMPORTANT]
>
>Het schrappingsverzoek kan slechts worden gebruikt om gegevens verwerkte attributen te schrappen die een status van **ontwerp** (`DRAFT`) hebben. Dit eindpunt **kan** niet worden gebruikt om gegevens verwerkte attributen in een andere staat te schrappen.

**API formaat**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | De `id` -waarde van het berekende kenmerk dat u wilt verwijderen. |

**Verzoek**

+++ Een voorbeeldverzoek om een berekend kenmerk te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 202 met details van het verwijderde berekende kenmerk.

+++ Een voorbeeldreactie bij het verwijderen van een berekend kenmerk.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Een specifiek berekend kenmerk bijwerken

U kunt een specifiek gegevens verwerkt attribuut bijwerken door een verzoek van PATCH aan het `/attributes` eindpunt te doen en identiteitskaart van de gegevens verwerkte attributen te verstrekken u wenst om in de verzoekweg bij te werken.

>[!IMPORTANT]
>
>Wanneer u een berekend kenmerk bijwerkt, kunnen alleen de volgende velden worden bijgewerkt:
>
>- Als de huidige status `NEW` is, kan de status alleen worden gewijzigd in `DISABLED` .
>- Als de huidige status `DRAFT` is, kunt u de waarden van de volgende velden wijzigen: `name`, `description`, `keepCurrent`, `expression` en `duration` . U kunt de status ook wijzigen van `DRAFT` in `NEW` . Wijzigingen in door het systeem gegenereerde velden, zoals `mergeFunction` of `path` , retourneren een fout.
>- Als de huidige status `PROCESSING` of `PROCESSED` is, kan de status alleen worden gewijzigd in `DISABLED` .

**API formaat**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | De `id` -waarde van het berekende kenmerk dat u wilt bijwerken. |

**Verzoek**

In de volgende aanvraag wordt de status van het berekende kenmerk van `DRAFT` tot `NEW` bijgewerkt.

+++ Een voorbeeldverzoek om een berekend kenmerk bij te werken.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met informatie over het zojuist bijgewerkte berekende kenmerk.

+++ Een voorbeeldreactie bij het bijwerken van een berekend kenmerk.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Volgende stappen

Nu u de grondbeginselen van berekende attributen hebt geleerd, bent u klaar om te beginnen bepalend hen voor uw organisatie. Leren hoe te om gegevens verwerkte attributen in het Experience Platform UI te gebruiken, te lezen gelieve de [ gegevens verwerkte gids UI van attributen ](./ui.md).
