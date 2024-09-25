---
solution: Experience Platform
title: Evalueer Gebeurtenissen in Bijna Echt - tijd met het stromen Segmentatie
description: Dit document bevat voorbeelden over het gebruik van streamingsegmentatie met de Adobe Experience Platform Segmentation Service-API.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 0%

---

# Evalueer gebeurtenissen in bijna real time met het stromen segmentatie

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met de API. Voor informatie bij het gebruiken van het stromen segmentatie die UI gebruiken, gelieve de [ het stromen segmentatie UI gids ](../ui/streaming-segmentation.md) te lezen.

Door segmentatie te streamen op [!DNL Adobe Experience Platform] kunnen klanten segmentering uitvoeren in de buurt van realtime en tegelijk de nadruk leggen op gegevensrijkdom. Met streamingsegmentatie gebeurt segmentkwalificatie nu als streaminggegevens in [!DNL Platform] terechtkomen, waardoor de noodzaak om segmentatietaken te plannen en uit te voeren, wordt verminderd. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in [!DNL Platform] worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie.
>
>Bovendien, kunnen de segmentdefinities die met het stromen segmentatie worden geëvalueerd tussen ideaal en daadwerkelijke lidmaatschap drijven als de segmentdefinitie van een andere segmentdefinitie wordt gebaseerd die gebruikend partijsegmentatie wordt geëvalueerd. Bijvoorbeeld, als Segment A van Segment B wordt gebaseerd, en Segment B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Segment B slechts om de 24 uur bijwerkt, zal Segment A zich verder van de daadwerkelijke gegevens bewegen tot het met de update van Segment B hersynchroniseert.

## Aan de slag

Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Adobe Experience Platform] diensten betrokken bij het stromen segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform consumentenprofiel in realtime, gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Segmentation]](../home.md): biedt de mogelijkheid om een publiek te maken met behulp van segmentdefinities en andere externe bronnen van uw [!DNL Real-Time Customer Profile] -gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen van [!DNL Platform] API&#39;s te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze ontwikkelaarsgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Voor het invullen van specifieke aanvragen kunnen extra kopteksten nodig zijn. In elk voorbeeld in dit document worden de juiste kopteksten weergegeven. Gelieve speciale aandacht te besteden aan de steekproefverzoeken om ervoor te zorgen dat alle vereiste kopballen inbegrepen zijn.

### Voor streaming segmentatie ingeschakelde querytypen {#query-types}

