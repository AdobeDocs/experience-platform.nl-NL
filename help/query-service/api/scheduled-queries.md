---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;geplande query's;geplande query;
solution: Experience Platform
title: Planningeindpunt
description: De volgende secties lopen door de diverse API vraag u voor geplande vragen met de Dienst API van de Vraag kunt maken.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 10c0c5c639226879b1ca25391fc4a1006cf40003
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---

# Planningeindpunt

Leer hoe te om, geplande vragen tot stand te brengen te beheren en te controleren programmatically gebruikend de API van de Programma&#39;s van de Dienst van de Vraag met gedetailleerde informatie en voorbeelden.

## Eisen en voorwaarden

U kunt geplande vragen tot stand brengen gebruikend of een technische rekening (voor authentiek verklaard via de geloofsbrieven van Server-aan-Server van OAuth) of een persoonlijke gebruikersrekening (gebruikerstoken). Adobe raadt echter ten zeerste aan een technische account te gebruiken om ervoor te zorgen dat de geplande query&#39;s zonder onderbreking en veilig worden uitgevoerd, met name bij langdurige of productiewerklasten.

Vragen die met een persoonlijke gebruikersaccount zijn gemaakt, mislukken als de toegang van die gebruiker is ingetrokken of als hun account is uitgeschakeld. Technische rekeningen zorgen voor meer stabiliteit omdat ze niet gekoppeld zijn aan de arbeidsstatus of toegangsrechten van een individuele gebruiker.

>[!IMPORTANT]
>
>Belangrijke overwegingen wanneer het beheren van geplande vragen:<ul><li>Gepland vragen zullen ontbreken als de rekening (technisch of gebruiker) die wordt gebruikt om hen tot stand te brengen toegang of toestemmingen verliest.</li><li>Geplande query&#39;s moeten worden uitgeschakeld voordat ze kunnen worden verwijderd via de API of UI.</li><li>Het voor onbepaalde tijd plannen zonder een einddatum wordt niet gesteund; een einddatum moet altijd worden gespecificeerd.</li></ul>

