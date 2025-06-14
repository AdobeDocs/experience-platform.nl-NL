---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;vraagmalplaatjes;api gids;malplaatjes;de dienst van de Vraag;
solution: Experience Platform
title: API-eindpunt voor querysjablonen
description: Deze gids specificeert de diverse vraag API van het vraagmalplaatje u het gebruiken van de Dienst API van de Vraag kunt maken.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# Zoeksjablonen, eindpunt

## Voorbeeld-API-aanroepen

In de volgende secties worden de verschillende API-aanroepen beschreven die u met de API [!DNL Query Service] kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

Zie de [ documentatie van de vraagmalplaatjes UI ](../ui/query-templates.md) voor informatie bij het creëren van malplaatjes door Experience Platform UI.

### Een lijst met querysjablonen ophalen

U kunt een lijst van alle vraagmalplaatjes voor uw organisatie terugwinnen door een verzoek van de GET tot het `/query-templates` eindpunt te richten.

**API formaat**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatieve*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden. De beschikbare parameters worden hieronder weergegeven. |

**de parameters van de Vraag**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van querysjablonen. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vraagmalplaatjes beschikbaar voor uw organisatie terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated` . `orderby=created` sorteert de resultaten bijvoorbeeld in oplopende volgorde. Wanneer u een `-` vóór het maken (`orderby=-created` ) toevoegt, worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Geef een tijdstempel voor de ISO-indeling op om de resultaten te bestellen. Als er geen begindatum is opgegeven, retourneert de API-aanroep eerst de oudste gemaakte sjablonen en worden de meest recente resultaten weergegeven.<br> Met ISO-tijdstempels kunt u verschillende niveaus van granulariteit opgeven in de datum en tijd. De basis-ISO-tijdstempels hebben de notatie: `2020-09-07` voor het uitdrukken van de datum 7 september 2020. Een complexer voorbeeld zou als `2022-11-05T08:15:30-05:00` worden geschreven en beantwoordt aan 5 November, 2022, 8 :15: 30 am, de Tijd van de Norm van de V.S. Een timezone kan met een UTC compensatie worden voorzien en door het achtervoegsel &quot;Z&quot; (`2020-01-01T01:01:01Z`) wordt aangeduid. Als er geen tijdzone is opgegeven, wordt de standaardwaarde nul gebruikt. |
| `property` | Filterresultaten op basis van velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `name` en `userId` . De enige ondersteunde operator is `==` (gelijk aan). `name==my_template` retourneert bijvoorbeeld alle querysjablonen met de naam `my_template` . |

**Verzoek**

Het volgende verzoek wint het recentste vraagmalplaatje terug dat voor uw organisatie wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van vraagmalplaatjes voor de gespecificeerde organisatie terug. De volgende reactie keert het recentste vraagmalplaatje terug dat voor uw organisatie wordt gecreeerd.

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
>U kunt de waarde van `_links.delete` gebruiken om [ uw vraagmalplaatje ](#delete-a-specified-query-template) te schrappen.

### Een querysjabloon maken

U kunt een vraagmalplaatje tot stand brengen door een verzoek van de POST aan het `/query-templates` eindpunt te doen.

**API formaat**

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
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sql` | De SQL-query die u wilt maken. U kunt standaard-SQL of parametervervanging gebruiken. Als u een parametervervanging in SQL wilt gebruiken, moet u de parametersleutel met een `$` voorafgaan. Bijvoorbeeld `$key` en geef de parameters die in de SQL als JSON-sleutelwaardeparen worden gebruikt, op in het `queryParameters` -veld. De waarden die hier worden doorgegeven, zijn de standaardparameters die in de sjabloon worden gebruikt. Als u deze parameters wilt met voeten treden, moet u hen in het verzoek van de POST met voeten treden. |
| `name` | De naam van de querysjabloon. |
| `queryParameters` | Een sleutelwaarde die wordt geparseerd om het even welke parameters bepaalde waarden in de SQL verklaring te vervangen. Het wordt slechts vereist **als** u parametervervangingen binnen SQL gebruikt u verstrekt. Op deze sleutelwaardeparen wordt het waardetype niet gecontroleerd. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met details van de nieuw gemaakte querysjabloon.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
>U kunt de waarde van `_links.delete` gebruiken om [ uw vraagmalplaatje ](#delete-a-specified-query-template) te schrappen.

### Een opgegeven querysjabloon ophalen

U kunt een specifiek vraagmalplaatje terugwinnen door een verzoek van de GET aan het `/query-templates/{TEMPLATE_ID}` eindpunt te doen en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

**API formaat**

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

**Reactie**

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
>U kunt de waarde van `_links.delete` gebruiken om [ uw vraagmalplaatje ](#delete-a-specified-query-template) te schrappen.

### Een opgegeven querysjabloon bijwerken

U kunt een specifieke vraagmalplaatje bijwerken door een verzoek van de PUT aan het `/query-templates/{TEMPLATE_ID}` eindpunt te doen en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

**API formaat**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TEMPLATE_ID}` | De `id` waarde van het vraagmalplaatje u wilt terugwinnen. |

**Verzoek**

>[!NOTE]
>
>Het verzoek van de PUT vereist zowel sql als naamgebied om worden gevuld, en zal **&#x200B;**&#x200B;de huidige inhoud van dat vraagmalplaatje beschrijven.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sql` | De SQL-query die u wilt maken. U kunt standaard-SQL of parametervervanging gebruiken. Als u een parametervervanging in SQL wilt gebruiken, moet u de parametersleutel met een `$` voorafgaan. Bijvoorbeeld `$key` en geef de parameters die in de SQL als JSON-sleutelwaardeparen worden gebruikt, op in het `queryParameters` -veld. De waarden die hier worden doorgegeven, zijn de standaardparameters die in de sjabloon worden gebruikt. Als u deze parameters wilt met voeten treden, moet u hen in het verzoek van de POST met voeten treden. |
| `name` | De naam van de querysjabloon. |
| `queryParameters` | Een sleutelwaarde die wordt geparseerd om het even welke parameters bepaalde waarden in de SQL verklaring te vervangen. Het wordt slechts vereist **als** u parametervervangingen binnen SQL gebruikt u verstrekt. Op deze sleutelwaardeparen wordt het waardetype niet gecontroleerd. |

**Reactie**

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
>U kunt de waarde van `_links.delete` gebruiken om [ uw vraagmalplaatje ](#delete-a-specified-query-template) te schrappen.

### Een opgegeven querysjabloon verwijderen

U kunt een specifieke vraagmalplaatje schrappen door een DELETE verzoek aan `/query-templates/{TEMPLATE_ID}` te doen en identiteitskaart van het vraagmalplaatje in de verzoekweg te verstrekken.

**API formaat**

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

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
