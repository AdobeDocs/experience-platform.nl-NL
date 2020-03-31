---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming segmentering
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Evalueer gebeurtenissen in real time met het stromen segmentatie (Bèta)

>[!NOTE] Streaming segmentatie is een bètafunctie en is op verzoek beschikbaar.

Het stromen segmentatie (die ook als ononderbroken vraagevaluatie wordt bekend) is de capaciteit om een klant onmiddellijk te evalueren zodra een gebeurtenis in een bepaalde segmentgroep komt. Met deze mogelijkheid kunnen de meeste segmentregels nu worden geëvalueerd wanneer de gegevens worden doorgegeven aan het Adobe Experience Platform. Dit betekent dat segmentlidmaatschap up-to-date blijft zonder geplande segmentatietaken.

![](../images/api/streaming-segment-evaluation.png)

## Aan de slag

Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het streamen van segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Segmentatie](../home.md): Biedt de mogelijkheid om segmenten en publiek te maken op basis van uw gegevens in het realtime klantprofiel.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze ontwikkelaarsgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Voor het invullen van specifieke aanvragen kunnen extra kopteksten nodig zijn. In elk voorbeeld in dit document worden de juiste kopteksten weergegeven. Gelieve speciale aandacht te besteden aan de steekproefverzoeken om ervoor te zorgen dat alle vereiste kopballen inbegrepen zijn.

### Voor streaming segmentatie ingeschakelde querytypen

De volgende lijst maakt een lijst van de verschillende types van segmenteringsvragen en of zij het stromen segmentatie al dan niet steunen.

| Type query | Voorbeeldquery | Ondersteunde streamingsegmentatie |
| ---------- | ------------ | --------------------------------- |
| Eenvoudig demografisch | &quot;Geef me alle mensen van wie het huisadres in Canada is.&quot; | Ondersteund |
| Gebeurtenissen uit de tijdreeks | &quot;Geef mij alle personen die Lightroom hebben gedownload.&quot; | Ondersteund |
| Demografische en tijdreeksen | &quot;Geef me alle mensen die in Canada wonen en in de afgelopen 30 dagen een bestelling hebben geplaatst.&quot; | Ondersteund |
| Geen gebeurtenissen | &quot;Geef me alle mensen die twee aparte karretjes hebben verlaten binnen twee dagen na elkaar.&quot; | Ondersteund |
| Meerdere entiteiten | &quot;Geef me alle mensen van wie het machtigingstype &quot;ervaren&quot;is.&quot; | Niet ondersteund |
| Geavanceerde PQL-functies | &quot;Geef me alle profielen die een orde in de vorige week plaatsten, en omvat SKU en Naam voor alle gekochte producten.&quot; | Niet ondersteund |

## Hiermee worden alle segmenten opgehaald waarvoor segmentatie voor streaming is ingeschakeld

Voordat u een nieuw segment voor streaming maakt of een bestaand segment bijwerkt dat voor streaming is ingeschakeld, moet u ervoor zorgen dat u geen informatie dupliceert door een lijst met alle voor streaming ingeschakelde segmenten op te halen.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

Nadat u hebt bevestigd dat het segment dat u wilt maken, nog niet bestaat, kunt u een nieuw segment maken dat is ingeschakeld voor het streamen van segmentatie.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

Met het volgende verzoek wordt een nieuw segment gemaakt dat segmentatie streamt ingeschakeld. De `continuous` sectie is ingesteld op `enabled: true`.

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
    }
}'
```

>[!NOTE] Dit is een standaard &quot;creeer een segment&quot;verzoek, met de toegevoegde parameter van de `continuous` sectie die aan wordt geplaatst `enabled: true`. Voor meer informatie over het creëren van een segmentdefinitie, te lezen gelieve de documentatie over [segmentverwezenlijking](../tutorials/create-a-segment.md).

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

## Een bestaand segment voor streamingsegmentatie inschakelen

U kunt een bestaand segment voor het stromen segmentatie toelaten door identiteitskaart van de segmentdefinitie in de weg van een verzoek van de PATCH te verstrekken. Bovendien moet de nuttige lading van dit PATCH verzoek de volledige details van de bestaande segmentdefinitie omvatten, die kan worden betreden door een GET verzoek aan de segmentdefinitie in kwestie te doen.

### Een bestaande segmentdefinitie opzoeken

Om omhoog een bestaande segmentdefinitie te kijken, moet u zijn identiteitskaart in de weg van een GET verzoek leveren.

**API-indeling**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | De id van de segmentdefinitie die u wilt opzoeken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie zal details van de segmentdefinitie terugkeren u vroeg.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Voor het volgende verzoek, zult u de volledige details van de segmentdefinitie nodig hebben die in deze reactie zijn teruggekeerd. Kopieer de details van dit antwoord die in de tekst van het volgende verzoek moeten worden gebruikt.

### Het bestaande segment voor streamingsegmentatie inschakelen

Nu u de details van het segment kent u wilt bijwerken, kunt u een verzoek van de PATCH uitvoeren om het segment bij te werken om het stromen segmentatie toe te laten.

**API-indeling**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Verzoek**

De nuttige lading van het volgende verzoek verstrekt de details van de segmentdefinitie (die in de [vorige stap](#look-up-an-existing-segment-definition)wordt verkregen), en werkt het bij door zijn `continuous.enabled` bezit in te veranderen `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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
    }
}'
```

**Antwoord**

Een succesvolle reactie keert de details van de onlangs bijgewerkte segmentdefinitie terug.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Geplande evaluatie inschakelen

Zodra de het stromen evaluatie is toegelaten, moet een basislijn worden gecreeerd (waarna zal het segment altijd bijgewerkt zijn). Dit wordt automatisch gedaan door het systeem, nochtans moet de geplande evaluatie (die ook als geplande segmentatie wordt bekend) eerst worden toegelaten opdat baselining plaatsvindt.

Met geplande segmentatie, kan uw IMS Org een terugkerend programma tot stand brengen om de uitvoerbanen automatisch in werking te stellen om segmenten te evalueren.

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

Als u wilt weten hoe u vergelijkbare acties uitvoert en met segmenten werkt via de gebruikersinterface van het Adobe Experience Platform, raadpleegt u de gebruikershandleiding [van](../ui/overview.md)Segment Builder.