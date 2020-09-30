---
keywords: Experience Platform;home;popular topics;query service;api guide;queries;query;Query service;
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: queries
description: De volgende secties lopen door vraag u het gebruiken van het /query eindpunt in de Dienst API van de Vraag kunt maken.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Zoekopdrachten

## Voorbeeld-API-aanroepen

De volgende secties lopen door vraag u het gebruiken van het `/queries` eindpunt in [!DNL Query Service] API kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Een lijst met query&#39;s ophalen

U kunt een lijst van alle vragen voor uw IMS Organisatie terugwinnen door een verzoek van de GET tot het `/queries` eindpunt te richten.

**API-indeling**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatief*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven.

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. De resultaten worden bijvoorbeeld in oplopende volgorde `orderby=created` gesorteerd. Als u een `-` voorinstelling toevoegt (`orderby=-created`), worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Default value: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. Bijvoorbeeld, `start=2` zal een lijst terugkeren die van de derde vermelde vraag begint. (*Default value: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **moeten** zijn beschermd tegen HTML. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created`, `updated`, `state`en `id`. De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan), `>=` (groter dan of gelijk aan), `<=` (kleiner dan of gelijk aan), `==` (gelijk aan), `!=` (niet gelijk aan) en `~` (bevat). Retourneert bijvoorbeeld `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` alle query&#39;s met de opgegeven id. |
| `excludeSoftDeleted` | Geeft aan of een query die is verwijderd, moet worden opgenomen. Bijvoorbeeld, zal `excludeSoftDeleted=false` zachte geschrapte vragen **omvatten** . (*Boolean, standaardwaarde: true*) |
| `excludeHidden` | Geeft aan of niet-door de gebruiker gestuurde query&#39;s moeten worden weergegeven. Als deze waarde is ingesteld op false, **worden query&#39;s die niet door de gebruiker worden gestart, zoals CURSOR-definities, FETCH of metagegevensquery&#39;s, opgenomen** . (*Boolean, standaardwaarde: true*) |

**Verzoek**

Met het volgende verzoek wordt de laatste query opgehaald die voor uw IMS-organisatie is gemaakt.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst met query&#39;s voor de opgegeven IMS-organisatie als JSON. De volgende reactie keert de recentste vraag terug die voor uw organisatie IMS wordt gecreeerd.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Een query maken

U kunt een nieuwe vraag tot stand brengen door een verzoek van de POST aan het `/queries` eindpunt te doen.

**API-indeling**

```http
POST /queries
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe vraag, die door de waarden wordt gevormd die in de lading worden verstrekt:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `dbName` | De naam van de database waarvoor u een SQL-query maakt. |
| `sql` | De SQL-query die u wilt maken. |
| `name` | De naam van uw SQL-query. |
| `description` | De beschrijving van uw SQL-query. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met details van de nieuwe query. Nadat de query is geactiveerd en correct is uitgevoerd, verandert de query van `state` naar `SUBMITTED` `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van gebruiken `_links.cancel` om uw gemaakte query [te](#cancel-a-query)annuleren.

### Een query ophalen op ID

U kunt gedetailleerde informatie over een specifieke vraag terugwinnen door een verzoek van de GET tot het `/queries` eindpunt te richten en de `id` waarde van de vraag in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /queries/{QUERY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` waarde van de vraag u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde vraag terug.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van gebruiken `_links.cancel` om uw gemaakte query [te](#cancel-a-query)annuleren.

### Een query annuleren

U kunt verzoeken om een gespecificeerde vraag te schrappen door een verzoek van PATCH aan het `/queries` eindpunt te doen en de `id` waarde van de vraag in de verzoekweg te verstrekken.

**API-indeling**

```http
PATCH /queries/{QUERY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` waarde van de query die u wilt annuleren. |


**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | Als u de query wilt annuleren, moet u de parameter op met de waarde instellen `cancel `. |

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
