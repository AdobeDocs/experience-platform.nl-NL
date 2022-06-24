---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;vraagmalplaatjes;api gids;malplaatjes;de dienst van de Vraag;
solution: Experience Platform
title: API-eindpunt voor querysjablonen
topic-legacy: query templates
description: Deze gids specificeert de diverse vraag API van het vraagmalplaatje u kunt maken gebruikend de Dienst API van de Vraag.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c8b3b22b678622c31462ba0baa2f50fbe89b00d5
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Zoeksjablonen, eindpunt

## Voorbeeld-API-aanroepen

In de volgende secties worden de verschillende API-aanroepen beschreven die u kunt maken met de [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

Zie de [UI-query sjabloondocumentatie](../ui/query-templates.md) voor informatie over het creëren van malplaatjes door de UI van het Experience Platform.

### Een lijst met querysjablonen ophalen

U kunt een lijst van alle vraagmalplaatjes voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan `/query-templates` eindpunt.

**API-indeling**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optioneel*) Parameters die aan het verzoekweg worden toegevoegd die de resultaten vormen die in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven. |

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van querysjablonen. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vraagmalplaatjes beschikbaar voor uw organisatie terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. Bijvoorbeeld: `orderby=created` sorteert de resultaten in oplopende volgorde. Een `-` vóór het maken (`orderby=-created`) sorteert objecten in aflopende volgorde. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. Bijvoorbeeld: `start=2` Hiermee wordt een lijst geretourneerd die begint bij de derde query. (*Standaardwaarde: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **moet** zijn aan HTML ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `name` en `userId`. De enige ondersteunde operator is `==` (gelijk aan). Bijvoorbeeld: `name==my_template` retourneert alle querysjablonen met de naam `my_template`. |

**Verzoek**

Het volgende verzoek wint het recentste vraagmalplaatje terug dat voor uw organisatie IMS wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert HTTP status 200 met een lijst van vraagmalplaatjes voor de gespecificeerde IMS Organisatie terug. De volgende reactie keert het recentste vraagmalplaatje terug dat voor uw organisatie IMS wordt gecreeerd.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` tot [verwijder uw querysjabloon](#delete-a-specified-query-template).

### Een querysjabloon maken

U kunt een vraagmalplaatje tot stand brengen door een verzoek van de POST aan `/query-templates` eindpunt.

**API-indeling**

```http
POST /query-templates
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sql` | De SQL-query die u wilt maken. |
| `name` | De naam van de querysjabloon. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met details van de nieuw gemaakte querysjabloon.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` tot [verwijder uw querysjabloon](#delete-a-specified-query-template).

### Een opgegeven querysjabloon ophalen

U kunt een specifieke vraagmalplaatje terugwinnen door een verzoek van de GET aan `/query-templates/{TEMPLATE_ID}` eindpunt en het verstrekken van identiteitskaart van het vraagmalplaatje in de verzoekweg.

**API-indeling**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | De `id` waarde van het vraagmalplaatje u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw gespecificeerd vraagmalplaatje terug.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` tot [verwijder uw querysjabloon](#delete-a-specified-query-template).

### Een opgegeven querysjabloon bijwerken

U kunt een specifieke vraagmalplaatje bijwerken door een verzoek van de PUT aan `/query-templates/{TEMPLATE_ID}` eindpunt en het verstrekken van identiteitskaart van het vraagmalplaatje in de verzoekweg.

**API-indeling**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TEMPLATE_ID}` | De `id` waarde van het vraagmalplaatje u wilt terugwinnen. |

**Verzoek**

>[!NOTE]
>
>Voor de aanvraag van de PUT moeten zowel het veld sql als de naam worden ingevuld en **overschrijven** de huidige inhoud van die vraagmalplaatje.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sql` | De SQL-query die u wilt bijwerken. |
| `name` | De naam van de geplande query. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met de bijgewerkte informatie voor de opgegeven querysjabloon.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` tot [verwijder uw querysjabloon](#delete-a-specified-query-template).

### Een opgegeven querysjabloon verwijderen

U kunt een specifieke vraagmalplaatje schrappen door een verzoek van de DELETE aan te richten `/query-templates/{TEMPLATE_ID}` en het verstrekken van identiteitskaart van het vraagmalplaatje in de verzoekweg.

**API-indeling**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TEMPLATE_ID}` | De `id` waarde van het vraagmalplaatje u wilt terugwinnen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
