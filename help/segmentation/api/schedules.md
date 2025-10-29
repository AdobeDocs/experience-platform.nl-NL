---
solution: Experience Platform
title: API-eindpunt voor planningen
description: Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---

# Planningeindpunt

Planningen zijn een hulpmiddel dat kan worden gebruikt om batch-segmentatietaken één keer per dag automatisch uit te voeren. U kunt het `/config/schedules` eindpunt gebruiken om een lijst van programma&#39;s terug te winnen, een nieuw programma tot stand te brengen, details van een specifiek programma terug te winnen, een specifiek programma bij te werken, of een specifiek programma te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met schema&#39;s ophalen {#retrieve-list}

U kunt een lijst van alle programma&#39;s voor uw organisatie terugwinnen door een GET- verzoek aan het `/config/schedules` eindpunt te doen.

**API formaat**

Het `/config/schedules` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle programma&#39;s beschikbaar voor uw organisatie terugwinnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**de parameters van de Vraag**

+++ Een lijst met beschikbare queryparameters.

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `start` | Geeft aan vanaf welke pagina de verschuiving begint. Deze waarde is standaard 0. | `start=5` |
| `limit` | Geeft het aantal geretourneerde schema&#39;s op. Deze waarde is standaard 100. | `limit=20` |

+++

**Verzoek**

Het volgende verzoek zal de laatste tien programma&#39;s terugwinnen die binnen uw organisatie worden gepost.

+++ Een steekproefverzoek om een lijst van programma&#39;s terug te winnen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van programma&#39;s voor de gespecificeerde organisatie als JSON terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor ruimte, en toont slechts het eerste teruggekeerde programma.

+++ Een voorbeeldreactie bij het ophalen van een lijst met schema&#39;s.

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
| `children.properties.segments` | Als u `["*"]` gebruikt, worden alle segmenten opgenomen. |
| `children.schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Voor meer informatie over kroonprogramma&#39;s, te lezen gelieve het bijlage op het [ formaat van de cron uitdrukking ](#appendix). In dit voorbeeld, &quot;`0 0 1 * *`&quot;betekent dat dit programma bij 1AM elke dag zal lopen. |
| `children.state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

+++

## Een nieuw schema maken {#create}

U kunt een nieuw schema tot stand brengen door een POST- verzoek aan het `/config/schedules` eindpunt te doen.

**API formaat**

```http
POST /config/schedules
```

**Verzoek**

+++ Een voorbeeldverzoek om een programma te maken. 

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
| `properties` | **Vereist.** Een object dat aanvullende eigenschappen bevat die gerelateerd zijn aan het schema. |
| `properties.segments` | **vereist wanneer `type` &quot;batch_segmentation&quot;evenaart.** Met `["*"]` zorgt u ervoor dat alle segmenten worden opgenomen. |
| `schedule` | *Facultatief.* Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Voor meer informatie over kroonprogramma&#39;s, te lezen gelieve het bijlage op het [ formaat van de cron uitdrukking ](#appendix). In dit voorbeeld, &quot;`0 0 1 * *`&quot;betekent dat dit programma bij 1AM elke dag zal lopen. <br><br> als dit koord niet wordt geleverd, zal een systeem-geproduceerd programma automatisch worden geproduceerd. |
| `state` | *Facultatief.* Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn &quot;actief&quot; en &quot;inactief&quot;. De status wordt standaard ingesteld op &quot;inactief&quot;. |

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerd programma terug.

+++ Een voorbeeldreactie bij het maken van een schema.

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

+++

## Een specifiek schema ophalen {#get}

U kunt gedetailleerde informatie over een specifiek programma terugwinnen door een GET- verzoek aan het `/config/schedules` eindpunt te doen en identiteitskaart van het programma te verstrekken u in de verzoekweg wenst terug te winnen.

**API formaat**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het programma u wilt terugwinnen. |

**Verzoek**

+++ Een steekproefverzoek om een programma terug te winnen. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over het gespecificeerde programma terug.

+++ Een voorbeeldreactie bij het ophalen van een schema.

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
| `type` | Het type taak als tekenreeks. De twee ondersteunde typen zijn `batch_segmentation` en `export` . |
| `properties` | Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `properties.segments` | Als u `["*"]` gebruikt, worden alle segmenten opgenomen. |
| `schedule` | Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Voor meer informatie over kroonprogramma&#39;s, te lezen gelieve het bijlage op het [ formaat van de cron uitdrukking ](#appendix). In dit voorbeeld, &quot;`0 0 1 * *`&quot;betekent dat dit programma bij 1AM elke dag zal lopen. |
| `state` | Een tekenreeks die de staat van het schema bevat. De twee ondersteunde statussen zijn `active` en `inactive` . De status wordt standaard ingesteld op `inactive` . |

