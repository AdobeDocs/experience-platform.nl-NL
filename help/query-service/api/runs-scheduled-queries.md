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

Nu u begrijpt welke headers u moet gebruiken, bent u klaar om aanroepen uit te voeren naar de [!DNL Query Service] API. De volgende secties doorlopen de verschillende API-aanroepen die u met de [!DNL Query Service] API kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Hiermee wordt een lijst met alle uitvoeringen voor een opgegeven geplande query opgehaald

U kunt een lijst van alle looppas voor een specifieke geplande vraag terugwinnen, ongeacht of zij momenteel lopen of reeds voltooid zijn. Dit wordt gedaan door een verzoek van de GET aan het `/schedules/{SCHEDULE_ID}/runs` eindpunt, waar `{SCHEDULE_ID}` de `id` waarde van de geplande vraag is waarvan looppas u wenst terug te winnen.

**API formaat**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van de geplande query die u wilt ophalen. |
| `{QUERY_PARAMETERS}` | (*Facultatieve*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden. De beschikbare parameters worden hieronder weergegeven. |

**de parameters van de Vraag**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van uitvoeringen voor een opgegeven geplande query. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle looppas beschikbaar voor de gespecificeerde geplande vraag terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated` . `orderby=created` sorteert de resultaten bijvoorbeeld in oplopende volgorde. Wanneer u een `-` vóór het maken (`orderby=-created` ) toevoegt, worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Geef een tijdstempel voor de ISO-indeling op om de resultaten te bestellen. Als geen begindatum wordt gespecificeerd, zal de API vraag de oudste looppas eerst terugkeren, dan zal blijven van recentere resultaten <br> timestamps van ISO staan voor verschillende niveaus van granulariteit in de datum en de tijd toe. De basis-ISO-tijdstempels hebben de notatie: `2020-09-07` voor het uitdrukken van de datum 7 september 2020. Een complexer voorbeeld zou als `2022-11-05T08:15:30-05:00` worden geschreven en beantwoordt aan 5 November, 2022, 8 :15: 30 am, de Tijd van de Norm van de V.S. Een timezone kan met een UTC compensatie worden voorzien en door het achtervoegsel &quot;Z&quot; (`2020-01-01T01:01:01Z`) wordt aangeduid. Als er geen tijdzone is opgegeven, wordt de standaardwaarde nul gebruikt. |
| `property` | Filterresultaten op basis van velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created` , `state` en `externalTrigger` . De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan) en `==` (gelijk aan) en `!=` (niet gelijk aan). `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` retourneert bijvoorbeeld alle bewerkingen die handmatig zijn gemaakt, geslaagd en gemaakt na 20 april 2019. |

**Verzoek**

Het volgende verzoek wint de laatste vier looppas voor de gespecificeerde geplande vraag terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
>U kunt de waarde van `_links.cancel` gebruiken om [ een looppas voor een gespecificeerde geplande vraag ](#immediately-stop-a-run-for-a-specific-scheduled-query) tegen te houden.

### Breng onmiddellijk een looppas voor een specifieke geplande vraag teweeg

U kunt een run voor een opgegeven geplande query onmiddellijk activeren door een aanvraag voor een POST in te dienen bij het `/schedules/{SCHEDULE_ID}/runs` -eindpunt, waarbij `{SCHEDULE_ID}` de `id` -waarde is van de geplande query waarvan u de uitvoering wilt activeren.

**API formaat**

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

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Haal details van een looppas voor een specifieke geplande vraag terug

U kunt details over een looppas voor een specifieke geplande vraag terugwinnen door een verzoek van de GET tot het `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt te richten en zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg te verstrekken.

**API formaat**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande query waarvan u de details wilt ophalen. |
| `{RUN_ID}` | De `id` -waarde van de uitvoering die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

U kunt een looppas voor een specifieke geplande vraag onmiddellijk tegenhouden door een verzoek van de PATCH aan het `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` eindpunt te doen en zowel identiteitskaart van de geplande vraag als looppas in de verzoekweg te verstrekken.

**API formaat**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van de geplande query waarvan u de details wilt ophalen. |
| `{RUN_ID}` | De `id` -waarde van de uitvoering die u wilt ophalen. |

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

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
