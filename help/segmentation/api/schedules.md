---
keywords: Experience Platform;huis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsdienst;planningen;programma;api;API;
solution: Experience Platform
title: API-eindpunt voor planningen
topic-legacy: developer guide
description: Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 84026b447eea00955bc9e6482b81ae1aad3c312e
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# Planningeindpunt

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt de `/config/schedules` eindpunt om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met schema&#39;s ophalen {#retrieve-list}

U kunt een lijst van alle programma&#39;s voor uw organisatie terugwinnen door een verzoek van de GET tot de `/config/schedules` eindpunt.

**API-indeling**

De `/config/schedules` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle programma&#39;s beschikbaar voor uw organisatie terugwinnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

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

Het volgende verzoek zal de laatste tien programma&#39;s terugwinnen die binnen uw organisatie worden gepost.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
| `children.properties.segments` | Gebruiken `["*"]` zorgt ervoor dat alle segmenten worden opgenomen. |
| `children.schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Lees voor meer informatie over de cron-schema&#39;s de bijlage bij de [expressie-indeling voor uitsnijden](#appendix). In dit voorbeeld betekent &quot;0 0 1 * *&quot;dat dit programma om 1AM elke dag zal lopen. |
| `children.state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

## Een nieuw schema maken {#create}

U kunt een nieuw programma tot stand brengen door een verzoek van de POST aan `/config/schedules` eindpunt.

**API-indeling**