+++

## Details bijwerken voor een specifiek schema {#update}

U kunt een specifiek programma bijwerken door een PATCH-aanvraag in te dienen bij het `/config/schedules` -eindpunt en de id op te geven van het schema dat u probeert bij te werken in het aanvraagpad.

Het verzoek van PATCH staat u toe om of de [ staat ](#update-state) of het [ bouwplan ](#update-schedule) voor een individueel programma bij te werken.

**API formaat**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` waarde van het schema u wilt bijwerken. |

>[!BEGINTABS]

>[!TAB  de planningsstaat van de Update ]

U kunt een JSON-patchbewerking gebruiken om de status van de planning bij te werken. Als u de status wilt bijwerken, declareert u de eigenschap `path` als `/state` en stelt u de eigenschap `value` in op `active` of `inactive` . Voor meer informatie over Reparatie JSON, te lezen gelieve de [ documentatie van het Reparatie 0} JSON {.](https://datatracker.ietf.org/doc/html/rfc6902)

**Verzoek**

+++ Een voorbeeldverzoek om de planningsstatus bij te werken.

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

+++

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt repareren. In dit geval moet u, aangezien u de status van het programma bijwerkt, de waarde van `path` instellen op &quot;/state&quot;. |
| `value` | De bijgewerkte waarde van de staat van het programma. Deze waarde kan worden ingesteld op &quot;actief&quot; of &quot;inactief&quot; om het schema te activeren of deactiveren. Gelieve te merken op dat u **niet** een programma kan onbruikbaar maken als de organisatie voor het stromen is toegelaten. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

>[!TAB  Update bouwt programma ]

U kunt een JSON-reparatiebewerking gebruiken om het uitsnijdschema bij te werken. Als u het schema wilt bijwerken, declareert u de eigenschap `path` als `/schedule` en stelt u de eigenschap `value` in op een geldig uitsnijdschema. Voor meer informatie over Reparatie JSON, te lezen gelieve de [ documentatie van het Reparatie 0} JSON {. ](https://datatracker.ietf.org/doc/html/rfc6902) Voor meer informatie over kroonprogramma&#39;s, te lezen gelieve het bijlage op het [ formaat van de cron uitdrukking ](#appendix).

>[!ENDTABS]

**Verzoek**

+++ Een voorbeeldverzoek om het schema bij te werken.

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
        "value":"0 0 2 * * ?"
    }
]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `path` | Het pad van de waarde die u wilt bijwerken. In dit geval moet u, aangezien u het bijsnijdschema bijwerkt, de waarde van `path` instellen op `/schedule` . |
| `value` | De bijgewerkte waarde van het uitsnijdschema. Deze waarde moet de vorm hebben van een uitsnijdschema. In dit voorbeeld, zal het programma op de tweede van elke maand lopen. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Een specifiek schema verwijderen

U kunt verzoeken om een specifiek programma te schrappen door een DELETE- verzoek aan het `/config/schedules` eindpunt te doen en identiteitskaart van het programma te verstrekken u wenst om in de verzoekweg te schrappen.

**API formaat**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SCHEDULE_ID}` | De `id` -waarde van het schema dat u wilt verwijderen. |

**Verzoek**

+++ Een voorbeeldverzoek om een schema te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud).

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe de programma&#39;s werken.

## Bijlage {#appendix}

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
| Maand | Ja | 1-12, JAN-DEC | `, - * /` |
| Dag van de week | Ja | 1-7, SUN-SAT | `, - * ? / L #` |
| Jaar | Nee | Leeg, 1970-2099 | `, - * /` |

>[!NOTE]
>
>De namen van de maanden en de namen van de dagen van de week zijn **niet** gevoelig geval. Daarom is `SUN` gelijk aan het gebruik van `sun` .

De speciale tekens die zijn toegestaan, vertegenwoordigen de volgende betekenissen:

