---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;alert;
title: Alert Subscriptions Endpoint
description: Deze gids verstrekt steekproefHTTP- verzoeken en reacties voor diverse API vraag u aan het waakzame abonnementseindpunt met de Dienst API van de Vraag kunt maken.
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3213'
ht-degree: 0%

---

# Alert Abonnementen, eindpunt

Met Adobe Experience Platform Query Service kunt u zich abonneren op waarschuwingen voor zowel ad-hocquery&#39;s als geplande query&#39;s. Waarschuwingen kunnen via e-mail worden ontvangen, binnen de gebruikersinterface van Experience Platform of beide. De inhoud van het bericht is gelijk voor waarschuwingen in Experience Platform en e-mailberichten.

## Aan de slag

De eindpunten die in deze gids worden gebruikt maken deel uit van Adobe Experience Platform [ API van de Dienst van de Vraag ](https://developer.adobe.com/experience-platform-apis/references/query-service/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

>[!IMPORTANT]
>
>Als u e-mailwaarschuwingen wilt ontvangen, moet u deze instelling eerst inschakelen in de gebruikersinterface. Zie de documentatie voor [ instructies op hoe te om e-mailalarm ](../../observability/alerts/ui.md#enable-email-alerts) toe te laten.

## Typen waarschuwingen {#alert-types}

In de onderstaande tabel worden de ondersteunde typen querywaarschuwingen beschreven:

>[!IMPORTANT]
>
>Het waarschuwingstype `delay` of [!UICONTROL Query Run Delay] wordt momenteel niet ondersteund door de API voor Query Service. Deze waarschuwing brengt u op de hoogte als er een vertraging in het resultaat van een geplande vraaguitvoering voorbij een gespecificeerde drempel is. Als u deze waarschuwing wilt gebruiken, moet u een aangepaste tijd instellen die een waarschuwing activeert wanneer de query voor die duur wordt uitgevoerd zonder dat dit wordt voltooid of mislukt. Leren hoe te om dit alarm in UI te plaatsen, verwijs naar de [ vraagprogramma&#39;s ](../ui/query-schedules.md#alerts-for-query-status) documentatie of de [ gids aan gealigneerde vraagacties ](../ui/monitor-queries.md#query-run-delay).

| Type waarschuwing | Beschrijving |
|---|---|
| `start` | Deze waarschuwing brengt u op de hoogte wanneer een geplande vraaglooppas in werking wordt gesteld of begint te verwerken. |
| `success` | Deze waarschuwing geeft aan wanneer een geplande query correct is uitgevoerd en geeft aan dat de query zonder fouten is uitgevoerd. |
| `failed` | Deze waarschuwing treedt op wanneer een geplande query een fout aantreft of niet met succes wordt uitgevoerd. Hiermee kunt u problemen snel identificeren en verhelpen. |
| `quarantine` | Dit alarm wordt geactiveerd wanneer een geplande vraaglooppas in quarantined staat wordt gezet. Wanneer query&#39;s zijn ingeschreven in de quarantainefunctie, wordt elke geplande query die tien opeenvolgende regels mislukt, automatisch in een [!UICONTROL Quarantined] -status geplaatst. Vervolgens hebben zij uw tussenkomst nodig voordat verdere executies kunnen plaatsvinden. |

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

Haal een lijst op met alle waarschuwingen voor een organisatie-sandbox door een GET-aanvraag in te dienen bij het `/alert-subscriptions` -eindpunt.

**API formaat**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (Facultatief) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (&amp;). De beschikbare parameters worden hieronder weergegeven. |

**de parameters van de Vraag**

Hieronder volgt een lijst met beschikbare queryparameters voor het weergeven van query&#39;s. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle vragen terugwinnen beschikbaar voor uw organisatie.

| Parameter | Beschrijving |
| --------- | ----------- |
| `orderby` | Het veld dat de volgorde van de resultaten aangeeft. De ondersteunde velden zijn `created` en `updated` . Voeg aan de naam van de eigenschap `+` voor oplopende volgorde en `-` voor aflopende volgorde toe. De standaardwaarde is `-created` . Merk op dat het plusteken (`+`) met `%2B` moet worden beschermd. `%2Bcreated` is bijvoorbeeld de waarde voor een oplopende, gemaakte volgorde. |
| `pagesize` | Gebruik deze parameter om het aantal verslagen te controleren u van de API vraag per pagina wilt halen. De standaardlimiet is ingesteld op een maximum van 50 records per pagina. |
| `page` | Geef het paginanummer op van de geretourneerde resultaten waarvoor u de records wilt zien. |
| `property` | De resultaten filteren op basis van gekozen velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. Met de volgende eigenschappen kunt u filteren: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> De ondersteunde operatoren zijn `==` (gelijk aan). `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert bijvoorbeeld de waarschuwing met een overeenkomende id. |

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

**Reactie**

Een geslaagde reactie retourneert een HTTP 200-status en de `alerts` -array met paginering en versiegegevens. De array `alerts` bevat details van alle waarschuwingen voor een organisatie en een bepaalde sandbox. Er zijn maximaal drie waarschuwingen beschikbaar per reactie, één signalering per type signalering is opgenomen in de responsinstantie.

>[!NOTE]
>
>Het `alerts._links` -object in de `alerts` -array is afgebroken om kort te zijn. Een volledig voorbeeld van het `alerts._links` voorwerp kan in de [ reactie van het verzoek van de POST ](#subscribe-users) worden gevonden.

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
| `alerts.id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing, de `alertType` en de flow-id zijn opgeslagen. De informatie over het beschikbare alarm kan in de [ het dashboarddocumentatie van het Alarm van Experience Platform ](../../observability/alerts/ui.md) worden gevonden. |
| `alerts.status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled` en `disabling` . Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alerts.alertType` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul> |
| `alerts._links` | Verstrekt informatie over de beschikbare methodes en de eindpunten die kunnen worden gebruikt om, informatie terug te winnen bij te werken uit te geven of te schrappen met betrekking tot deze waakzame identiteitskaart |
| `_page` | Het object bevat eigenschappen die de volgorde, grootte, het totale aantal pagina&#39;s en de huidige pagina beschrijven. |
| `_links` | Het object bevat URI-verwijzingen waarmee de volgende of vorige pagina met bronnen kan worden opgehaald. |

## Haal de informatie van het waakzame abonnement voor een bepaalde vraag of programma identiteitskaart op {#retrieve-all-alert-subscriptions-by-id}

Haal de informatie van het waakzame abonnement voor een bepaalde vraag ID of programma identiteitskaart door een GET verzoek aan `/alert-subscriptions/{QUERY_ID}` of het `/alert-subscriptions/{SCHEDULE_ID}` eindpunt te doen.

**API formaat**

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

**Reactie**

Een geslaagde reactie retourneert een HTTP-status van 200 en de `alerts` -array die abonnementsgegevens voor de opgegeven vraag- of plannings-id bevat.

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
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing, de `alertType` en de flow-id zijn opgeslagen. De informatie over het beschikbare alarm kan in de [ het dashboarddocumentatie van het Alarm van Experience Platform ](../../observability/alerts/ui.md) worden gevonden. |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled` en `disabling` . Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alertType` | Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `subscriptions.emailNotifications` | Een array met Adobe-geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd om e-mails voor de waarschuwing te ontvangen. |
| `subscriptions.inContextNotifications` | Een array met Adobe-geregistreerde e-mailadressen voor gebruikers die zijn geabonneerd op UI-berichten voor de waarschuwing. |

## Hiermee worden abonnementsgegevens voor een bepaalde query of planning-id en een waarschuwingstype opgehaald {#get-alert-info-by-id-and-alert-type}

Haal de informatie van het waakzame abonnement voor een bepaalde identiteitskaart en waakzaam type door een GET verzoek aan het `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` eindpunt te doen. Dit is van toepassing op zowel vraag als geplande vraag IDs.

**API formaat**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | This property describes the state of query implementation that triggers an alert. Het antwoord bevat alleen waarschuwingsabonnementsgegevens voor dit type waarschuwingen. Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
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

**Reactie**

Een succesvolle reactie keert een status van HTTP van 200 en alle alarm terug die aan worden geabonneerd. Dit omvat de waarschuwings-id, het type waarschuwing, de door de Adobe geregistreerde e-mailadressen van de abonnee en het bijbehorende berichtkanaal.

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
| `alertType` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de in Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.inContextNotifications` | Een array met Adobe-geregistreerde e-mailadressen voor gebruikers die zijn geabonneerd op UI-berichten voor de waarschuwing. |
| `subscriptions.emailNotifications` | Een array met Adobe-geregistreerde e-mailadressen voor gebruikers die zich hebben geabonneerd om e-mails voor de waarschuwing te ontvangen. |

## Hiermee wordt een lijst opgehaald met alle waarschuwingen waarop een gebruiker is geabonneerd {#get-alert-subscription-list}

Haal een lijst op van alle waarschuwingen waarop een gebruiker is geabonneerd door een GET-aanvraag in te dienen bij het `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` -eindpunt. De reactie omvat de waakzame naam, identiteitskaarts, status, waakzaam type, en berichtkanalen.

**API formaat**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `{EMAIL_ID}` | Een e-mailadres dat bij een Adobe-account is geregistreerd, wordt gebruikt om de gebruikers te identificeren die zijn geabonneerd op waarschuwingen. |
| `orderby` | Het veld dat de volgorde van de resultaten aangeeft. De ondersteunde velden zijn `created` en `updated` . Voeg aan de naam van de eigenschap `+` voor oplopende volgorde en `-` voor aflopende volgorde toe. De standaardwaarde is `-created` . Merk op dat het plusteken (`+`) met `%2B` moet worden beschermd. `%2Bcreated` is bijvoorbeeld de waarde voor een oplopende, gemaakte volgorde. |
| `pagesize` | Gebruik deze parameter om het aantal verslagen te controleren u van de API vraag per pagina wilt halen. De standaardlimiet is ingesteld op een maximum van 50 records per pagina. |
| `page` | Geef het paginanummer op van de geretourneerde resultaten waarvoor u de records wilt zien. |
| `property` | De resultaten filteren op basis van gekozen velden. De filters **moeten** HTML zijn ontsnapt. Met komma&#39;s kunt u meerdere sets filters combineren. De volgende eigenschappen staan filtering toe: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> De ondersteunde operatoren zijn `==` (gelijk aan). `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retourneert bijvoorbeeld de waarschuwing met een overeenkomende id. |

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

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 en de array `items` met gegevens over de waarschuwingen waarop de opgegeven `emailId` heeft geabonneerd.

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
| `name` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing, de `alertType` en de flow-id zijn opgeslagen. De informatie over het beschikbare alarm kan in de [ het dashboarddocumentatie van het Alarm van Experience Platform ](../../observability/alerts/ui.md) worden gevonden. |
| `assetId` | De vraag-id die aan de waarschuwing met een bepaalde query is gekoppeld. |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled` en `disabling` . Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |
| `alertType` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de in Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.inContextNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. Een `true` -waarde bevestigt dat waarschuwingen via de gebruikersinterface moeten worden verzonden. Een `false` -waarde zorgt ervoor dat de gebruikers geen meldingen via dat kanaal ontvangen. |
| `subscriptions.emailNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. Een `true` -waarde bevestigt dat waarschuwingen via e-mail moeten worden verzonden. Een `false` -waarde zorgt ervoor dat de gebruikers geen meldingen via dat kanaal ontvangen. |

## Een waarschuwing maken en gebruikers abonneren {#subscribe-users}

Als u een waarschuwing wilt maken en een gebruiker wilt abonneren om deze te ontvangen, dient u een `POST` -aanvraag in bij het `/alert-subscriptions` -eindpunt. Deze aanvraag koppelt een query aan een nieuw gemaakte waarschuwing met behulp van een eigenschap `assetId` en abonneert gebruikers op waarschuwingen voor die query met behulp van `emailIds` .

>[!IMPORTANT]
>
>Je kunt maximaal vijf door Adobe geregistreerde e-mailadressen doorgeven in één aanvraag. Als u zich wilt abonneren op meer dan vijf gebruikers, moeten daarop volgende verzoeken worden ingediend.

**API formaat**

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
| `alertType` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul> |
| `subscriptions` | Een object dat wordt gebruikt om de in Adobe geregistreerde e-mailadressen door te geven die aan de waarschuwingen zijn gekoppeld, en de kanalen waarin de gebruikers de waarschuwingen zullen ontvangen. |
| `subscriptions.emailIds` | Een array met e-mailadressen om de gebruikers te identificeren die de waarschuwingen moeten ontvangen. De e-mailadressen **moeten** aan een rekening van Adobe worden geregistreerd. |
| `subscriptions.inContextNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. Een `true` -waarde bevestigt dat waarschuwingen via de gebruikersinterface moeten worden verzonden. Een `false` -waarde zorgt ervoor dat de gebruikers geen meldingen via dat kanaal ontvangen. |
| `subscriptions.emailNotifications` | Een Booleaanse waarde die bepaalt hoe gebruikers waarschuwingsmeldingen ontvangen. Een `true` -waarde bevestigt dat waarschuwingen via e-mail moeten worden verzonden. Een `false` -waarde zorgt ervoor dat de gebruikers geen meldingen via dat kanaal ontvangen. |

{style="table-layout:auto"}

**Reactie**

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
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing, de `alertType` en de flow-id zijn opgeslagen. De informatie over het beschikbare alarm kan in de [ het dashboarddocumentatie van het Alarm van Experience Platform ](../../observability/alerts/ui.md) worden gevonden. |
| `_links` | Verstrekt informatie over de beschikbare methodes en de eindpunten die kunnen worden gebruikt om, informatie terug te winnen bij te werken uit te geven of te schrappen met betrekking tot deze waakzame identiteitskaart |

## Een waarschuwing in- of uitschakelen {#enable-or-disable-alert}

Deze aanvraag verwijst naar een bepaalde waarschuwing met behulp van een vraag- of plannings-id en een waarschuwingstype en werkt de waarschuwingsstatus bij naar `enable` of `disable` . U kunt de status van een waarschuwing bijwerken door een `PATCH` -aanvraag in te dienen bij het `/alert-subscriptions/{queryId}/{alertType}` - of `/alert-subscriptions/{scheduleId}/{alertType}` -eindpunt.

**API formaat**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul>U moet het huidige waakzame type in eindpuntnamespace specificeren om het te veranderen. |
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
| `op` | De uit te voeren bewerking. Momenteel is de enige toegestane waarde `replace` . |
| `path` | Deze waarde heeft betrekking op de naamruimte in het eindpunt. Momenteel is de enige toegestane waarde `/status` . |
| `value` | In een succesvol PATCH-verzoek wijzigt dit de `status` -waarde van de waarschuwing. Momenteel zijn de toegestane waarden `enable` of `disable` . |

{style="table-layout:auto"}

**Reactie**

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
| `id` | De naam van de waarschuwing. Deze naam wordt gegenereerd door de service Waarschuwingen en wordt gebruikt op het dashboard Waarschuwingen. De waarschuwingsnaam bestaat uit de map waarin de waarschuwing, de `alertType` en de flow-id zijn opgeslagen. De informatie over het beschikbare alarm kan in de [ het dashboarddocumentatie van het Alarm van Experience Platform ](../../observability/alerts/ui.md) worden gevonden. |
| `assetId` | De waarschuwing is gekoppeld aan deze id. De id kan een query-id of een planning-id zijn. |
| `alertType` | Elke waarschuwing kan drie verschillende waarschuwingstypen hebben. Het zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li></ul> |
| `status` | De waarschuwing heeft vier statuswaarden: `enabled`, `enabling`, `disabled` en `disabling` . Een waarschuwing luistert actief naar de gebeurtenissen, gepauzeerd voor toekomstig gebruik terwijl het behouden van alle relevante abonnees en montages, of het overgaan tussen deze staten. |

## De waarschuwing voor een bepaald type query en waarschuwing verwijderen {#delete-alert-info-by-id-and-alert-type}

Verwijder een waarschuwing voor een bepaalde vraag- of plannings-id en een waarschuwingstype door een DELETE-aanvraag in te dienen bij het `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` - of `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` -eindpunt.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `ALERT_TYPE` | Het type waarschuwing. Er zijn vijf waarschuwingsstatussen beschikbaar voor geplande query&#39;s, hoewel er slechts vier waarschuwingsstatussen beschikbaar zijn voor ad-hocquery&#39;s. De waarschuwing `quarantine` is alleen beschikbaar voor geplande query&#39;s. U kunt de waarschuwing `delay` ook alleen instellen via de gebruikersinterface van Experience Platform. Daarom wordt `delay` hier niet beschreven. De beschikbare waarschuwingen zijn: <ul><li>`start`: hiermee wordt een gebruiker gewaarschuwd wanneer de uitvoering van de query is gestart.</li><li>`success`: hiermee wordt de gebruiker op de hoogte gesteld wanneer de query is voltooid.</li><li>`failure`: hiermee wordt de gebruiker gewaarschuwd als de query mislukt.</li><li>`quarantine`: activeert wanneer een geplande vraaglooppas in quarantined staat wordt gezet.</li></ul> Het DELETE-verzoek geldt alleen voor het opgegeven specifieke type waarschuwing. |
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

**Reactie**

Een geslaagde reactie retourneert een HTTP 200-status en een bevestigingsbericht met de element-id en het waarschuwingstype van de verwijderde waarschuwing.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Volgende stappen

Deze gids behandelde het gebruik van het `/alert-subscriptions` eindpunt in de Dienst API van de Vraag. Na het lezen van deze gids hebt u nu een beter inzicht in hoe te om een alarm voor een vraag tot stand te brengen, gebruikers aan de alarm in te schrijven, de soorten alarm beschikbaar en hoe de waakzame informatie van het abonnement kan worden teruggewonnen, worden bijgewerkt en worden geschrapt.

Zie de [ gids van de Dienst API van de Vraag ](./getting-started.md) om meer over andere beschikbare eigenschappen en verrichtingen te leren.
