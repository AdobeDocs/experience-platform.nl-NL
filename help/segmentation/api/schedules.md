---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Planningen
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Handleiding voor ontwikkelaars van planningen

intro

- Een lijst met schema&#39;s ophalen
- Een nieuw schema maken
- Een specifiek schema ophalen
- Een specifiek schema bijwerken
- Een specifiek schema verwijderen

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de segmentatie-API. Lees de ontwikkelaarsgids voor [segmentatie voordat u verdergaat](./getting-started.md).

In het bijzonder, omvat de [begonnen sectie](./getting-started.md#getting-started) van de de ontwikkelaarsgids van de Segmentatie verbindingen aan verwante onderwerpen, een gids aan het lezen van de steekproefAPI vraag in het document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke API van het Platform van de Ervaring met succes te maken.

## Een lijst met schema&#39;s ophalen

U kunt een lijst van alle programma&#39;s voor uw IMS Organisatie terugwinnen door een GET verzoek aan het `/config/schedules` eindpunt te doen.

**API-indeling**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatief*) Parameters die aan de verzoekweg worden toegevoegd die de resultaten vormen in de reactie zijn teruggekeerd. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`). De beschikbare parameters worden hieronder weergegeven.

**Parameters query**

Hieronder volgt een lijst met beschikbare queryparameters voor lijsten. Al deze parameters zijn optioneel. Het maken van een vraag aan dit eindpunt zonder parameters zal alle programma&#39;s beschikbaar voor uw organisatie terugwinnen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `start` | Geeft aan vanaf welke pagina de verschuiving begint. Deze waarde is standaard 0. |
| `limit` | Geeft het aantal geretourneerde schema&#39;s op. Deze waarde is standaard 100. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst met schema&#39;s voor de opgegeven IMS-organisatie als JSON.

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Een nieuw schema maken

U kunt een nieuw programma tot stand brengen door een POST- verzoek aan het `/config/schedules` eindpunt te doen.

**API-indeling**

```http
POST /config/schedules
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parameter | Beschrijving |
| --------- | ------------ |
| `name` | **Vereist.** De naam van het schema als een tekenreeks. |
| `type` | **Vereist.** Het type taak als tekenreeks. De twee ondersteunde typen zijn `batch_segmentation` en `export`. |
| `properties` | **Vereist.** Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `properties.segments` | **Vereist als`type`gelijk is`batch_segmentation`.** Het gebruiken `["*"]` zorgt ervoor alle segmenten inbegrepen zijn. |
| `schedule` | **Vereist.** Een tekenreeks met het taakschema. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s. In dit voorbeeld betekent &quot;0 0 1 *&quot; dat dit schema om middernacht op het eerste van elke maand zal lopen. |
| `state` | *Optioneel.* Een tekenreeks die de staat van het schema bevat. De twee ondersteunde staten zijn `active` en `inactive`. De status is standaard ingesteld op `inactive`. |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerd programma terug.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Een specifiek schema ophalen

U kunt gedetailleerde informatie over een specifiek programma terugwinnen door een GET verzoek aan het `/config/schedules` eindpunt te doen en de `id` waarde van het programma in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: De `id` waarde van het programma u wilt terugwinnen.

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over het gespecificeerde programma terug.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## Details van een specifiek schema bijwerken

U kunt een gespecificeerd programma bijwerken door een verzoek van de PATCH aan het `/config/schedules` eindpunt en het verstrekken van de `id` waarde van het programma in de verzoekweg te doen.

De PATCH-aanvraag ondersteunt twee verschillende paden: `/state` en `/schedule`.

### Status schema bijwerken

U kunt de status van het programma bijwerken `/state` - ACTIEF of INACTIEF. Als u de status wilt bijwerken, moet u de waarde instellen op `active` of `inactive`.

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: De `id` waarde van het programma dat u wilt bijwerken.

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u de staat van het programma bijwerkt, moet u de waarde van plaatsen `path` aan `/state`. |
| `value` | De bijgewerkte waarde van de `/state`. U kunt deze waarde instellen als `active` of `inactive` om het schema te activeren of te deactiveren. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

### Plan voor uitsnijden bijwerken

U kunt het uitsnijdschema bijwerken `schedule` met behulp van dit schema. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s.

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: De `id` waarde van het programma dat u wilt bijwerken.

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u het programma van het programma bijwerkt, moet u de waarde van plaatsen `path` aan `/schedule`. |
| `value` | De bijgewerkte waarde van de `/state`. Deze waarde moet de vorm hebben van een uitsnijdschema. In dit voorbeeld, zal het programma op de tweede van elke maand lopen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Een specifiek schema verwijderen

U kunt verzoeken om een gespecificeerd programma te schrappen door een verzoek van de SCHRAPPING aan het `/config/schedules` en het verstrekken van de waarde van het programma in de verzoekweg te doen `id` .

**API-indeling**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: De `id` waarde van het programma u wilt schrappen.

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 204 (Geen inhoud) met het volgende bericht:

```json
(No Content) Schedule deleted successfully
```

## Volgende stappen
