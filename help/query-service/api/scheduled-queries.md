---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;geplande vragen;geplande vraag;
solution: Experience Platform
title: Het geplande Eindpunt van Vragen API
topic-legacy: scheduled queries
description: De volgende secties lopen door de diverse API vraag u voor geplande vragen met de Dienst API van de Vraag kunt maken.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 34a3b71ace2f9ece02e4368b6bd7eab716330ee1
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 0%

---

# Gepland vragen eindpunt

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten vraag aan [!DNL Query Service] API. De volgende secties lopen door de diverse API vraag u kan maken gebruikend [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Hiermee wordt een lijst met geplande query&#39;s opgehaald

U kunt een lijst van alle geplande vragen voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan het `/schedules` eindpunt te doen.

**API-indeling**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatieve*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven. |

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van geplande query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle geplande vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. `orderby=created` sorteert de resultaten bijvoorbeeld in oplopende volgorde. Als u een `-` toevoegt voordat u een item (`orderby=-created`) hebt gemaakt, worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. `start=2` retourneert bijvoorbeeld een lijst die begint bij de derde query. (*Standaardwaarde: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **must** moeten uit HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created`, `templateId` en `userId`. De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan) en `==` (gelijk aan). `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert bijvoorbeeld alle geplande query&#39;s waarbij de gebruiker-id overeenkomt met de opgegeven waarde. |

**Verzoek**

Het volgende verzoek wint de recentste geplande vraag terug die voor uw organisatie IMS wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met een lijst van geplande vragen voor de gespecificeerde IMS Organisatie terug. De volgende reactie keert de recentste geplande vraag terug die voor uw organisatie IMS wordt gecreeerd.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Nieuwe geplande query maken

U kunt een nieuwe geplande vraag tot stand brengen door een verzoek van de POST aan het `/schedules` eindpunt te doen. Wanneer u een geplande query maakt in de API, kunt u deze ook zien in de Query-editor. Voor meer informatie over geplande vragen in UI, te lezen gelieve [de documentatie van de Redacteur van de Vraag](../ui/user-guide.md#scheduled-queries).

**API-indeling**

```http
POST /schedules
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `query.dbName` | De naam van de database waarvoor u een geplande query maakt. |
| `query.sql` | De SQL-query die u wilt maken. |
| `query.name` | De naam van de geplande query. |
| `schedule.schedule` | Het uitsnijdschema voor de query. Lees de [indeling van de expressie voor uitsnijden](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentatie voor meer informatie over uitsnijdschema&#39;s. In dit voorbeeld betekent &quot;30 * * *&quot;dat de vraag elk uur bij het minteken van 30 minuten zal lopen.<br><br>U kunt ook de volgende steno-expressies gebruiken:<ul><li>`@once`: De query wordt maar één keer uitgevoerd.</li><li>`@hourly`: De vraag loopt elk uur aan het begin van het uur. Dit is gelijk aan de expressie voor uitsnijden `0 * * * *`.</li><li>`@daily`: De query wordt eenmaal per dag om middernacht uitgevoerd. Dit is gelijk aan de expressie voor uitsnijden `0 0 * * *`.</li><li>`@weekly`: De query wordt één keer per week uitgevoerd, op zondag, om middernacht. Dit is gelijk aan de expressie voor uitsnijden `0 0 * * 0`.</li><li>`@monthly`: De query wordt één keer per maand uitgevoerd, op de eerste dag van de maand, om middernacht. Dit is gelijk aan de expressie voor uitsnijden `0 0 1 * *`.</li><li>`@yearly`: De query wordt één keer per jaar uitgevoerd, op 1 januari, om middernacht. Dit is gelijk aan de expressie voor uitsnijden `1 0 0 1 1 *`. |
| `schedule.startDate` | De begindatum voor uw geplande query, geschreven als een UTC-tijdstempel. |

**Antwoord**

Een succesvolle reactie keert status 202 (Toegelaten) van HTTP met details van uw onlangs gecreeerde geplande vraag terug. Wanneer de geplande query is geactiveerd, verandert `state` van `REGISTERING` in `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` aan [schrappen uw gecreeerde geplande vraag](#delete-a-specified-scheduled-query) gebruiken.

### Gegevens van een opgegeven geplande query aanvragen

U kunt informatie voor een specifieke geplande vraag terugwinnen door een verzoek van de GET aan het `/schedules` eindpunt te doen en zijn identiteitskaart in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van de gespecificeerde geplande vraag terug.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>U kunt de waarde van `_links.delete` aan [schrappen uw gecreeerde geplande vraag](#delete-a-specified-scheduled-query) gebruiken.

### Details van een opgegeven geplande query bijwerken

U kunt de details voor een gespecificeerde geplande vraag bijwerken door een verzoek van PATCH aan het `/schedules` eindpunt en door zijn identiteitskaart in de verzoekweg te verstrekken.

De PATCH-aanvraag ondersteunt twee verschillende paden: `/state` en `/schedule/schedule`.

### Geplande querystatus bijwerken

U kunt `/state` gebruiken om de staat van de geselecteerde geplande vraag bij te werken - INGESCHAKELD of UITGESCHAKELD. Als u de status wilt bijwerken, moet u de waarde instellen als `enable` of `disable`.

**API-indeling**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag u wilt terugwinnen. |


**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u de geplande staat van de vraag bijwerkt, moet u de waarde van `path` aan `/state` plaatsen. |
| `value` | De bijgewerkte waarde van `/state`. Deze waarde kan als `enable` of `disable` worden geplaatst om de geplande vraag toe te laten of onbruikbaar te maken. |

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Geplande queryplanning bijwerken

U kunt `/schedule/schedule` gebruiken om het cron programma van de geplande vraag bij te werken. Lees de [indeling van de expressie voor uitsnijden](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentatie voor meer informatie over uitsnijdschema&#39;s.

**API-indeling**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag u wilt terugwinnen. |

**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u het geplande programma van de vraag bijwerkt, moet u de waarde van `path` aan `/schedule/schedule` plaatsen. |
| `value` | De bijgewerkte waarde van `/schedule`. Deze waarde moet de vorm hebben van een uitsnijdschema. Dus, in dit voorbeeld, zal de geplande vraag elk uur bij het 45 minieme teken in werking stellen. |

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Opgegeven geplande query verwijderen

U kunt een gespecificeerde geplande vraag schrappen door een verzoek van DELETE aan het `/schedules` eindpunt te doen en identiteitskaart van de geplande vraag te verstrekken u in de verzoekweg wilt schrappen.

>[!NOTE]
>
>Het schema **must** moet worden onbruikbaar gemaakt alvorens wordt geschrapt.

**API-indeling**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag u wilt terugwinnen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