>[!NOTE]
>
>U zult geplande segmentatie voor de organisatie moeten toelaten opdat het stromen segmentatie werkt. De informatie over het toelaten van geplande segmentatie kan in [ worden gevonden toelaat geplande segmentatiesectie ](#enable-scheduled-segmentation)

Opdat een segmentdefinitie wordt geëvalueerd die het stromen segmentatie gebruikt, moet de vraag aan de volgende richtlijnen in overeenstemming zijn.

| Type query | Details |
| ---------- | ------- |
| Eén gebeurtenis binnen een tijdsvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een tijdvenster van minder dan 24 uur. |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Nota:** als een segment van segmenten wordt gebruikt, zal de profielontzetting **elke 24 uren** gebeuren. |
| Meerdere gebeurtenissen met een profielkenmerk | Om het even welke segmentdefinitie die naar veelvoudige gebeurtenissen **binnen de laatste 24 uren** verwijst en (naar keuze) heeft één of meerdere profielattributen. |

Een segmentdefinitie zal **** niet voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als het segment in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **** voor het stromen segmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

Houd rekening met de volgende richtlijnen bij het uitvoeren van streaming segmentatie:

| Type query | Richtsnoer |
| ---------- | -------- |
| Single-event-query | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het raadplegingsvenster is beperkt tot **één dag**.</li><li>Een strikte tijd-opdracht gevend voorwaarde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. Nochtans, kan de volledige gebeurtenis **niet** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een profiel niet langer in aanmerking komt voor een segmentdefinitie, wordt het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## Hiermee worden alle segmentdefinities opgehaald die zijn ingeschakeld voor streaming segmentatie

U kunt een lijst van al uw segmentdefinities terugwinnen die voor het stromen segmentatie binnen uw organisatie door een verzoek van de GET tot het `/segment/definitions` eindpunt te richten worden toegelaten.

**API formaat**

Als u streaming-ingeschakelde segmentdefinities wilt ophalen, moet u de queryparameter `evaluationInfo.continuous.enabled=true` opnemen in het aanvraagpad.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een serie van segmentdefinities in uw organisatie terug die voor het stromen segmentatie worden toegelaten.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## Een segmentdefinitie maken die geschikt is voor streaming

Een segmentdefinitie zal automatisch stromen-toegelaten zijn als het één van de [ het stromen segmentatietypen aanpast die hierboven ](#query-types) worden vermeld.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE]
>
>Dit is een standaard &quot;creeer een verzoek van de segmentdefinitie&quot;. Voor meer informatie over het creëren van een segmentdefinitie, te lezen gelieve het leerprogramma bij [ het creëren van een segmentdefinitie ](../tutorials/create-a-segment.md).

**Reactie**

Een succesvolle reactie keert de details van de nieuw gecreeerd streaming-toegelaten segmentdefinitie terug.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
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

Nadat de streamingevaluatie is ingeschakeld, moet een basislijn worden gemaakt (waarna de segmentdefinitie altijd up-to-date is). De geplande evaluatie (die ook als geplande segmentatie wordt bekend) moet eerst worden toegelaten opdat het systeem baselining automatisch uitvoert. Met geplande segmentatie, kan uw organisatie aan een terugkomende planning houden om de uitvoerbanen automatisch in werking te stellen om segmentdefinities te evalueren.

>[!NOTE]
>
>Een geplande evaluatie kan worden ingeschakeld voor sandboxen met maximaal vijf (5) samenvoegbeleidsregels voor [!DNL XDM Individual Profile] . Als uw organisatie meer dan vijf samenvoegbeleidsregels voor [!DNL XDM Individual Profile] heeft binnen één sandbox-omgeving, kunt u geen geplande evaluatie gebruiken.

### Een schema maken

Door een verzoek van de POST aan het `/config/schedules` eindpunt te doen, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **(Vereist)** De naam van programma. Moet een tekenreeks zijn. |
| `type` | **(Vereist)** Het baantype in koordformaat. De ondersteunde typen zijn `batch_segmentation` en `export` . |
| `properties` | **(Vereist)** Een voorwerp dat extra eigenschappen met betrekking tot het programma bevat. |
| `properties.segments` | **(Vereist als `type` gelijk is aan `batch_segmentation` )** `["*"]` zorgt ervoor dat alle segmentdefinities worden opgenomen. |
| `schedule` | **(Vereist)** Een koord dat het baanprogramma bevat. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Het getoonde voorbeeld (`0 0 1 * * ?`) betekent de baan elke dag bij 1 :00: 00 UTC wordt teweeggebracht. Voor meer informatie, te herzien gelieve het bijlage op het [ formaat van de cron uitdrukking ](./schedules.md#appendix) binnen de documentatie over programma&#39;s binnen segmentatie. |
| `state` | *(Facultatief)* Koord die de planningsstaat bevatten. Beschikbare waarden: `active` en `inactive` . De standaardwaarde is `inactive` . Een organisatie kan slechts één programma maken. De stappen voor het bijwerken van het programma zijn beschikbaar later in dit leerprogramma. |

**Reactie**

Een succesvolle reactie keert de details van het onlangs gecreeerde programma terug.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Een schema inschakelen

Een schema is standaard niet actief wanneer het wordt gemaakt, tenzij de eigenschap `state` is ingesteld op `active` in de aanvraagtekst (POST) create. U kunt een schema inschakelen (stel `state` in op `active` ) door een PATCH-aanvraag in te dienen bij het `/config/schedules` -eindpunt en de id van het schema op te nemen in het pad.

**API formaat**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Verzoek**

Het volgende verzoek gebruikt [ het formatteren van het Reparatie JSON ](https://datatracker.ietf.org/doc/html/rfc6902) om `state` van het programma aan `active` bij te werken.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Reactie**

Een geslaagde update retourneert een lege reactiehoofdtekst en HTTP Status 204 (Geen inhoud).

Dezelfde bewerking kan worden gebruikt om een schema uit te schakelen door de waarde in het vorige verzoek te vervangen door &quot;inactief&quot;.

## Volgende stappen

Nu u zowel nieuwe als bestaande segmentdefinities voor het stromen segmentatie hebt toegelaten, en geplande segmentatie toegelaten om een basislijn te ontwikkelen en terugkomende evaluaties uit te voeren, kunt u beginnen streaming-Toegelaten segmentdefinities voor uw organisatie tot stand te brengen.

Leren hoe te om gelijkaardige acties uit te voeren en met segmentdefinities te werken gebruikend het gebruikersinterface van Adobe Experience Platform, gelieve de [ gebruikersgids van de Bouwer van het Segment ](../ui/segment-builder.md) te bezoeken.

## Bijlage

In de volgende sectie worden veelgestelde vragen over streamingsegmentatie weergegeven:

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

Doorgaans gebeurt een onkwalificatie van streamingsegmentatie in real-time. Nochtans, die segmentdefinities stromen die segmenten van segmenten gebruiken **niet** in real time niet kwalificeren, in plaats daarvan na 24 uren unqualified.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie. Gebeurtenissen die naar het systeem worden gestreamd met een tijdstempel die ouder is dan 24 uur, worden verwerkt in de volgende batchtaak.

### Hoe worden segmentdefinities gedefinieerd als batch- of streaming-segmentatie?

Een segmentdefinitie wordt gedefinieerd als batch- of streaming-segmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst waarvan segmentdefinities als het stromen segment zullen worden geëvalueerd kan in de [ het stromen sectie van de segmenteringsvraagtypes ](#query-types) worden gevonden.

Gelieve te merken op dat als een segment **zowel** een `inSegment` uitdrukking als een directe enige-gebeurtenisketting bevat, het niet voor het stromen segmentatie kan kwalificeren. Als u deze segmentdefinitie voor het stromen segmentatie wilt kwalificeren, zou u de directe enige-gebeurtenisketting zijn eigen segmentdefinitie moeten maken.

### Waarom neemt het aantal &quot;totaal gekwalificeerde&quot;segmentdefinities toe terwijl het aantal onder &quot;Laatste X dagen&quot;bij nul blijft binnen de sectie van de segmentdefinitiedetails?

Het aantal totaal gekwalificeerde segmentdefinities wordt getrokken uit de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als streaming segmentdefinities kwalificeert. Deze waarde wordt weergegeven voor definities van zowel batch- als streaming segmenten.

Het aantal onder de &quot;Laatste dagen van X&quot;**slechts** omvat publiek dat in het stromen segmentatie wordt gekwalificeerd, en **slechts** verhogingen als u gegevens in het systeem hebt gestroomd en het telt naar die het stromen definitie. Deze waarde is **slechts** getoond voor het stromen segmentdefinities. Dientengevolge, kan deze waarde **** tonen als 0 voor de definities van het partijsegment.

Dientengevolge, als u ziet dat het aantal onder &quot;Laatste dagen van X&quot;nul is, en de lijngrafiek ook nul rapporteert, hebt u **** gestroomd geen profielen in het systeem dat voor die segmentdefinitie zou kwalificeren.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is?

Het duurt tot één uur voordat een segmentdefinitie beschikbaar is.

### Zijn er beperkingen aan de gegevens waarin wordt gestreamd?

Opdat de gestroomde gegevens in het stromen segmentatie worden gebruikt, moet **** het uit elkaar plaatsen tussen de gebeurtenissen zijn die binnen worden gestroomd. Als er te veel gebeurtenissen binnen dezelfde seconde worden gestreamd, behandelt Platform deze gebeurtenissen als door beide gegenereerde gegevens en worden ze genegeerd. Als beste praktijken, zou u **minstens** vijf seconden tussen gebeurtenisgegevens moeten hebben om ervoor te zorgen dat het gegeven behoorlijk wordt gebruikt.