| Speciaal teken | Beschrijving |
| ----------------- | ----------- |
| `*` | Deze waarde wordt gebruikt om **alle** waarden op een gebied te selecteren. Bijvoorbeeld, zou het zetten van `*` op het urengebied **elk** uur betekenen. |
| `?` | Deze waarde betekent dat er geen specifieke waarde is vereist. Dit wordt doorgaans gebruikt om iets op te geven in het ene veld waar het teken is toegestaan, maar niet in het andere veld. Als u bijvoorbeeld wilt dat een gebeurtenis elke drie maanden wordt geactiveerd, maar niet om de dag van de week gaat, plaatst u `3` in het veld Dag van de maand en `?` in het veld Dag van de week. |
| `-` | Deze waarde wordt gebruikt om **inclusieve** waaiers voor het gebied te specificeren. Als u bijvoorbeeld `9-15` in het veld Uren plaatst, betekent dit dat de uren 9, 10, 11, 12, 13, 14 en 15 bevatten. |
| `,` | Deze waarde wordt gebruikt om extra waarden op te geven. Als u bijvoorbeeld `MON, FRI, SAT` op de dag van het weekveld plaatst, betekent dit dat de dagen van de week maandag, vrijdag en zaterdag bevatten. |
| `/` | Deze waarde wordt gebruikt om toenamen op te geven. De waarde die vóór de `/` wordt geplaatst, bepaalt waar deze wordt verhoogd, terwijl de waarde die na de `/` wordt geplaatst, bepaalt in hoeverre de waarde wordt verhoogd. Als u bijvoorbeeld `1/7` in het minutenveld plaatst, betekent dit dat de minuten 1, 8, 15, 22, 29, 36, 43, 50 en 57 bevatten. |
| `L` | Deze waarde wordt gebruikt om `Last` op te geven en heeft een andere betekenis, afhankelijk van het veld waarin deze wordt gebruikt. Als het met de dag van het maandgebied wordt gebruikt, vertegenwoordigt het de laatste dag van de maand. Als het met de dag van het weekgebied door zich wordt gebruikt, vertegenwoordigt het de laatste dag van de week, die Zaterdag (`SAT`) is. Als het samen met de dag van het weekgebied, samen met een andere waarde wordt gebruikt, vertegenwoordigt het de laatste dag van dat type voor de maand. Bijvoorbeeld, als u `5L` op de dag van het weekgebied zet, zou het **slechts** de laatste Vrijdag van de maand omvatten. |
| `W` | Deze waarde wordt gebruikt om de dichtste weekdag aan de bepaalde dag te specificeren. Als u bijvoorbeeld `18W` op de dag van het maandveld plaatst en de 18e van die maand op een zaterdag, wordt deze op vrijdag 17e geactiveerd, de dichtstbijzijnde weekdag. Als de 18e van die maand een zondag was, zou het op maandag 19de, die dichtstbijzijnde weekdag is, in werking treden. Gelieve te merken op dat als u `1W` op de dag van het maandgebied zet, en de dichtstbijzijnde weekdag in de vorige maand zou zijn, de gebeurtenis nog op de dichtstbijzijnde weekdag van de **huidige** maand zal teweegbrengen.</br></br> Bovendien, kunt u `L` en `W` combineren om `LW` te maken, die de laatste weekdag van de maand zou specificeren. |
| `#` | Deze waarde wordt gebruikt om de negende dag van de week in een maand te specificeren. De waarde die vóór `#` wordt geplaatst, vertegenwoordigt de dag van de week, terwijl de waarde die na `#` wordt geplaatst, aangeeft welk exemplaar in de maand waarin het zich bevindt. Als u bijvoorbeeld `1#3` plaatst, wordt de gebeurtenis geactiveerd op de derde zondag van de maand. Gelieve te merken op dat als u `X#5` plaatst en er geen vijfde voorkomen van die dag van de week in die maand is, de gebeurtenis **niet** zal teweeggebracht worden. Bijvoorbeeld, als u `1#5` zet, en er geen vijfde Zondag in die maand is, zal de gebeurtenis **niet** worden teweeggebracht. |

### Voorbeelden

In de volgende tabel ziet u voorbeelden van tekenreeksen voor snijexpressie en geeft u een uitleg van wat deze betekenen.

| Uitdrukking | Toelichting |
| ---------- | ----------- |
| `0 0 13 * * ?` | Het evenement gaat elke dag om 13.00 uur branden. |
| `0 30 9 * * ? 2022` | De gebeurtenis zal elke dag om 9 :30AM in het jaar 2022 branden. |
| `0 * 18 * * ?` | De gebeurtenis zal elke minuut in brand steken, beginnend bij 6 PM en eindigend bij 6 :59PM, elke dag. |
| `0 0/10 17 * * ?` | De gebeurtenis wordt elke 10 minuten gestart, van 17.00 tot 18.00 uur, elke dag. |
| `0 13,38 5 ? 6 WED` | Het evenement gaat elke woensdag om 5 :13AM en 5 :38AM branden. |
| `0 30 12 ? * 4#3` | De gebeurtenis zal om 12 :30PM op de derde Woensdag elke maand branden. |
| `0 30 12 ? * 6L` | De gebeurtenis zal om 12 :30PM op de laatste Vrijdag van elke maand in brand steken. |
| `0 45 11 ? * MON-THU` | De gebeurtenis zal om 11 :45AM elke maandag, Dinsdag, Woensdag, en Donderdag branden. |