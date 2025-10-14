---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;api gids;vragen;vraag;de dienst van de Vraag;
solution: Experience Platform
title: API-eindpunt voor query's
description: De volgende secties lopen door vraag u het gebruiken van het /query eindpunt in de Dienst API van de Vraag kunt maken.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Zoekopdrachten, eindpunt

## Voorbeeld-API-aanroepen

In de volgende secties worden aanroepen doorlopen die u kunt maken met het eindpunt `/queries` in de [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Een lijst met query&#39;s ophalen

U kunt een lijst van alle vragen voor uw organisatie terugwinnen door een verzoek van de GET tot het `/queries` eindpunt te richten.

**API formaat**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatieve*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden. De beschikbare parameters worden hieronder weergegeven.

**de parameters van de Vraag**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated` . `orderby=created` sorteert de resultaten bijvoorbeeld in oplopende volgorde. Wanneer u een `-` vóór het maken (`orderby=-created` ) toevoegt, worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Geef een tijdstempel voor de ISO-indeling op om de resultaten te bestellen. Als geen begindatum wordt gespecificeerd, zal de API vraag eerst de oudste gecreeerde vraag terugkeren, dan zal blijven van recentere resultaten een lijst maken.<br> Met ISO-tijdstempels kunt u verschillende niveaus van granulariteit opgeven in de datum en tijd. De basis-ISO-tijdstempels hebben de notatie: `2020-09-07` voor het uitdrukken van de datum 7 september 2020. Een complexer voorbeeld zou als `2022-11-05T08:15:30-05:00` worden geschreven en beantwoordt aan 5 November, 2022, 8 :15: 30 am, de Tijd van de Norm van de V.S. Een timezone kan met een UTC compensatie worden voorzien en door het achtervoegsel &quot;Z&quot; (`2020-01-01T01:01:01Z`) wordt aangeduid. Als er geen tijdzone is opgegeven, wordt de standaardwaarde nul gebruikt. |
| `property` | Filterresultaten op basis van velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created` , `updated` , `state` en `id` . De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan), `>=` (groter dan of gelijk aan), `<=` (kleiner dan of gelijk aan), `==` (gelijk aan), `!=` (niet gelijk aan) en `~` (bevat). `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert bijvoorbeeld alle query&#39;s met de opgegeven id. |
| `excludeSoftDeleted` | Geeft aan of een query die is verwijderd, moet worden opgenomen. Bijvoorbeeld, `excludeSoftDeleted=false` zal **&#x200B;**&#x200B;zachte geschrapte vragen omvatten. (*Van Boole, standaardwaarde: waar*) |
| `excludeHidden` | Geeft aan of niet-door de gebruiker gestuurde query&#39;s moeten worden weergegeven. Het hebben van deze waarde die aan vals wordt geplaatst zal **&#x200B;**&#x200B;niet-gebruiker gedreven vragen, zoals CURSOR definities, FETCH, of meta-gegevensvragen omvatten. (*Van Boole, standaardwaarde: waar*) |
| `isPrevLink` | De query-parameter `isPrevLink` wordt gebruikt voor paginering. De resultaten van de API-aanroep worden gesorteerd op basis van hun `created` timestamp en de `orderby` -eigenschap. Wanneer u door de resultatenpagina&#39;s navigeert, wordt `isPrevLink` ingesteld op true wanneer achterwaarts wordt gepagineerd. Het keert de orde van de vraag om. Zie &quot;volgende&quot; en &quot;vorige&quot; koppelingen als voorbeelden. |

**Verzoek**

Het volgende verzoek wint de recentste vraag terug die voor uw organisatie wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

U kunt een nieuwe vraag tot stand brengen door een verzoek van de POST aan het `/queries` eindpunt te doen.

**API formaat**

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
| `queryParameters` | Een sleutelwaarde die wordt geparseerd om het even welke parameters bepaalde waarden in de SQL verklaring te vervangen. Het wordt slechts vereist **als** u parametervervangingen binnen SQL gebruikt u verstrekt. Op deze sleutelwaardeparen wordt het waardetype niet gecontroleerd. |
| `templateId` | De unieke id voor een bestaande query. U kunt dit opgeven in plaats van een SQL-instructie. |
| `insertIntoParameters` | (Optioneel) Als deze eigenschap is gedefinieerd, wordt deze query omgezet in een INSERT INTO-query. |
| `ctasParameters` | (Optioneel) Als deze eigenschap is gedefinieerd, wordt deze query omgezet in een CTAS-query. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) met details van de nieuwe query. Nadat de query is geactiveerd en correct is uitgevoerd, verandert de `state` van `SUBMITTED` in `SUCCESS` .

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
>U kunt de waarde van `_links.cancel` gebruiken om [&#x200B; uw gecreeerde vraag &#x200B;](#cancel-a-query) te annuleren.

### Een query ophalen op ID

U kunt gedetailleerde informatie over een specifieke vraag terugwinnen door een verzoek van de GET tot het `/queries` eindpunt te richten en de waarde van de vraag `id` in de verzoekweg te verstrekken.

**API formaat**

```http
GET /queries/{QUERY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` -waarde van de query die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
>U kunt de waarde van `_links.cancel` gebruiken om [&#x200B; uw gecreeerde vraag &#x200B;](#cancel-a-query) te annuleren.

### Een query annuleren of verwijderen op een andere manier

U kunt verzoeken om een opgegeven query te annuleren of te verwijderen door een PATCH-aanvraag in te dienen bij het `/queries` -eindpunt en de waarde `id` van de query op te geven in het aanvraagpad.

**API formaat**

```http
PATCH /queries/{QUERY_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De `id` -waarde van de query waarop u de bewerking wilt uitvoeren. |


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
| `op` | Het type bewerking dat op de bron moet worden uitgevoerd. Accepteerde waarden zijn `cancel` en `soft_delete` . Als u de query wilt annuleren, moet u de parameter op met de waarde `cancel ` instellen. Merk op dat de zachte schrappingsverrichting de vraag tegenhoudt van zijn teruggekeerd op verzoeken van de GET maar schrapt het niet van het systeem. |

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
