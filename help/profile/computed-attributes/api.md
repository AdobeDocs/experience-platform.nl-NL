---
title: Computed Attributes API Endpoint
description: Leer hoe u berekende kenmerken kunt maken, weergeven, bijwerken en verwijderen met de realtime-API voor klantprofiel.
badge: "Bèta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# API-eindpunt van berekende kenmerken

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.
>
>Bovendien is de toegang tot de API beperkt. Neem contact op met de Adobe Support voor meer informatie over het verkrijgen van toegang tot de API voor berekende kenmerken.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Deze handleiding bevat voorbeeld-API-aanroepen voor het uitvoeren van standaard-CRUD-bewerkingen met behulp van de `/attributes` eindpunt.

Als u meer wilt weten over berekende kenmerken, leest u eerst de [overzicht van berekende kenmerken](overview.md).

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [Real-Time Customer Profile API](https://www.adobe.com/go/profile-apis-en).

Controleer voordat je doorgaat de [Aan de slag-handleiding voor profiel-API](../api/getting-started.md) voor verbindingen aan geadviseerde documentatie, een gids aan het lezen van de steekproefAPI vraag die in dit document verschijnt, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

Raadpleeg ook de documentatie bij de volgende service:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Gids Aan de slag met schema-register](../../xdm/api/getting-started.md#know-your-tenant_id): Informatie over uw `{TENANT_ID}`, die in de reacties in deze handleiding wordt weergegeven, wordt weergegeven.

## Een lijst met berekende kenmerken ophalen {#list}

U kunt een lijst van alle gegevens verwerkte attributen voor uw organisatie terugwinnen door een verzoek van de GET aan `/attributes` eindpunt.

**API-indeling**

De `/attributes` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle gegevens verwerkte attributen beschikbaar voor uw organisatie worden teruggewonnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

De volgende queryparameters kunnen worden gebruikt bij het ophalen van een lijst met berekende kenmerken:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `limit` | Een parameter die het maximumaantal punten specificeert die als deel van de reactie worden teruggekeerd. De minimumwaarde van deze parameter is 1 en de maximumwaarde is 40. Als deze parameter niet is opgenomen, worden standaard 20 items geretourneerd. | `limit=20` |
| `offset` | Een parameter die het aantal punten specificeert om over te slaan alvorens de punten terug te keren. | `offset=5` |
| `sortBy` | Een parameter die de orde specificeert waarin de teruggekeerde punten worden gesorteerd. Beschikbare opties zijn `name`, `status`, `updateEpoch`, en `createEpoch`. U kunt ook kiezen of u in oplopende of aflopende volgorde wilt sorteren door geen of door een `-` vóór de sorteeroptie. Standaard worden de items gesorteerd op `updateEpoch` in aflopende volgorde. | `sortBy=name` |
| `status` | Een parameter waarmee u kunt filteren op de status van het berekende kenmerk. Beschikbare opties zijn `draft`, `new`, `processing`, `processed`, `failed`, `disabled`, en `initializing`. Deze optie is niet hoofdlettergevoelig. | `status=draft` |

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

**Antwoord**

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
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
                "meta": " "
            },
            "mergeFunction": {
                "value": "-"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
                "meta": " "
            },
            "mergeFunction": {
                "value": "-"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
                "meta": " "
            },
            "mergeFunction": {
                "value": "-"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
| `computedAttributes` | Een array die de berekende kenmerken bevat op basis van de queryparameters. Meer informatie over de berekende kenmerkenarray vindt u in de [een specifieke berekende kenmerksectie ophalen](#get). |
| `_page` | Een object dat metagegevens bevat over de geretourneerde resultaten. Dit omvat informatie over de huidige verschuiving, het aantal geretourneerde berekende kenmerken, het totale aantal berekende kenmerken en de limiet van geretourneerde berekende kenmerken. |

+++

## Een berekend kenmerk maken {#create}

Om een gegevens verwerkt attribuut tot stand te brengen, begin door een verzoek van de POST aan `/attributes` eindpunt met een verzoeklichaam dat de details van de gegevens verwerkte attributen bevat die u wenst om tot stand te brengen.

**API-indeling**

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
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)"
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
| `name` | De naam van het berekende kenmerkveld, als een tekenreeks. De naam van het berekende kenmerk kan alleen bestaan uit alfanumerieke tekens zonder spaties of onderstrepingstekens. Deze waarde **moet** uniek zijn onder alle berekende kenmerken. Deze naam moet een camelCase-versie van het dialoogvenster `displayName`. |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat dit anderen binnen uw organisatie helpt te bepalen welk kenmerk correct moet worden berekend. |
| `displayName` | De weergavenaam voor het berekende kenmerk. Dit is de naam die wordt weergegeven wanneer u uw berekende kenmerken weergeeft in de gebruikersinterface van Adobe Experience Platform. |
| `expression` | Een object dat de query-expressie vertegenwoordigt van het berekende kenmerk dat u probeert te maken. |
| `expression.type` | Het type van de expressie. Momenteel wordt alleen PQL ondersteund. |
| `expression.format` | De indeling van de expressie. Alleen `pql/text` wordt ondersteund. |
| `expression.value` | De waarde van de expressie. |
| `keepCurrent` | Een Booleaanse waarde die bepaalt of de waarde van het berekende kenmerk up-to-date wordt gehouden. Deze waarde moet momenteel worden ingesteld op `false`. |
| `duration` | Een object dat de terugzoekperiode voor het berekende kenmerk vertegenwoordigt. De terugkijkperiode vertegenwoordigt hoe ver terug kan worden gezocht om de gegevens verwerkte attributen te berekenen. |
| `duration.count` | Een getal dat de duur van de terugzoekperiode vertegenwoordigt. Welke waarden mogelijk zijn, is afhankelijk van de waarde van de `duration.unit` veld. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Een tekenreeks die de tijdseenheid vertegenwoordigt die voor de terugzoekperiode wordt gebruikt. Mogelijke waarden zijn: `HOURS`, `DAYS`, `WEEKS`, en `MONTHS`. |
| `status` | De status van het berekende kenmerk. Mogelijke waarden zijn `DRAFT` en `NEW`. |

+++

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd gegevens verwerkt attribuut terug.

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
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De door het systeem gegenereerde id van het nieuwe berekende kenmerk. |
| `status` | De status van het berekende kenmerk. Dit kan `DRAFT` of `NEW`. |
| `createEpoch` | De tijd waarop het berekende attribuut werd gecreeerd, in seconden. |
| `updateEpoch` | Het tijdstip waarop het berekende kenmerk voor het laatst is bijgewerkt, in seconden. |
| `createdBy` | De id van de gebruiker die het berekende kenmerk heeft gemaakt. |

+++

## Hiermee wordt een specifiek berekend kenmerk opgehaald {#get}

U kunt gedetailleerde informatie over een specifiek gegevens verwerkt attribuut terugwinnen door een verzoek van de GET aan `/attributes` eindpunt en het verstrekken van identiteitskaart van de gegevens verwerkte attributen u wenst om in de verzoekweg terug te winnen.

**API-indeling**

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

**Antwoord**

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
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde id die kan worden gebruikt voor het verwijzen naar het berekende kenmerk tijdens andere API-bewerkingen. |
| `type` | Een tekenreeks die aangeeft dat het geretourneerde object een berekend kenmerk is. |
| `imsOrgId` | De id van de organisatie waartoe het berekende kenmerk behoort. |
| `sandbox` | Het sandboxobject bevat details van de sandbox waarin het berekende kenmerk is geconfigureerd. Deze informatie wordt getekend vanuit de sandboxheader die in de aanvraag wordt verzonden. Zie voor meer informatie de [sandboxen, overzicht](../../sandboxes/home.md). |
| `path` | De `path` naar het berekende kenmerk. |
| `expression` | Een object dat de expressie van het berekende kenmerk bevat. |
| `mergeFunction` | Een object dat de samenvoegfunctie voor het berekende kenmerk bevat. Deze waarde is gebaseerd op de overeenkomstige aggregatieparameter binnen de berekende expressie van het kenmerk. |
| `status` | De status van het berekende kenmerk. Dit kan een van de volgende waarden zijn: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED`, of `DISABLED`. |
| `schema` | Een object dat informatie bevat over het schema waarin de expressie wordt geëvalueerd. Alleen `_xdm.context.profile` wordt ondersteund. |
| `createEpoch` | De tijd waarop het berekende attribuut werd gecreeerd, in seconden. |
| `updateEpoch` | Het tijdstip waarop het berekende kenmerk voor het laatst is bijgewerkt, in seconden. |
| `createdBy` | De id van de gebruiker die het berekende kenmerk heeft gemaakt. |

+++

## Een specifiek berekend kenmerk verwijderen {#delete}

U kunt een specifiek gegevens verwerkt kenmerk verwijderen door een DELETE-aanvraag in te dienen bij de `/attributes` eindpunt en het verstrekken van identiteitskaart van de gegevens verwerkte attributen u wenst om in de verzoekweg te schrappen.

>[!IMPORTANT]
>
>Het verwijderingsverzoek kan alleen worden gebruikt om berekende kenmerken met de status **ontwerp** (`DRAFT`). Dit eindpunt **kan** worden gebruikt om berekende kenmerken in een ander frame te verwijderen.

**API-indeling**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | De `id` waarde van het berekende kenmerk dat u wilt verwijderen. |

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

**Antwoord**

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
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Een specifiek berekend kenmerk bijwerken

U kunt een specifiek berekend kenmerk bijwerken door een PATCH-aanvraag in te dienen bij de `/attributes` eindpunt en het verstrekken van identiteitskaart van de gegevens verwerkte attributen u wenst om in de verzoekweg bij te werken.

>[!IMPORTANT]
>
>Wanneer u een berekend kenmerk bijwerkt, kunnen alleen de volgende velden worden bijgewerkt:
>
>- Als de huidige status `NEW`, kan de status alleen worden gewijzigd in `DISABLED`.
>- Als de huidige status `DRAFT`kunt u de waarden van de volgende velden wijzigen: `name`, `description`, `keepCurrent`, `expression`, en `duration`. U kunt de status ook wijzigen vanuit `DRAFT` tot `NEW`. Wijzigingen in door het systeem gegenereerde velden, zoals `mergeFunction` of `path` retourneert een fout.
>- Als de huidige status `PROCESSING` of `PROCESSED`, kan de status alleen worden gewijzigd in `DISABLED`.

**API-indeling**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | De `id` waarde van het berekende kenmerk dat u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek wordt de status van het berekende kenmerk bijgewerkt vanuit `DRAFT` tot `NEW`.

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

**Antwoord**

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
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Volgende stappen

Nu u de grondbeginselen van berekende attributen hebt geleerd, bent u klaar om te beginnen bepalend hen voor uw organisatie. Lees voor meer informatie over het gebruik van berekende kenmerken in de gebruikersinterface van het Experience Platform de [UI-gids voor berekende kenmerken](./ui.md).
