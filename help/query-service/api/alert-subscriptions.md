---
keywords: Experience Platform;thuis;populaire onderwerpen;vraagdienst;de dienst van de vraag;alarm;
title: API-eindpunt voor abonnementen waarschuwen
description: Deze gids verstrekt steekproefHTTP- verzoeken en reacties voor diverse API vraag u aan het waakzame abonnementseindpunt met de Dienst API van de Vraag kunt maken.
source-git-commit: cab7fcfda1bd8f6462af6e631f1fcee1f354d26b
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 0%

---

# API-eindpunt voor abonnementen waarschuwen

Met Adobe Experience Platform Query Service kunt u zich abonneren op waarschuwingen voor zowel ad-hocquery&#39;s als geplande query&#39;s. Waarschuwingen kunnen via e-mail worden ontvangen, binnen de gebruikersinterface van het Platform of beide. De inhoud van het bericht is hetzelfde voor waarschuwingen in het Platform en e-mailwaarschuwingen. Op dit moment kunnen querywaarschuwingen alleen worden geabonneerd op [Query Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Als u e-mailwaarschuwingen wilt ontvangen, moet u deze instelling eerst inschakelen in de gebruikersinterface. Zie de documentatie voor [instructies voor het inschakelen van e-mailwaarschuwingen](../../observability/alerts/ui.md#enable-email-alerts).

In de onderstaande tabel worden de ondersteunde typen waarschuwingen voor verschillende typen query&#39;s uitgelegd:

| Type query | Ondersteunde typen waarschuwingen |
|---|---|
| Ad-hocquery&#39;s | `success` of `failed` executies. |
| Geplande query&#39;s | `start`, `success`, of `failed` executies. |

>[!NOTE]
>
>Alle vragen niet-SELECT steunen waakzame abonnementen, en u te hoeven niet de vraagschepper te zijn om op een alarm in te tekenen. Andere gebruikers kunnen zich ook inschrijven voor waarschuwingen over een query die ze niet hebben gemaakt.

De volgende waarschuwingen zijn van toepassing zonder een waarschuwingsabonnement:

* Wanneer een batchquerytaak is voltooid, ontvangen gebruikers een melding.
* Wanneer de duur van een batch-querytaak een drempel overschrijdt, wordt een waarschuwing geactiveerd voor de persoon die de query heeft gepland.

>[!NOTE]
>
>De vragen die voor het testen worden gebruikt kunnen van dit alarm worden uitgesloten indien geschikt gevormd.

## Voorbeeld-API-aanroepen

De volgende secties lopen door diverse API vraag u het gebruiken van de Dienst API van de Vraag kunt maken. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

## Een lijst met alle waarschuwingen voor een organisatie en een sandbox ophalen {#get-list-of-org-alert-subs}

Hiermee wordt een lijst met alle waarschuwingen voor een organisatie-sandbox opgehaald door een GET-aanvraag in te dienen bij de `/alert-subscriptions` eindpunt.

**API-indeling**

```http
GET /alert-subscriptions
```

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert een HTTP 200-status en de `alerts` array met paginering- en versiegegevens. De `alerts` array bevat details van alle waarschuwingen voor een organisatie en een bepaalde sandbox. Er zijn maximaal drie waarschuwingen beschikbaar per reactie, één signalering per type signalering is opgenomen in de responsinstantie.

