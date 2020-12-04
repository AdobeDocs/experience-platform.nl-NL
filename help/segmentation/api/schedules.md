---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;schedules;schedule;api;API;
solution: Experience Platform
title: Planningen
topic: developer guide
description: Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---


# Planningeindpunt

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt het `/config/schedules` eindpunt gebruiken om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Voordat u verdergaat, bekijkt u eerst de gids [](./getting-started.md) Aan de slag voor belangrijke informatie die u moet weten om oproepen naar de API met succes te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Een lijst met schema&#39;s ophalen {#retrieve-list}

U kunt een lijst van alle programma&#39;s voor uw IMS Organisatie terugwinnen door een verzoek van de GET tot het `/config/schedules` eindpunt te richten.

**API-indeling**

Het `/config/schedules` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle programma&#39;s beschikbaar voor uw organisatie terugwinnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{START}` | Geeft aan vanaf welke pagina de verschuiving begint. Deze waarde is standaard 0. |
| `{LIMIT}` | Geeft het aantal geretourneerde schema&#39;s op. Deze waarde is standaard 100. |

**Verzoek**

Het volgende verzoek zal de laatste tien programma&#39;s terugwinnen die binnen uw IMS Organisatie worden gepost.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst met schema&#39;s voor de opgegeven IMS-organisatie als JSON.

>[!NOTE]
>
>De volgende reactie is afgebroken voor ruimte, en toont slechts het eerste teruggekeerde programma.

```json
{
    "_page": {
        "totalCount": 10,
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

| Eigenschap | Beschrijving |
| -------- | ------------ |
| `_page.totalCount` | Het totale aantal geretourneerde schema&#39;s. |
| `_page.pageSize` | De grootte van de pagina met schema&#39;s. |
| `children.name` | De naam van het schema als een tekenreeks. |
| `children.type` | Het type taak als tekenreeks. De twee ondersteunde typen zijn &quot;batch_segmentation&quot; en &quot;export&quot;. |
| `children.properties` | Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `children.properties.segments` | Het gebruiken `["*"]` zorgt ervoor alle segmenten inbegrepen zijn. |
| `children.schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s. In dit voorbeeld betekent &quot;0 0 1 *&quot; dat dit schema om middernacht op het eerste van elke maand zal lopen. |
| `children.state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

## Een nieuw schema maken {#create}

U kunt een nieuw programma tot stand brengen door een verzoek van de POST aan het `/config/schedules` eindpunt te doen.

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Eigenschap | Beschrijving |
| -------- | ------------ |
| `name` | **Vereist.** De naam van het schema als een tekenreeks. |
| `type` | **Vereist.** Het type taak als tekenreeks. De twee ondersteunde typen zijn &quot;batch_segmentation&quot; en &quot;export&quot;. |
| `properties` | **Vereist.** Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `properties.segments` | **Vereist wanneer `type` gelijk is aan &quot;batch_segmentation&quot;.** Het gebruiken `["*"]` zorgt ervoor alle segmenten inbegrepen zijn. |
| `schedule` | *Optioneel.* Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s. In dit voorbeeld betekent &quot;0 0 1 *&quot; dat dit schema om middernacht op het eerste van elke maand zal lopen. <br><br>Als deze tekenreeks niet wordt opgegeven, wordt automatisch een door het systeem gegenereerd schema gegenereerd. |
| `state` | *Optioneel.* Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

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

## Een specifiek schema ophalen {#get}

U kunt gedetailleerde informatie over een specifiek programma terugwinnen door een verzoek van de GET aan het `/config/schedules` eindpunt te doen en identiteitskaart van het programma te verstrekken u in de verzoekweg wenst terug te winnen.

**API-indeling**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het programma u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
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
}
```

| Eigenschap | Beschrijving |
| -------- | ------------ |
| `name` | De naam van het schema als een tekenreeks. |
| `type` | Het type taak als tekenreeks. De twee ondersteunde typen zijn `batch_segmentation` en `export`. |
| `properties` | Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `properties.segments` | Het gebruiken `["*"]` zorgt ervoor alle segmenten inbegrepen zijn. |
| `schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd. Dit betekent dat u een taak niet meer dan één keer gedurende een periode van 24 uur kunt plannen. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s. In dit voorbeeld betekent &quot;0 0 1 *&quot; dat dit schema om middernacht op het eerste van elke maand zal lopen. |
| `state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde staten zijn `active` en `inactive`. De status is standaard ingesteld op `inactive`. |

## Details bijwerken voor een specifiek schema {#update}

U kunt een specifiek programma bijwerken door een verzoek van PATCH aan het `/config/schedules` eindpunt te doen en identiteitskaart van het programma te verstrekken u probeert om in de verzoekweg bij te werken.

Met het verzoek PATCH kunt u de [status](#update-state) of het [bijsnijdschema](#update-schedule) voor een afzonderlijk schema bijwerken.

### Status schema bijwerken {#update-state}

U kunt een JSON-patchbewerking gebruiken om de status van de planning bij te werken. Als u de status wilt bijwerken, declareert u de `path` eigenschap als `/state` en stelt u de eigenschap in `value` op `active` of `inactive`. Lees de [JSON Patch](http://jsonpatch.com/) -documentatie voor meer informatie over JSON Patch.

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het programma dat u wilt bijwerken. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u de staat van het programma bijwerkt, moet u de waarde van aan &quot;/staat&quot;plaatsen `path` . |
| `value` | De bijgewerkte waarde van de staat van het programma. Deze waarde kan worden ingesteld op &quot;actief&quot; of &quot;inactief&quot; om het schema te activeren of deactiveren. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

### Uitsnijdschema bijwerken {#update-schedule}

U kunt een JSON-reparatiebewerking gebruiken om het uitsnijdschema bij te werken. Als u het schema wilt bijwerken, declareert u de `path` eigenschap als `/schedule` en stelt u de eigenschap in `value` op een geldig uitsnijdschema. Lees de [JSON Patch](http://jsonpatch.com/) -documentatie voor meer informatie over JSON Patch. Lees de documentatie over de indeling van de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie over de uitsnijdschema&#39;s.

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het programma dat u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt bijwerken. In dit geval moet u de waarde van `path` `/schedule`aan instellen, aangezien u het uitsnijdschema bijwerkt. |
| `value` | De bijgewerkte waarde van het uitsnijdschema. Deze waarde moet de vorm hebben van een uitsnijdschema. In dit voorbeeld, zal het programma op de tweede van elke maand lopen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Een specifiek schema verwijderen

U kunt verzoeken om een specifiek programma te schrappen door een verzoek van DELETE aan het `/config/schedules` eindpunt te doen en identiteitskaart van het programma te verstrekken u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het programma u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de programma&#39;s werken.