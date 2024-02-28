---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;stel geplande vragen in werking;stel geplande vraag;de dienst van de vraag;geplande vragen;geplande vraag;
solution: Experience Platform
title: Het geplande Eindpunt van de Vraag loopt API
description: De volgende secties lopen door de diverse API vraag u voor het runnen van geplande vragen met de Dienst API van de Vraag kunt maken.
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Geplande eindpunt van vraaglooppas

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik zijn, bent u bereid beginnen het richten van vraag aan [!DNL Query Service] API. De volgende secties lopen door diverse API vraag u kunt maken gebruikend [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Hiermee wordt een lijst met alle uitvoeringen voor een opgegeven geplande query opgehaald

U kunt een lijst van alle looppas voor een specifieke geplande vraag terugwinnen, ongeacht of zij momenteel lopen of reeds voltooid zijn. Dit gebeurt door een verzoek van de GET aan `/schedules/{SCHEDULE_ID}/runs` eindpunt, waarbij `{SCHEDULE_ID}` is de `id` De waarde van de geplande vraag waarvan looppas u wenst terug te winnen.

**API-indeling**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` De waarde van de geplande query die u wilt ophalen. |
| `{QUERY_PARAMETERS}` | (*Optioneel*) Parameters die aan het verzoekweg worden toegevoegd die de resultaten vormen die in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven. |

**Query-parameters**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van uitvoeringen voor een opgegeven geplande query. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle looppas beschikbaar voor de gespecificeerde geplande vraag terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated`. Bijvoorbeeld: `orderby=created` sorteert de resultaten in oplopende volgorde. Een `-` vóór het maken (`orderby=-created`) sorteert objecten in aflopende volgorde. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Geef een tijdstempel voor de ISO-indeling op om de resultaten te bestellen. Als er geen begindatum is opgegeven, retourneert de API-aanroep eerst de oudste uitvoering en worden de meest recente resultaten weergegeven<br> Met ISO-tijdstempels kunt u de datum en tijd korter maken. De basis ISO-tijdstempels hebben de notatie: `2020-09-07` om de datum 7 september 2020 uit te drukken. Een complexer voorbeeld zou worden geschreven zoals `2022-11-05T08:15:30-05:00` en komt overeen met 5 november 2022, 8:15:30 uur &#39;s ochtends, Amerikaanse Eastern Standard Time. Een tijdzone kan worden opgegeven met een UTC-verschuiving en wordt aangeduid met het achtervoegsel &quot;Z&quot; (`2020-01-01T01:01:01Z`). Als er geen tijdzone is opgegeven, wordt de standaardwaarde nul gebruikt. |
| `property` | Filterresultaten op basis van velden. De filters **moet** zijn aan HTML ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created`, `state`, en `externalTrigger`. De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan), en  `==` (gelijk aan), en `!=` (niet gelijk aan). Bijvoorbeeld: `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` retourneert alle handmatig gemaakte, geslaagd en na 20 april 2019 gemaakte uitvoeringen. |

**Verzoek**

Het volgende verzoek wint de laatste vier looppas voor de gespecificeerde geplande vraag terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>U kunt de waarde van `_links.cancel` tot [Een run voor een opgegeven geplande query stoppen](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Breng onmiddellijk een looppas voor een specifieke geplande vraag teweeg

U kunt een looppas voor een gespecificeerde geplande vraag onmiddellijk teweegbrengen door een verzoek van de POST aan `/schedules/{SCHEDULE_ID}/runs` eindpunt, waarbij `{SCHEDULE_ID}` is de `id` De waarde van de geplande query waarvan u de uitvoering wilt activeren.

**API-indeling**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt details over een looppas voor een specifieke geplande vraag terugwinnen door een verzoek van de GET aan `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt en het verstrekken van zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg.

**API-indeling**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` De waarde van de geplande vraag waarvan looppas u wenst om details van terug te winnen. |
| `{RUN_ID}` | De `id` de waarde van de run die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt een looppas voor een specifieke geplande vraag onmiddellijk tegenhouden door een verzoek van de PATCH aan `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt en het verstrekken van zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg.

**API-indeling**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` De waarde van de geplande vraag waarvan looppas u wenst om details van terug te winnen. |
| `{RUN_ID}` | De `id` de waarde van de run die u wilt ophalen. |

**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