```http
POST /config/schedules
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `properties.segments` | **Vereist wanneer `type` is gelijk aan &quot;batch_segmentation&quot;.** Gebruiken `["*"]` zorgt ervoor dat alle segmenten worden opgenomen. |
| `schedule` | *Optioneel.* Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Lees voor meer informatie over de cron-schema&#39;s de bijlage bij de [expressie-indeling voor uitsnijden](#appendix). In dit voorbeeld betekent &quot;0 0 1 * *&quot;dat dit programma om 1AM elke dag zal lopen. <br><br>Als deze tekenreeks niet wordt opgegeven, wordt automatisch een door het systeem gegenereerd schema gegenereerd. |
| `state` | *Optioneel.* Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerd programma terug.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

U kunt gedetailleerde informatie over een specifiek programma terugwinnen door een verzoek van de GET aan `/config/schedules` eindpunt en het verstrekken van identiteitskaart van het programma u wenst om in de verzoekweg terug te winnen.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over het gespecificeerde programma terug.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `properties.segments` | Gebruiken `["*"]` zorgt ervoor dat alle segmenten worden opgenomen. |
| `schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Lees voor meer informatie over de cron-schema&#39;s de bijlage bij de [expressie-indeling voor uitsnijden](#appendix). In dit voorbeeld betekent &quot;0 0 1 * *&quot;dat dit programma om 1AM elke dag zal lopen. |
| `state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn `active` en `inactive`. De status is standaard ingesteld op `inactive`. |

## Details bijwerken voor een specifiek schema {#update}

U kunt een specifieke planning bijwerken door een PATCH-verzoek in te dienen bij de `/config/schedules` en het verstrekken van identiteitskaart van het programma u probeert om in de verzoekweg bij te werken.

Met de PATCH-aanvraag kunt u een van de [state](#update-state) of de [uitsnijdschema](#update-schedule) voor een afzonderlijk schema.

### Status schema bijwerken {#update-state}

U kunt een JSON-patchbewerking gebruiken om de status van de planning bij te werken. Als u de status wilt bijwerken, declareert u de `path` eigenschap as `/state` en stelt de `value` hetzij `active` of `inactive`. Lees voor meer informatie over JSON Patch de [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) documentatie.

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het schema u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Het pad van de waarde die u wilt repareren. In dit geval, aangezien u de staat van het programma bijwerkt, moet u de waarde van plaatsen `path` naar &quot;/state&quot;. |
| `value` | De bijgewerkte waarde van de staat van het programma. Deze waarde kan worden ingesteld op &quot;actief&quot; of &quot;inactief&quot; om het schema te activeren of deactiveren. Houd er rekening mee dat u **kan** Schakel een schema uit als de IMS-organisatie is ingeschakeld voor streaming. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

### Uitsnijdschema bijwerken {#update-schedule}

U kunt een JSON-reparatiebewerking gebruiken om het uitsnijdschema bij te werken. Om het programma bij te werken, verklaart u het `path` eigenschap as `/schedule` en stelt de `value` naar een geldig uitsnijdschema. Lees voor meer informatie over JSON Patch de [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) documentatie. Lees voor meer informatie over de cron-schema&#39;s de bijlage bij de [expressie-indeling voor uitsnijden](#appendix).

**API-indeling**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het schema u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Het pad van de waarde die u wilt bijwerken. In dit geval moet u, aangezien u het bijsnijdschema bijwerkt, de waarde instellen van `path` tot `/schedule`. |
| `value` | De bijgewerkte waarde van het uitsnijdschema. Deze waarde moet de vorm hebben van een uitsnijdschema. In dit voorbeeld, zal het programma op de tweede van elke maand lopen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Een specifiek schema verwijderen

U kunt verzoeken om een specifiek programma te schrappen door een verzoek van DELETE aan te richten `/config/schedules` eindpunt en het verstrekken van identiteitskaart van het programma u wenst om in de verzoekweg te schrappen.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de programma&#39;s werken.

## Aanhangsel {#appendix}

In de volgende bijlage wordt de notatie van de expressie van een uitsnede beschreven die in de planningen wordt gebruikt.

### Indeling

Een uitsnijdexpressie is een tekenreeks die bestaat uit 6 of 7 velden. De expressie ziet er ongeveer als volgt uit:

`0 0 12 * * ?`

In een expressie-tekenreeks voor een bijsnijden vertegenwoordigt het eerste veld de seconden, het tweede veld de minuten, het derde veld de uren, het vierde veld de dag van de maand, het vijfde veld de maand en het zesde veld de dag van de week. U kunt desgewenst ook een zevende veld opnemen, dat het jaar vertegenwoordigt.

| Veldnaam | Vereist | Mogelijke waarden | Speciale tekens toegestaan |
| ---------- | -------- | --------------- | -------------------------- |
| Seconden | Ja | 0-59 | `, - * /` |
| Minuten | Ja | 0-59 | `, - * /` |
| Uren | Ja | 0-23 | `, - * /` |
| Dag van de maand | Ja | 1-31 | `, - * ? / L W` |
| Month | Ja | 1-12, JAN-DEC | `, - * /` |
| Dag van de week | Ja | 1-7, SUN-SAT | `, - * ? / L #` |
| Year | Nee | Leeg, 1970-2099 | `, - * /` |

>[!NOTE]
>
>De namen van de maanden en de dagen van de week zijn **niet** hoofdlettergevoelig. Daarom `SUN` is gelijk aan `sun`.

De speciale tekens die zijn toegestaan, vertegenwoordigen de volgende betekenissen:

