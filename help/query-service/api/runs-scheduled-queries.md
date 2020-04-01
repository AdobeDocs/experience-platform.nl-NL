---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Runs voor geplande vragen

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten vraag aan de Dienst API van de Vraag. De volgende secties lopen door diverse API vraag u het gebruiken van de Dienst API van de Vraag kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Hiermee wordt een lijst met alle uitvoeringen voor een opgegeven geplande query opgehaald

U kunt een lijst van alle looppas voor een specifieke geplande vraag terugwinnen, ongeacht of zij momenteel lopen of reeds voltooid zijn. Dit wordt gedaan door een GET verzoek aan het `/schedules/{SCHEDULE_ID}/runs` eindpunt te doen, waar `{SCHEDULE_ID}` is de `id` waarde van de geplande vraag de waarvan looppas u wenst terug te winnen.

**API-indeling**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande query die u wilt ophalen. |
| `{QUERY_PARAMETERS}` | (*Facultatief*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven. |

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van uitvoeringen voor een opgegeven geplande query. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle looppas beschikbaar voor de gespecificeerde geplande vraag terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. De resultaten worden bijvoorbeeld in oplopende volgorde `orderby=created` gesorteerd. Als u een `-` voorinstelling toevoegt (`orderby=-created`), worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Default value: 20*) |
| `start` | Hiermee verschuift u de lijst met reacties met op nul gebaseerde nummering. Bijvoorbeeld, `start=2` zal een lijst terugkeren die van de derde vermelde vraag begint. (*Default value: 0*) |
| `property` | Filterresultaten op basis van velden. De filters **moeten** zijn beschermd tegen HTML. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created`, `state`en `externalTrigger`. De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan) en `==` (gelijk aan) en `!=` (niet gelijk aan). Bijvoorbeeld, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` zal alle looppas terugkeren die manueel creeerde, opvolgde, en creeerde na 20 april, 2019. |

**Verzoek**

Het volgende verzoek wint de laatste vier looppas voor de gespecificeerde geplande vraag terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met een lijst van looppas voor de gespecificeerde geplande vraag als JSON terug. De volgende reactie keert de laatste vier looppas voor de gespecificeerde geplande vraag terug.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE] U kunt de waarde van gebruiken `_links.cancel` om een looppas voor een gespecificeerde geplande vraag [tegen te](#immediately-stop-a-run-for-a-specific-scheduled-query)houden.

### Breng onmiddellijk een looppas voor een specifieke geplande vraag teweeg

U kunt een looppas voor een gespecificeerde geplande vraag onmiddellijk teweegbrengen door een POST- verzoek aan het `/schedules/{SCHEDULE_ID}/runs` eindpunt te doen, waar `{SCHEDULE_ID}` de `id` waarde van de geplande vraag is de waarvan looppas u wenst om te teweegbrengen.

**API-indeling**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Haal details van een looppas voor een specifieke geplande vraag terug

U kunt details over een looppas voor een specifieke geplande vraag terugwinnen door een GET verzoek aan het `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt te doen en zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag waarvan looppas u wenst om details van terug te winnen. |
| `{RUN_ID}` | De `id` waarde van de run die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van de gespecificeerde looppas terug.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Stop onmiddellijk een looppas voor een specifieke geplande vraag

U kunt onmiddellijk een looppas voor een specifieke geplande vraag tegenhouden door een verzoek van de PATCH aan het `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt te doen en zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg te verstrekken.

**API-indeling**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande vraag waarvan looppas u wenst om details van terug te winnen. |
| `{RUN_ID}` | De `id` waarde van de run die u wilt ophalen. |

**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
