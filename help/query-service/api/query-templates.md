---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Zoeksjablonen

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten vraag aan de Dienst API van de Vraag. De volgende secties lopen door diverse API vraag u het gebruiken van de Dienst API van de Vraag kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Een lijst met querysjablonen ophalen

U kunt een lijst van alle vraagmalplaatjes voor uw IMS Organisatie terugwinnen door een GET verzoek aan het `/query-templates` eindpunt te doen.

**API-indeling**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatief*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven. |

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van querysjablonen. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vraagmalplaatjes beschikbaar voor uw organisatie terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. De resultaten worden bijvoorbeeld in oplopende volgorde `orderby=created` gesorteerd. Als u een `-` voorinstelling toevoegt (`orderby=-created`), worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Default value: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. Bijvoorbeeld, `start=2` zal een lijst terugkeren die van de derde vermelde vraag begint. (*Default value: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **moeten** zijn beschermd tegen HTML. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `name` en `userId`. De enige ondersteunde operator is `==` (gelijk aan). Retourneert bijvoorbeeld `name==my_template` alle querysjablonen met de naam `my_template`. |

**Verzoek**

Het volgende verzoek wint het recentste vraagmalplaatje terug dat voor uw organisatie IMS wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
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

>[!NOTE] U kunt de waarde van gebruiken `_links.delete` om uw vraagmalplaatje [te](#delete-a-specified-query-template)schrappen.

### Een querysjabloon maken

U kunt een vraagmalplaatje tot stand brengen door een POST- verzoek aan het `/query-templates` eindpunt te doen.

**API-indeling**

```http
POST /query-templates
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] U kunt de waarde van gebruiken `_links.delete` om uw vraagmalplaatje [te](#delete-a-specified-query-template)schrappen.

### Een opgegeven querysjabloon ophalen

U kunt een specifiek vraagmalplaatje terugwinnen door een GET verzoek aan het `/query-templates/{TEMPLATE_ID}` eindpunt te doen en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] U kunt de waarde van gebruiken `_links.delete` om uw vraagmalplaatje [te](#delete-a-specified-query-template)schrappen.

### Een opgegeven querysjabloon bijwerken

U kunt een specifiek vraagmalplaatje bijwerken door een PPUT- verzoek aan het `/query-templates/{TEMPLATE_ID}` eindpunt te doen en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

**API-indeling**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TEMPLATE_ID}` | De `id` waarde van het vraagmalplaatje u wilt terugwinnen. |

**Verzoek**

>[!NOTE] Voor de PUT-aanvraag moeten zowel het veld sql als de naam worden ingevuld en de huidige inhoud van de querysjabloon wordt **overschreven** .

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] U kunt de waarde van gebruiken `_links.delete` om uw vraagmalplaatje [te](#delete-a-specified-query-template)schrappen.

### Een opgegeven querysjabloon verwijderen

U kunt een specifiek vraagmalplaatje schrappen door een verzoek van de VERWIJDERING aan te brengen `/query-templates/{TEMPLATE_ID}` en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