| Speciaal teken | Beschrijving |
| ----------------- | ----------- |
| `*` | Deze waarde wordt gebruikt om **alles** waarden in een veld. Bijvoorbeeld, plaatsen `*` in de uren **elke** uur. |
| `?` | Deze waarde betekent dat er geen specifieke waarde is vereist. Dit wordt doorgaans gebruikt om iets op te geven in het ene veld waar het teken is toegestaan, maar niet in het andere veld. Bijvoorbeeld, als u een gebeurtenis wilt teweegbrengen elke 3de van de maand, maar niet om geeft over welke dag van de week het is, zou u zetten `3` in het veld dag van de maand en `?` op de dag van de week. |
| `-` | Deze waarde wordt gebruikt om op te geven **inclusief** bereiken voor het veld. Als u bijvoorbeeld `9-15` in het veld Uren betekent dit dat de uren 9 , 10 , 11 , 12 , 13 , 14 en 15 moeten omvatten . |
| `,` | Deze waarde wordt gebruikt om extra waarden op te geven. Als u bijvoorbeeld `MON, FRI, SAT` op de dag van het weekgebied, zou dit betekenen de dagen van de week maandag, vrijdag, en Zaterdag omvatten. |
| `/` | Deze waarde wordt gebruikt om toenamen op te geven. De waarde die voor de `/` bepaalt waar het van stijgt, terwijl de waarde na wordt geplaatst `/` bepaalt hoeveel het met stijgt. Als u bijvoorbeeld `1/7` in het minutenveld betekent dit dat de notulen 1 , 8 , 15 , 22 , 29 , 36 , 43 , 50 en 57 bevatten . |
| `L` | Deze waarde wordt gebruikt om op te geven `Last`en heeft een andere betekenis, afhankelijk van het veld waarin deze wordt gebruikt. Als het met de dag van het maandgebied wordt gebruikt, vertegenwoordigt het de laatste dag van de maand. Als het op zich met de dag van het weekgebied wordt gebruikt, vertegenwoordigt het de laatste dag van de week, die Zaterdag (`SAT`). Als het samen met de dag van het weekgebied, samen met een andere waarde wordt gebruikt, vertegenwoordigt het de laatste dag van dat type voor de maand. Als u bijvoorbeeld `5L` op de dag van de week zou het **alleen** de laatste vrijdag van de maand. |
| `W` | Deze waarde wordt gebruikt om de dichtste weekdag aan de bepaalde dag te specificeren. Als u bijvoorbeeld `18W` op de dag van het maandveld, en de 18e van die maand was een zaterdag, zou het op vrijdag 17e, de dichtstbijzijnde weekdag, in werking treden. Als de 18e van die maand een zondag was, zou het op maandag 19de, die dichtstbijzijnde weekdag is, in werking treden. Houd er rekening mee dat als u `1W` in de dag van het maandveld, en de dichtstbijzijnde weekdag in de voorafgaande maand, wordt de gebeurtenis nog steeds geactiveerd op de dichtstbijzijnde weekdag van de maand **huidig** maand.</br></br>Bovendien kunt u `L` en `W` om `LW`, waarin de laatste weekdag van de maand wordt vermeld. |
| `#` | Deze waarde wordt gebruikt om de negende dag van de week in een maand te specificeren. De waarde die voor de `#` staat voor de dag van de week, terwijl de waarde na de `#` geeft aan welk exemplaar in de maand dit is. Als u bijvoorbeeld `1#3`, wordt de gebeurtenis op de derde zondag van de maand gestart. Houd er rekening mee dat als u `X#5` en er is geen vijfde van die dag van de week in die maand, zal het evenement **niet** worden geactiveerd. Als u bijvoorbeeld `1#5`en er is geen vijfde zondag in die maand, zal het evenement **niet** worden geactiveerd. |

### Voorbeelden

In de volgende tabel ziet u voorbeelden van tekenreeksen voor snijexpressie en geeft u een uitleg van wat deze betekenen.

| Uitdrukking | Toelichting |
| ---------- | ----------- |
| `0 0 13 * * ?` | Het evenement gaat elke dag om 13.00 uur branden. |
| `0 30 9 * * ? 2022` | Het evenement zal elke dag om 9.30 uur in 2022 plaatsvinden. |
| `0 * 18 * * ?` | De gebeurtenis wordt elke minuut gestart, te beginnen om 18.00 uur en te eindigen om 18.59 uur, elke dag. |
| `0 0/10 17 * * ?` | De gebeurtenis wordt elke 10 minuten gestart, van 17.00 tot 18.00 uur, elke dag. |
| `0 13,38 5 ? 6 WED` | Het evenement gaat elke woensdag om 5.13 en om 5.38 uur van start. |
| `0 30 12 ? * 4#3` | Het evenement gaat elke maand om 12:30 uur branden op de derde woensdag. |
| `0 30 12 ? * 6L` | De gebeurtenis wordt elke maand om 12:30 uur om de laatste vrijdag afgespeeld. |
| `0 45 11 ? * MON-THU` | Het evenement gaat elke maandag, dinsdag, woensdag en donderdag om 11.45 uur branden. |