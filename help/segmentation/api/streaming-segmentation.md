---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming segmentering
topic: developer guide
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# Evalueer gebeurtenissen in bijna real time met het stromen segmentatie

Streaming segmentering op [!DNL Adobe Experience Platform] staat klanten toe om segmentatie in bijna real time te doen terwijl het concentreren op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in landen [!DNL Platform], die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens worden overgegaan in [!DNL Platform], betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.

![](../images/api/streaming-segment-evaluation.png)

## Aan de slag

Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Adobe Experience Platform] diensten betrokken bij het stromen segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [!DNL Real-time Customer Profile](../../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [!DNL Segmentation](../home.md): Verstrekt de capaciteit om segmenten en publiek van uw [!DNL Real-time Customer Profile] gegevens tot stand te brengen.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan APIs te maken. [!DNL Platform]

### API-voorbeeldaanroepen lezen

Deze ontwikkelaarsgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Voor het invullen van specifieke aanvragen kunnen extra kopteksten nodig zijn. In elk voorbeeld in dit document worden de juiste kopteksten weergegeven. Gelieve speciale aandacht te besteden aan de steekproefverzoeken om ervoor te zorgen dat alle vereiste kopballen inbegrepen zijn.

### Voor streaming segmentatie ingeschakelde querytypen {#streaming-segmentation-query-types}

>[!NOTE] U zult geplande segmentatie voor de organisatie moeten toelaten opdat het stromen segmentatie werkt. Informatie over het toelaten van geplande segmentatie kan in [toelaat geplande segmenteringssectie worden gevonden](#enable-scheduled-segmentation)

Opdat een segment wordt geëvalueerd gebruikend het stromen segmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn.

| Type query | Details |
| ---------- | ------- |
| Binnenkomende hit | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. |
| Binnenkomende hit binnen relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis **in de laatste zeven dagen**. |
| Binnenkomende hit die verwijst naar een profiel | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. |
| Binnenkomende hit die verwijst naar een profiel binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis en een of meer profielkenmerken, **binnen de afgelopen zeven dagen**. |
| Meerdere gebeurtenissen die naar een profiel verwijzen | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de afgelopen 24 uur** en (optioneel), heeft een of meer profielkenmerken. |

In de volgende sectie worden voorbeelden van segmentdefinities weergegeven die **niet** zijn ingeschakeld voor streamingsegmentatie.

| Type query | Details |
| ---------- | ------- | 
| Binnenkomende hit binnen relatief tijdvenster | Als de segmentdefinitie naar een inkomende gebeurtenis verwijst die **niet** binnen de **laatste zeven-dagperiode** valt. Bijvoorbeeld binnen de **laatste twee weken**. |
| Binnenkomende hit die verwijst naar een profiel binnen een relatief venster | De volgende opties bieden **geen** ondersteuning voor streamingsegmentatie:<ul><li>Een binnenkomende gebeurtenis **die zich niet** binnen de **laatste periode** van zeven dagen bevindt.</li><li>Een segmentdefinitie die Adobe Audience Manager (AAM) segmenten of eigenschappen omvat.</li></ul> |
| Meerdere gebeurtenissen die naar een profiel verwijzen | De volgende opties bieden **geen** ondersteuning voor streamingsegmentatie:<ul><li>Een gebeurtenis die **niet** optreedt binnen **de laatste 24 uur**.</li><li>Een segmentdefinitie die Adobe Audience Manager (AAM) segmenten of eigenschappen omvat.</li></ul> |
| Vragen over meerdere entiteiten | Vraagstukken met meerdere entiteiten worden over het geheel genomen **niet** ondersteund door streamingsegmentatie. |

Daarnaast zijn enkele richtlijnen van toepassing wanneer streamingsegmentatie wordt uitgevoerd:

| Type query | Richtsnoer |
| ---------- | -------- |
| Query voor één gebeurtenis | Het terugkijkvenster is beperkt tot **zeven dagen**. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugkijkvenster is beperkt tot **één dag**.</li><li>Tussen de gebeurtenissen **moet** een strikte voorwaarde voor de tijdvolgorde bestaan.</li><li>Slechts worden de eenvoudige tijdorden (vóór en na) tussen de gebeurtenissen toegestaan.</li><li>De afzonderlijke gebeurtenissen **kunnen niet** worden genegeerd. De gehele query **kan** echter worden genegeerd.</li></ul> |

## Hiermee worden alle segmenten opgehaald die zijn ingeschakeld voor streamingsegmentatie

U kunt een lijst van al uw segmenten terugwinnen die voor het stromen segmentatie binnen uw IMS Organisatie door een GET verzoek aan het `/segment/definitions` eindpunt te maken worden toegelaten.

**API-indeling**

Als u streaming-ingeschakelde segmenten wilt ophalen, moet u de queryparameter opnemen `evaluationInfo.continuous.enabled=true` in het aanvraagpad.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een serie van segmenten in uw IMS Organisatie terug die voor het stromen segmentatie worden toegelaten.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Een segment met streaming mogelijkheden maken

Een segment wordt automatisch voor streaming ingeschakeld als het overeenkomt met een van de bovenstaande [](#streaming-segmentation-query-types)streaming segmentatietypen.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE] Dit is een standaard &quot;creeer een segment&quot;verzoek. Lees voor meer informatie over het maken van een segmentdefinitie de zelfstudie over het [maken van een segment](../tutorials/create-a-segment.md).

**Antwoord**

Een succesvolle reactie keert de details van de nieuw gecreeerd streaming-toegelaten segmentdefinitie terug.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Geplande evaluatie inschakelen {#enable-scheduled-segmentation}

Zodra de het stromen evaluatie is toegelaten, moet een basislijn worden gecreeerd (waarna zal het segment altijd bijgewerkt zijn). De geplande evaluatie (die ook als geplande segmentatie wordt bekend) moet eerst worden toegelaten opdat het systeem baselining automatisch uitvoert. Met geplande segmentatie, kan uw IMS Org aan een terugkerend programma houden om uitvoerbanen automatisch in werking te stellen om segmenten te evalueren.

>[!NOTE] De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor Individueel Profiel XDM worden toegelaten. Als uw organisatie meer dan vijf samenvoegingsbeleid voor Individueel Profiel XDM binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

### Een schema maken

Door een POST- verzoek aan het `/config/schedules` eindpunt te doen, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

**API-indeling**

```http
POST /config/schedules
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw programma dat op de specificaties in de lading wordt gebaseerd.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | **(Vereist)** De naam van het schema. Moet een tekenreeks zijn. |
| `type` | **(Vereist)** Het taaktype in tekenreeksindeling. De ondersteunde typen zijn `batch_segmentation` en `export`. |
| `properties` | **(Vereist)** Een object dat aanvullende eigenschappen bevat die betrekking hebben op het schema. |
| `properties.segments` | **(Vereist wanneer`type`evenaart`batch_segmentation`)** Door te gebruiken worden alle segmenten `["*"]` opgenomen. |
| `schedule` | **(Vereist)** Een tekenreeks die het taakschema bevat. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. In het voorbeeld (`0 0 1 * * ?`) wordt aangegeven dat de taak elke dag om 1:00:00 UTC wordt geactiveerd. Raadpleeg de documentatie bij de indeling [van de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) uitsnijdexpressie voor meer informatie. |
| `state` | *(Optioneel)* Tekenreeks die de staat van het schema bevat. Beschikbare waarden: `active` en `inactive`. De standaardwaarde is `inactive`. Een IMS-organisatie kan slechts één schema maken. De stappen voor het bijwerken van het programma zijn beschikbaar later in dit leerprogramma. |

**Antwoord**

Een succesvolle reactie keert de details van het onlangs gecreeerde programma terug.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Een schema inschakelen

Door gebrek, is een programma inactief wanneer gecreeerd tenzij het `state` bezit aan `active` in creeer (POST) verzoeklichaam wordt geplaatst. U kunt een programma toelaten (reeks `state` aan `active`) door een verzoek van de PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg te doen.

**API-indeling**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Verzoek**

In het volgende verzoek wordt de opmaak [van](http://jsonpatch.com/) JSON-patch gebruikt om de planning bij te werken `state` naar `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Antwoord**

Een geslaagde update retourneert een lege reactiehoofdtekst en HTTP Status 204 (Geen inhoud).

Dezelfde bewerking kan worden gebruikt om een schema uit te schakelen door de waarde in het vorige verzoek te vervangen door &quot;inactief&quot;.

## Volgende stappen

Nu u zowel nieuwe als bestaande segmenten voor het stromen segmentatie hebt toegelaten, en geplande segmentatie om een basislijn te ontwikkelen en terugkomende evaluaties uit te voeren toegelaten, kunt u beginnen om segmenten voor uw organisatie tot stand te brengen.

Leer hoe te om gelijkaardige acties uit te voeren en met segmenten te werken gebruikend het gebruikersinterface van het Adobe Experience Platform, gelieve de gebruikersgids [van de Bouwer van het](../ui/overview.md)Segment te bezoeken.