Voor gedetailleerde begeleiding op rekeningsvereisten, toestemmingsopstelling, en het beheren van geplande vragen, zie de [ documentatie van de programma&#39;s van de Vraag ](../ui/query-schedules.md#technical-account-user-requirements). Voor geleidelijke instructies bij het creëren van en het vormen van een technische rekening, verwijs naar [ de opstelling van Developer Console ](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) en [ technische de rekeningsopstelling van begin tot eind ](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup).

## Voorbeeld-API-aanroepen

Zodra u de noodzakelijke authentificatiekopballen (zie de [ API authentificatiegids ](../../landing/api-authentication.md)) hebt gevormd, kunt u beginnen het maken vraag aan [!DNL Query Service] API. In de volgende secties worden verschillende API-aanroepen met algemene indelingen getoond, bijvoorbeeld aanvragen met vereiste koppen en voorbeeldantwoorden.

### Hiermee wordt een lijst met geplande query&#39;s opgehaald

U kunt een lijst van alle geplande vragen voor uw organisatie terugwinnen door een GET- verzoek aan het `/schedules` eindpunt te doen.

**API formaat**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatieve*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden. De beschikbare parameters worden hieronder weergegeven. |

**de parameters van de Vraag**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van geplande query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle geplande vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Hiermee geeft u het veld op waarmee de resultaten moeten worden geordend. De ondersteunde velden zijn `created` en `updated` . `orderby=created` sorteert de resultaten bijvoorbeeld in oplopende volgorde. Wanneer u een `-` vóór het maken (`orderby=-created` ) toevoegt, worden de items in aflopende volgorde gesorteerd. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. (*Standaardwaarde: 20*) |
| `start` | Geef een tijdstempel voor de ISO-indeling op om de resultaten te bestellen. Als geen begindatum wordt gespecificeerd, zal de API vraag eerst de oudste gecreeerde geplande vraag terugkeren, dan zal blijven van recentere resultaten een lijst maken.<br> Met ISO-tijdstempels kunt u verschillende niveaus van granulariteit opgeven in de datum en tijd. De basis-ISO-tijdstempels hebben de notatie: `2020-09-07` voor het uitdrukken van de datum 7 september 2020. Een complexer voorbeeld zou als `2022-11-05T08:15:30-05:00` worden geschreven en beantwoordt aan 5 November, 2022, 8 :15: 30 am, de Tijd van de Norm van de V.S. Een timezone kan met een UTC compensatie worden voorzien en door het achtervoegsel &quot;Z&quot; (`2020-01-01T01:01:01Z`) wordt aangeduid. Als er geen tijdzone is opgegeven, wordt de standaardwaarde nul gebruikt. |
| `property` | Filterresultaten op basis van velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De ondersteunde velden zijn `created` , `templateId` en `userId` . De lijst met ondersteunde operatoren is `>` (groter dan), `<` (kleiner dan) en `==` (gelijk aan). `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert bijvoorbeeld alle geplande query&#39;s waarbij de gebruiker-id overeenkomt met de opgegeven waarde. |

**Verzoek**

Het volgende verzoek wint de recentste geplande vraag terug die voor uw organisatie wordt gecreeerd.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van geplande vragen voor de gespecificeerde organisatie terug. De volgende reactie keert de recentste geplande vraag terug die voor uw organisatie wordt gecreeerd.

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

U kunt een nieuwe geplande query maken door een POST-aanvraag in te dienen bij het `/schedules` -eindpunt. Wanneer u een geplande query maakt in de API, kunt u deze ook zien in de Query-editor. Voor meer informatie over geplande vragen in UI, te lezen gelieve de [ documentatie van de Redacteur van de Vraag ](../ui/user-guide.md#scheduled-queries).

**API formaat**

```http
POST /schedules
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `query.dbName` | De naam van het gegevensbestand waar de geplande vraag zal lopen. |
| `query.sql` | De SQL-query die moet worden uitgevoerd volgens het gedefinieerde schema. |
| `query.name` | De naam van de geplande query. |
| `query.description` | Een optionele beschrijving voor de geplande query. |
| `schedule.schedule` | Het uitsnijdschema voor de query. Verwijs naar [ Crontab.guru ](https://crontab.guru/) voor een interactieve manier om te creëren, te bevestigen, en gezamenlijke uitdrukkingen te begrijpen. In dit voorbeeld betekent &quot;30 * * *&quot;dat de vraag elk uur bij het minteken van 30 minuten zal lopen.<br><br> Alternatief, kunt u de volgende steno uitdrukkingen gebruiken:<ul><li>`@once`: de query wordt slechts één keer uitgevoerd.</li><li>`@hourly`: de query wordt elk uur uitgevoerd aan het begin van het uur. Dit is gelijk aan de expressie voor uitsnijden `0 * * * *` .</li><li>`@daily`: De query wordt eenmaal per dag om middernacht uitgevoerd. Dit is gelijk aan de expressie voor uitsnijden `0 0 * * *` .</li><li>`@weekly`: de query wordt één keer per week uitgevoerd, op zondag, om middernacht. Dit is gelijk aan de expressie voor uitsnijden `0 0 * * 0` .</li><li>`@monthly`: De query wordt één keer per maand uitgevoerd, op de eerste dag van de maand, om middernacht. Dit is gelijk aan de expressie voor uitsnijden `0 0 1 * *` .</li><li>`@yearly`: De query wordt één keer per jaar uitgevoerd, op 1 januari om middernacht. Dit is gelijk aan de expressie voor uitsnijden `0 0 1 1 *` . |
| `schedule.startDate` | De begindatum voor uw geplande query, geschreven als een UTC-tijdstempel. |

**Reactie**

Een succesvolle reactie keert status 202 (Toegelaten) van HTTP met details van uw onlangs gecreeerde geplande vraag terug. Nadat de geplande query is geactiveerd, verandert de `state` van `REGISTERING` in `ENABLED` .

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
>U kunt de waarde van `_links.delete` gebruiken om [ uw gecreeerde geplande vraag ](#delete-a-specified-scheduled-query) te schrappen.

### Gegevens van een opgegeven geplande query aanvragen

U kunt informatie voor een specifieke geplande vraag terugwinnen door een GET- verzoek aan het `/schedules` eindpunt te doen en zijn identiteitskaart in de verzoekweg te verstrekken.

**API formaat**

```http
GET /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van de geplande query die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
>U kunt de waarde van `_links.delete` gebruiken om [ uw gecreeerde geplande vraag ](#delete-a-specified-scheduled-query) te schrappen.

### Details van een opgegeven geplande query bijwerken

U kunt de details voor een gespecificeerde geplande vraag bijwerken door een PATCH- verzoek aan het `/schedules` eindpunt en door zijn identiteitskaart in de verzoekweg te verstrekken.

De PATCH-aanvraag ondersteunt twee verschillende paden: `/state` en `/schedule/schedule` .

### Geplande querystatus bijwerken

U kunt de status van de geselecteerde geplande query bijwerken door de eigenschap `path` in te stellen op `/state` en de eigenschap `value` op `enable` of `disable` .

**API formaat**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van de geplande query die u wilt PATCH. |


**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | De bewerking die op het queryprogramma moet worden uitgevoerd. De geaccepteerde waarde is `replace` . |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval moet u de waarde `path` instellen op `/state` , aangezien u de status van de geplande query bijwerkt. |
| `value` | De bijgewerkte waarde van de `/state` . Deze waarde kan worden ingesteld als `enable` of `disable` om de geplande query in of uit te schakelen. |

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Geplande queryplanning bijwerken

U kunt het bijsnijdschema van de geplande query bijwerken door de eigenschap `path` in te stellen op `/schedule/schedule` in de hoofdtekst van de aanvraag. Voor meer informatie over kroonprogramma&#39;s, te lezen gelieve het [ formaat van de cron uitdrukking ](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentatie.

**API formaat**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van de geplande query die u wilt PATCH. |

**Verzoek**

Voor deze API-aanvraag wordt de JSON-syntaxis voor patch gebruikt voor het laden. Lees het document met API-basisbeginselen voor meer informatie over hoe JSON Patch werkt.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | De bewerking die op het queryprogramma moet worden uitgevoerd. De geaccepteerde waarde is `replace` . |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval moet u de waarde `path` instellen op `/schedule/schedule` , aangezien u het schema van de geplande query bijwerkt. |
| `value` | De bijgewerkte waarde van de `/schedule` . Deze waarde moet de vorm hebben van een uitsnijdschema. Dus, in dit voorbeeld, zal de geplande vraag elk uur bij het 45 minieme teken in werking stellen. |

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Opgegeven geplande query verwijderen

U kunt een gespecificeerde geplande vraag schrappen door een DELETE- verzoek aan het `/schedules` eindpunt te doen en identiteitskaart van de geplande vraag te verstrekken u in de verzoekweg wilt schrappen.

>[!NOTE]
>
>Het programma **moet** worden onbruikbaar gemaakt alvorens wordt geschrapt.

**API formaat**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van de geplande query die u wilt DELETE. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met het volgende bericht.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