>[!NOTE]
>
>De `alerts._links` object in het `alerts` array is afgekapt voor beknoptheid. Een volledig voorbeeld van het `alerts._links` kan worden gevonden in het dialoogvenster [antwoord op het verzoek van de POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `alerts.assetId` | De vraag-id die aan de waarschuwing met een bepaalde query is gekoppeld. |
| `alerts.id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing is opgeslagen, de `alertType`en de flow-id. Informatie over de beschikbare waarschuwingen vindt u in de [Documentatie van het dashboard met waarschuwingen voor Platforms](../../observability/alerts/ui.md). |
| `alerts.status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled`, en `disabling`. Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alerts.alertType` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `alerts._links` | Verstrekt informatie over de beschikbare methodes en de eindpunten die kunnen worden gebruikt om, informatie terug te winnen bij te werken uit te geven of te schrappen met betrekking tot deze waakzame identiteitskaart |
| `_page` | Het object bevat eigenschappen die de volgorde, grootte, het totale aantal pagina&#39;s en de huidige pagina beschrijven. |
| `_links` | Het object bevat URI-verwijzingen waarmee de volgende of vorige pagina met bronnen kan worden opgehaald. |

## Haal de informatie van het waakzame abonnement voor een bepaalde vraag of programma identiteitskaart op {#retrieve-all-alert-subscriptions-by-id}

Haal de informatie van het waakzame abonnement voor een bepaalde vraag ID of programma identiteitskaart door een verzoek van de GET aan `/alert-subscriptions/{QUERY_ID}` of de `/alert-subscriptions/{SCHEDULE_ID}` eindpunt.

**API-indeling**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{QUERY_ID}` | De id van de query waarvoor u de abonnementsgegevens wilt retourneren. |
| `{SCHEDULE_ID}` | De id van de geplande query waarvoor u de abonnementsgegevens wilt retourneren. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert de HTTP-status 200 en de `alerts` array die abonnementsgegevens voor de opgegeven query- of planning-id bevat.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `assetId` | De waarschuwing is gekoppeld aan deze id. De id kan een query-id of een planning-id zijn. |
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing is opgeslagen, de `alertType`en de flow-id. Informatie over de beschikbare waarschuwingen vindt u in de [Documentatie van het dashboard met waarschuwingen voor Platforms](../../observability/alerts/ui.md). |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled`, en `disabling`. Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alertType` | Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `subscriptions.emailNotifications` | Een array met Adobe geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd om e-mails voor de waarschuwing te ontvangen. |
| `subscriptions.inContextNotifications` | Een array met Adobe geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd op UI-meldingen voor de waarschuwing. |

## Hiermee worden abonnementsgegevens voor een bepaalde query of planning-id en een waarschuwingstype opgehaald {#get-alert-info-by-id-and-alert-type}

Haal de abonnementsgegevens voor een bepaalde id en een bepaald type waarschuwing op door een GET-aanvraag in te dienen bij de `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` eindpunt. Dit is van toepassing op zowel vraag als geplande vraag IDs.

**API-indeling**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `QUERY_ID` | De unieke id voor de query die moet worden bijgewerkt. |
| `SCHEDULE_ID` | De unieke id voor de geplande query die moet worden bijgewerkt. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwoord**

Een succesvolle reactie keert een status van HTTP van 200 en alle alarm terug die aan worden geabonneerd. Dit omvat de waarschuwings-id, het type waarschuwing, de Adobe geregistreerde e-mailadressen van de abonnee en het bijbehorende berichtkanaal.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `assetId` | De vraag-id die aan de waarschuwing met een bepaalde query is gekoppeld. |
| `alertType` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.inContextNotifications` | Een array met Adobe geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd op UI-meldingen voor de waarschuwing. |
| `subscriptions.emailNotifications` | Een array met Adobe geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd om e-mails voor de waarschuwing te ontvangen. |

## Hiermee wordt een lijst opgehaald met alle waarschuwingen waarop een gebruiker is geabonneerd {#get-alert-subscription-list}

Hiermee wordt een lijst opgehaald met alle waarschuwingen waarop een gebruiker is geabonneerd door een GET-aanvraag in te dienen bij de `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` eindpunt. De reactie omvat de waakzame naam, identiteitskaarts, status, waakzaam type, en berichtkanalen.

**API-indeling**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `{EMAIL_ID}` | Een e-mailadres dat is geregistreerd voor een Adobe-account, wordt gebruikt om de gebruikers te identificeren die zijn geabonneerd op waarschuwingen. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 en de `items` array met bijzonderheden over de waarschuwingen waarop de `emailId` verstrekt.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing is opgeslagen, de `alertType`en de flow-id. Informatie over de beschikbare waarschuwingen vindt u in de [Documentatie van het dashboard met waarschuwingen voor Platforms](../../observability/alerts/ui.md). |
| `assetId` | De vraag-id die aan de waarschuwing met een bepaalde query is gekoppeld. |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled`, en `disabling`. Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alertType` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.inContextNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. A `true` waarde bevestigt dat waarschuwingen via de gebruikersinterface moeten worden verstrekt. A `false` zorgt ervoor dat de gebruikers niet via dat kanaal op de hoogte worden gesteld. |
| `subscriptions.emailNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. A `true` value bevestigt dat waarschuwingen via e-mail moeten worden verzonden . A `false` zorgt ervoor dat de gebruikers niet via dat kanaal op de hoogte worden gesteld. |

## Een waarschuwing maken en gebruikers abonneren {#subscribe-users}

Als u een waarschuwing wilt maken en een gebruiker wilt abonneren om deze te ontvangen, voert u een `POST` verzoek aan de `/alert-subscriptions` eindpunt. Dit verzoek associeert een vraag aan een pas gecreeerd alarm gebruikend een `assetId` eigenschap, en abonneert gebruikers op waarschuwingen voor die query via het gebruik van `emailIds`.

>[!IMPORTANT]
>
>U kunt maximaal vijf Adobe geregistreerde e-mailadressen doorgeven in één aanvraag. Als u zich wilt abonneren op meer dan vijf gebruikers, moeten daarop volgende verzoeken worden ingediend.

**API-indeling**

```http
POST /alert-subscriptions
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `assetId` | De waarschuwing is gekoppeld aan deze id. De id kan een query-id of een planning-id zijn. |
| `alertType` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.emailIds` | Een array met e-mailadressen om de gebruikers te identificeren die de waarschuwingen moeten ontvangen. De e-mailadressen **moet** worden geregistreerd bij een Adobe-account. |
| `subscriptions.inContextNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. A `true` waarde bevestigt dat waarschuwingen via de gebruikersinterface moeten worden verstrekt. A `false` zorgt ervoor dat de gebruikers niet via dat kanaal op de hoogte worden gesteld. |
| `subscriptions.emailNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. A `true` value bevestigt dat waarschuwingen via e-mail moeten worden verzonden . A `false` zorgt ervoor dat de gebruikers niet via dat kanaal op de hoogte worden gesteld. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) met details van de zojuist gemaakte waarschuwing.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing is opgeslagen, de `alertType`en de flow-id. Informatie over de beschikbare waarschuwingen vindt u in de [Documentatie van het dashboard met waarschuwingen voor Platforms](../../observability/alerts/ui.md). |
| `_links` | Verstrekt informatie over de beschikbare methodes en de eindpunten die kunnen worden gebruikt om, informatie terug te winnen bij te werken uit te geven of te schrappen met betrekking tot deze waakzame identiteitskaart |

## Een waarschuwing in- of uitschakelen {#enable-or-disable-alert}

Deze aanvraag verwijst naar een bepaalde waarschuwing met een vraag- of plannings-id en een waarschuwingstype en werkt de waarschuwingsstatus bij naar een van de volgende `enable` of `disable`. U kunt de status van een waarschuwing bijwerken door een `PATCH` verzoek aan de `/alert-subscriptions/{queryId}/{alertType}` of `/alert-subscriptions/{scheduleId}/{alertType}` eindpunt.

**API-indeling**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul>U moet het huidige waakzame type in eindpuntnamespace specificeren om het te veranderen. |
| `QUERY_ID` | De unieke id voor de query die moet worden bijgewerkt. |
| `SCHEDULE_ID` | De unieke id voor de geplande query die moet worden bijgewerkt. |

**Verzoek**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | De uit te voeren bewerking. Momenteel is de enige toegestane waarde `replace`. |
| `path` | Deze waarde heeft betrekking op de naamruimte in het eindpunt. Momenteel is de enige toegestane waarde `/status`. |
| `value` | In een succesvol verzoek van de PATCH verandert dit `status` waarde van de waarschuwing. Momenteel zijn de geaccepteerde waarden `enable` of `disable`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van de waakzame status, type, en identiteitskaart evenals de vraag terug het met betrekking tot heeft.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing is opgeslagen, de `alertType`en de flow-id. Informatie over de beschikbare waarschuwingen vindt u in de [Documentatie van het dashboard met waarschuwingen voor Platforms](../../observability/alerts/ui.md). |
| `assetId` | De waarschuwing is gekoppeld aan deze id. De id kan een query-id of een planning-id zijn. |
| `alertType` | Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled`, en `disabling`. Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |

## De waarschuwing voor een bepaald type query en waarschuwing verwijderen {#delete-alert-info-by-id-and-alert-type}

Een waarschuwing voor een bepaalde vraag- of plannings-id en een waarschuwingstype verwijderen door een DELETE-aanvraag in te dienen bij de `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` of `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` eindpunt.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | Het type waarschuwing. Er zijn drie mogelijke waarden voor een waarschuwing: <ul><li>`start`: Hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: Meldt de gebruiker wanneer de query is voltooid.</li><li>`failure`: Hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> De DELETE-aanvraag geldt alleen voor het specifieke type waarschuwing dat wordt gegeven. |
| `QUERY_ID` | De unieke id voor de query die moet worden bijgewerkt. |
| `SCHEDULE_ID` | De unieke id voor de geplande query die moet worden bijgewerkt. |

**Verzoek**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert een HTTP 200-status en een bevestigingsbericht met de element-id en het waarschuwingstype van de verwijderde waarschuwing.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Volgende stappen

In deze handleiding wordt ingegaan op het gebruik van het `/alert-subscriptions` eindpunt in de Dienst API van de Vraag. Na het lezen van deze gids hebt u nu een beter inzicht in hoe te om een alarm voor een vraag tot stand te brengen, gebruikers aan de alarm in te schrijven, de soorten alarm beschikbaar en hoe de waakzame informatie van het abonnement kan worden teruggewonnen, worden bijgewerkt en worden geschrapt.

Zie de [API-handleiding voor query-service](./getting-started.md) voor meer informatie over andere beschikbare functies en bewerkingen.
