---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;api gids;vragen;vraag;de dienst van de Vraag;
solution: Experience Platform
title: API-eindpunt voor query's
description: De volgende secties lopen door vraag u het gebruiken van het /query eindpunt in de Dienst API van de Vraag kunt maken.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Zoekopdrachten, eindpunt

## Voorbeeld-API-aanroepen

De volgende secties lopen door vraag u kunt maken gebruikend `/queries` in de [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Een lijst met query&#39;s ophalen

U kunt een lijst van alle vragen voor uw organisatie terugwinnen door een verzoek van de GET tot de `/queries` eindpunt.

**API-indeling**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optioneel*) Parameters die aan het verzoekweg worden toegevoegd die de resultaten vormen die in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven.

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. Bijvoorbeeld: `orderby=created` sorteert de resultaten in oplopende volgorde. Een `-` vóór het maken (`orderby=-created`) sorteert objecten in aflopende volgorde. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. Bijvoorbeeld: `start=2` Hiermee wordt een lijst geretourneerd die begint bij de derde query. (*Standaardwaarde: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **moet** zijn aan HTML ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created`, `updated`, `state`, en `id`. De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan), `>=` (groter dan of gelijk aan), `<=` (kleiner dan of gelijk aan), `==` (gelijk aan), `!=` (niet gelijk aan), en `~` (bevat). Bijvoorbeeld: `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert alle query&#39;s met de opgegeven id. |
| `excludeSoftDeleted` | Geeft aan of een query die is verwijderd, moet worden opgenomen. Bijvoorbeeld: `excludeSoftDeleted=false` zal **include** verwijderde softquery&#39;s. (*Boolean, standaardwaarde: true*) |
| `excludeHidden` | Geeft aan of niet-door de gebruiker gestuurde query&#39;s moeten worden weergegeven. Als deze waarde is ingesteld op false, wordt **include** query&#39;s die niet door gebruikers worden gestuurd, zoals CURSOR-definities, FETCH of metagegevensquery&#39;s. (*Boolean, standaardwaarde: true*) |
| `isPrevLink` | De `isPrevLink` queryparameter wordt gebruikt voor paginering. Resultaten van de API-aanroep worden gesorteerd op basis van hun `created` tijdstempel en de `orderby` eigenschap. Tijdens het navigeren door de resultatenpagina&#39;s `isPrevLink` wordt ingesteld op true wanneer achterwaarts wordt gepagineerd. Het keert de orde van de vraag om. Zie &quot;volgende&quot; en &quot;vorige&quot; koppelingen als voorbeelden. |

**Verzoek**

Het volgende verzoek wint de recentste vraag terug die voor uw organisatie wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert HTTP status 200 met een lijst van vragen voor de gespecificeerde organisatie als JSON terug. De volgende reactie keert de recentste vraag terug die voor uw organisatie wordt gecreeerd.

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

U kunt een nieuwe vraag tot stand brengen door een verzoek van de POST aan `/queries` eindpunt.

**API-indeling**

```http
POST /queries
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe vraag, met een SQL verklaring die in de nuttige lading wordt verstrekt:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

In het onderstaande aanvraagvoorbeeld wordt een nieuwe query gemaakt met een bestaande querysjabloon-id.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `dbName` | De naam van de database waarvoor u een SQL-query maakt. |
| `sql` | De SQL-query die u wilt maken. |
| `name` | De naam van uw SQL-query. |
| `description` | De beschrijving van uw SQL-query. |
| `queryParameters` | Een sleutelwaarde die wordt geparseerd om het even welke parameters bepaalde waarden in de SQL verklaring te vervangen. Alleen vereist **indien** u gebruikt parametervervangingen binnen SQL u verstrekt. Op deze sleutelwaardeparen wordt het waardetype niet gecontroleerd. |
| `templateId` | De unieke id voor een bestaande query. U kunt dit opgeven in plaats van een SQL-instructie. |
| `insertIntoParameters` | (Optioneel) Als deze eigenschap is gedefinieerd, wordt deze query omgezet in een INSERT INTO-query. |
| `ctasParameters` | (Optioneel) Als deze eigenschap is gedefinieerd, wordt deze query omgezet in een CTAS-query. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met details van de nieuwe query. Nadat de query is geactiveerd en correct is uitgevoerd, wordt de opdracht `state` verandert van `SUBMITTED` tot `SUCCESS`.

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
>U kunt de waarde van `_links.cancel` tot [uw gemaakte query annuleren](#cancel-a-query).

### Een query ophalen op ID

U kunt gedetailleerde informatie over een specifieke vraag terugwinnen door een verzoek van de GET aan `/queries` eindpunt en het verstrekken van de vraag `id` waarde in het aanvraagpad.

**API-indeling**

```http
GET /queries/{QUERY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` De waarde van de query die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>U kunt de waarde van `_links.cancel` tot [uw gemaakte query annuleren](#cancel-a-query).

### Een query annuleren of verwijderen op een andere manier

U kunt verzoeken om een opgegeven query te annuleren of te verwijderen door een PATCH-aanvraag in te dienen bij de `/queries` eindpunt en het verstrekken van de vraag `id` waarde in het aanvraagpad.

**API-indeling**

```http
PATCH /queries/{QUERY_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` waarde van de vraag u de verrichting wilt uitvoeren op. |


**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | Het type bewerking dat op de bron moet worden uitgevoerd. Accepteerde waarden zijn `cancel` en `soft_delete`. Als u de query wilt annuleren, moet u de parameter op met de waarde instellen `cancel `. Merk op dat de zachte schrappingsverrichting de vraag tegenhoudt van zijn teruggekeerd op verzoeken van de GET maar schrapt het niet van het systeem. |

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
