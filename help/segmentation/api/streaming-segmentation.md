---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsdienst;streamingsegmentatie;Streaming segmentatie;Continue evaluatie;
solution: Experience Platform
title: 'Evalueer Gebeurtenissen in Bijna Echt - tijd met het stromen Segmentatie '
topic: ontwikkelaarsgids
description: Dit document bevat voorbeelden over het gebruik van streamingsegmentatie met de Adobe Experience Platform Segmentation Service-API.
translation-type: tm+mt
source-git-commit: bb7edcaccca87918c56d00e092e4b7154d7c5d6e
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# Evalueer gebeurtenissen in bijna real time met het stromen segmentatie

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met de API. Voor informatie over het gebruiken van het stromen segmentatie die UI gebruikt, gelieve [het stromen segmentatie UI gids](../ui/streaming-segmentation.md) te lezen.

Door segmentering te streamen op [!DNL Adobe Experience Platform] kunnen klanten segmentering uitvoeren in bijna realtime en zich tegelijk richten op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien het stromen gegevens in [!DNL Platform] landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in [!DNL Platform] worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Streaming segmentatie kan alleen worden gebruikt om gegevens te evalueren die in het Platform worden gestreamd. Met andere woorden, gegevens die via batch-opname worden ingevoerd, worden niet geëvalueerd door streamingsegmentatie en worden samen met de nachtelijke geplande gesegmenteerde taak geëvalueerd.

## Aan de slag

Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Adobe Experience Platform] diensten betrokken bij het stromen segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd consumentenprofiel in echt - tijd, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Segmentation]](../home.md): Verstrekt de capaciteit om segmenten en publiek van uw  [!DNL Real-time Customer Profile] gegevens tot stand te brengen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Platform] APIs te maken.

### API-voorbeeldaanroepen lezen

Deze ontwikkelaarsgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Voor het invullen van specifieke aanvragen kunnen extra kopteksten nodig zijn. In elk voorbeeld in dit document worden de juiste kopteksten weergegeven. Gelieve speciale aandacht te besteden aan de steekproefverzoeken om ervoor te zorgen dat alle vereiste kopballen inbegrepen zijn.

### Streaming segmentatie ingeschakeld querytypen {#streaming-segmentation-query-types}

>[!NOTE]
>
>U zult geplande segmentatie voor de organisatie moeten toelaten opdat het stromen segmentatie werkt. Informatie over het toelaten van geplande segmentatie kan in [toelaat geplande segmenteringssectie](#enable-scheduled-segmentation) worden gevonden

Opdat een segment wordt geëvalueerd gebruikend het stromen segmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn.

| Type query | Details |
| ---------- | ------- |
| Binnenkomende hit | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. |
| Binnenkomende hit binnen relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis. |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |
| Binnenkomende hit die verwijst naar een profiel | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. |
| Binnenkomende hit die verwijst naar een profiel binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis en een of meer profielkenmerken. |
| Meerdere gebeurtenissen die naar een profiel verwijzen | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de laatste 24 uur** en (optioneel) heeft een of meer profielkenmerken. |

Een segmentdefinitie zal **not** voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).

Daarnaast zijn enkele richtlijnen van toepassing wanneer streamingsegmentatie wordt uitgevoerd:

| Type query | Richtsnoer |
| ---------- | -------- |
| Query voor één gebeurtenis | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugkijkvenster is beperkt tot **one dag**.</li><li>Er bestaat een strikte voorwaarde **must** voor de tijdvolgorde tussen de gebeurtenissen.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. De gehele gebeurtenis **kan echter geen** zijn als een negatie.</li></ul> |

## Hiermee worden alle segmenten opgehaald die zijn ingeschakeld voor streaming segmentatie

U kunt een lijst van al uw segmenten terugwinnen die voor het stromen segmentatie binnen uw IMS Organisatie door een verzoek van de GET aan het `/segment/definitions` eindpunt worden toegelaten.

**API-indeling**

Om streaming-toegelaten segmenten terug te winnen, moet u de vraagparameter `evaluationInfo.continuous.enabled=true` in de verzoekweg omvatten.

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

Een segment wordt automatisch voor streaming geschikt als het overeenkomt met een van de bovenstaande streaming segmentatietypen](#streaming-segmentation-query-types).[

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

>[!NOTE]
>
>Dit is een standaard &quot;creeer een segment&quot;verzoek. Lees voor meer informatie over het maken van een segmentdefinitie de zelfstudie over [het maken van een segment](../tutorials/create-a-segment.md).

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

## Geplande evaluatie {#enable-scheduled-segmentation} inschakelen

Zodra de het stromen evaluatie is toegelaten, moet een basislijn worden gecreeerd (waarna zal het segment altijd bijgewerkt zijn). De geplande evaluatie (die ook als geplande segmentatie wordt bekend) moet eerst worden toegelaten opdat het systeem baselining automatisch uitvoert. Met geplande segmentatie, kan uw IMS Org aan een terugkerend programma houden om uitvoerbanen automatisch in werking te stellen om segmenten te evalueren.

>[!NOTE]
>
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor [!DNL XDM Individual Profile] worden toegelaten. Als uw organisatie meer dan vijf samenvoegingsbeleid voor [!DNL XDM Individual Profile] binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

### Een schema maken

Door een verzoek van de POST aan het `/config/schedules` eindpunt te doen, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

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
| `properties.segments` | **(Vereist wanneer  `type` evenaart  `batch_segmentation`)** Het gebruiken  `["*"]` verzekert alle segmenten inbegrepen zijn. |
| `schedule` | **(Vereist)** Een tekenreeks die het taakschema bevat. Taken kunnen slechts eenmaal per dag worden uitgevoerd. Dit betekent dat u een taak niet meer dan één keer gedurende een periode van 24 uur kunt plannen. Het getoonde voorbeeld (`0 0 1 * * ?`) betekent de baan elke dag om 1:00:00 UTC wordt teweeggebracht. Raadpleeg de documentatie [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor meer informatie. |
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

Door gebrek, is een programma inactief wanneer gecreeerd tenzij het `state` bezit aan `active` in creeer (POST) verzoeklichaam wordt geplaatst. U kunt een programma toelaten (plaats `state` aan `active`) door een verzoek van PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg in te dienen.

**API-indeling**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Verzoek**

In het volgende verzoek wordt [JSON-patchopmaak](http://jsonpatch.com/) gebruikt om de `state` van het schema bij te werken naar `active`.

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

Nu u zowel nieuwe als bestaande segmenten voor het stromen segmentatie hebt toegelaten, en geplande segmentatie toegelaten om een basislijn te ontwikkelen en terugkomende evaluaties uit te voeren, kunt u beginnen streaming-toegelaten segmenten voor uw organisatie tot stand te brengen.

Als u wilt leren hoe u vergelijkbare acties kunt uitvoeren en met segmenten kunt werken via de Adobe Experience Platform-gebruikersinterface, gaat u naar de [gebruikersgids voor segmentBuilder](../ui/segment-builder.md).