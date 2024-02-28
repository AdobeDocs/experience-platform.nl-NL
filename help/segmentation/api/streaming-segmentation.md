---
solution: Experience Platform
title: Evalueer Gebeurtenissen in Bijna Echt - tijd met het stromen Segmentatie
description: Dit document bevat voorbeelden over het gebruik van streamingsegmentatie met de Adobe Experience Platform Segmentation Service-API.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Evalueer gebeurtenissen in bijna real time met het stromen segmentatie

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met de API. Voor informatie over het gebruik van streaming segmentatie via de gebruikersinterface, leest u de [UI-gids voor streamingsegmentatie](../ui/streaming-segmentation.md).

Segmentering streamen op [!DNL Adobe Experience Platform] staat klanten toe om segmentatie in bijna real time te doen terwijl het concentreren op gegevensrijkdom. Met streaming segmentering gebeurt segmentkwalificatie nu als streaming gegevens binnenkomen [!DNL Platform], om de noodzaak om segmentatietaken te plannen en uit te voeren te verlichten. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien het gegeven wordt overgegaan in [!DNL Platform]Dit betekent dat segmentlidmaatschap up-to-date blijft zonder geplande segmentatietaken uit te voeren.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie.
>
>Bovendien, kunnen de segmentdefinities die met het stromen segmentatie worden geëvalueerd tussen ideaal en daadwerkelijke lidmaatschap drijven als de segmentdefinitie van een andere segmentdefinitie wordt gebaseerd die gebruikend partijsegmentatie wordt geëvalueerd. Bijvoorbeeld, als Segment A van Segment B wordt gebaseerd, en Segment B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Segment B slechts om de 24 uur bijwerkt, zal Segment A zich verder van de daadwerkelijke gegevens bewegen tot het met de update van Segment B hersynchroniseert.

## Aan de slag

Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] diensten betrokken bij het stromen segmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Biedt een eenvormig consumentenprofiel in real-time, gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Segmentation]](../home.md): Verstrekt de capaciteit om publiek tot stand te brengen gebruikend segmentdefinities en andere externe bronnen van uw [!DNL Real-Time Customer Profile] gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze ontwikkelaarsgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Toestemming: houder `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Voor het invullen van specifieke aanvragen kunnen extra kopteksten nodig zijn. In elk voorbeeld in dit document worden de juiste kopteksten weergegeven. Gelieve speciale aandacht te besteden aan de steekproefverzoeken om ervoor te zorgen dat alle vereiste kopballen inbegrepen zijn.

### Voor streaming segmentatie ingeschakelde querytypen {#query-types}

>[!NOTE]
>
>U zult geplande segmentatie voor de organisatie moeten toelaten opdat het stromen segmentatie werkt. Informatie over het inschakelen van geplande segmentatie vindt u in het gedeelte [geplande segmenteringssectie inschakelen](#enable-scheduled-segmentation)

Opdat een segmentdefinitie wordt geëvalueerd die het stromen segmentatie gebruikt, moet de vraag aan de volgende richtlijnen in overeenstemming zijn.

| Type query | Details |
| ---------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. |
| Eén gebeurtenis binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis. |
| Eén gebeurtenis met een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis met een tijdvenster. |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Opmerking:** Als een segment van segmenten wordt gebruikt, zal de profielontzetting gebeuren **om de 24 uur**. |
| Meerdere gebeurtenissen met een profielkenmerk | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de laatste 24 uur** en (optioneel) heeft een of meer profielkenmerken. |

Een segmentdefinitie zal **niet** voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie omvat een combinatie van één gebeurtenis en een `inSegment` gebeurtenis.
   - Als het segment echter in de `inSegment` gebeurtenis is alleen profiel, de segmentdefinitie **zal** is ingeschakeld voor streamingsegmentatie.

Houd rekening met de volgende richtlijnen bij het uitvoeren van streaming segmentatie:

| Type query | Richtsnoer |
| ---------- | -------- |
| Single-event-query | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugzoekvenster is beperkt tot **één dag**.</li><li>Een strikte voorwaarde voor de tijdvolgorde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. De gehele gebeurtenis **kan** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een profiel niet langer in aanmerking komt voor een segmentdefinitie, wordt het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## Hiermee worden alle segmentdefinities opgehaald die zijn ingeschakeld voor streaming segmentatie

U kunt een lijst van al uw segmentdefinities terugwinnen die voor het stromen segmentatie binnen uw organisatie door een verzoek van de GET aan te dienen worden toegelaten `/segment/definitions` eindpunt.

**API-indeling**

Om streaming-toegelaten segmentdefinities terug te winnen, moet u de vraagparameter omvatten `evaluationInfo.continuous.enabled=true` in het aanvraagpad.

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

**Antwoord**

Een succesvolle reactie keert een serie van segmentdefinities in uw organisatie terug die voor het stromen segmentatie worden toegelaten.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
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
            "ttlInDays": 30,
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

Als een segmentdefinitie overeenkomt met een van de [hierboven vermelde typen streamingsegmentatie](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>Dit is een standaard &quot;creeer een verzoek van de segmentdefinitie&quot;. Lees de zelfstudie voor meer informatie over het maken van een segmentdefinitie [segmentdefinitie maken](../tutorials/create-a-segment.md).

**Antwoord**

Een succesvolle reactie keert de details van de nieuw gecreeerd streaming-toegelaten segmentdefinitie terug.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
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
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor worden toegelaten [!DNL XDM Individual Profile]. Als uw organisatie meer dan vijf samenvoegbeleidsregels heeft voor [!DNL XDM Individual Profile] binnen één sandboxomgeving kunt u geen geplande evaluatie gebruiken.

### Een schema maken

Door een POST aan de `/config/schedules` eindpunt, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

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
| `name` | **(Vereist)** De naam van het schema. Moet een tekenreeks zijn. |
| `type` | **(Vereist)** Het taaktype in tekenreeksindeling. De ondersteunde typen zijn `batch_segmentation` en `export`. |
| `properties` | **(Vereist)** Een object dat aanvullende eigenschappen bevat die verwant zijn aan het schema. |
| `properties.segments` | **(Vereist als `type` equals `batch_segmentation`)** Gebruiken `["*"]` zorgt ervoor dat alle segmentdefinities worden opgenomen. |
| `schedule` | **(Vereist)** Een tekenreeks met het taakschema. Taken kunnen slechts eenmaal per dag worden uitgevoerd, wat betekent dat u een taak niet meer dan één keer kunt plannen gedurende een periode van 24 uur. Het getoonde voorbeeld (`0 0 1 * * ?`) betekent dat de baan elke dag om 1 wordt geactiveerd:00:00 UTC. Voor meer informatie raadpleegt u de bijlage bij de [expressie-indeling voor uitsnijden](./schedules.md#appendix) binnen de documentatie over de programma&#39;s binnen de segmentatie. |
| `state` | *(Optioneel)* Tekenreeks die de planningsstatus bevat. Beschikbare waarden: `active` en `inactive`. Standaardwaarde is `inactive`. Een organisatie kan slechts één programma maken. De stappen voor het bijwerken van het programma zijn beschikbaar later in dit leerprogramma. |

**Antwoord**

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

Een schema is standaard inactief wanneer het wordt gemaakt, tenzij het `state` eigenschap is ingesteld op `active` in de create (POST) aanvraaginstantie. U kunt een programma inschakelen (stel de `state` tot `active`) door een PATCH-verzoek aan de `/config/schedules` en met inbegrip van identiteitskaart van het programma in de weg.

**API-indeling**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Verzoek**

Het volgende verzoek gebruikt [JSON-patchopmaak](https://datatracker.ietf.org/doc/html/rfc6902) om de `state` van het schema `active`.

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

**Antwoord**

Een geslaagde update retourneert een lege reactiehoofdtekst en HTTP Status 204 (Geen inhoud).

Dezelfde bewerking kan worden gebruikt om een schema uit te schakelen door de waarde in het vorige verzoek te vervangen door &quot;inactief&quot;.

## Volgende stappen

Nu u zowel nieuwe als bestaande segmentdefinities voor het stromen segmentatie hebt toegelaten, en geplande segmentatie toegelaten om een basislijn te ontwikkelen en terugkomende evaluaties uit te voeren, kunt u beginnen streaming-Toegelaten segmentdefinities voor uw organisatie tot stand te brengen.

Ga voor meer informatie over het uitvoeren van vergelijkbare acties en het werken met segmentdefinities in de Adobe Experience Platform-gebruikersinterface naar de [Gebruikershandleiding voor Segment Builder](../ui/segment-builder.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over streamingsegmentatie weergegeven:

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

Doorgaans gebeurt een onkwalificatie van streamingsegmentatie in real-time. Bij streamingsegmentdefinities die gebruikmaken van segmenten, is dit echter wel het geval **niet** in real time niet in aanmerking komen, in plaats daarvan na 24 uur niet in aanmerking.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie. Gebeurtenissen die naar het systeem worden gestreamd met een tijdstempel die ouder is dan 24 uur, worden verwerkt in de volgende batchtaak.

### Hoe worden segmentdefinities gedefinieerd als batch- of streaming-segmentatie?

Een segmentdefinitie wordt gedefinieerd als batch- of streaming-segmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst met segmentdefinities die als streaming segment worden geëvalueerd, kunt u vinden in het dialoogvenster [sectie met querytypen voor streamingsegmentering](#query-types).

Houd er rekening mee dat als een segment **beide** een `inSegment` en een directe &#39;single-event&#39;-keten, kan deze niet in aanmerking komen voor streamingsegmentatie. Als u deze segmentdefinitie voor het stromen segmentatie wilt kwalificeren, zou u de directe enige-gebeurtenisketting zijn eigen segmentdefinitie moeten maken.

### Waarom neemt het aantal &quot;totaal gekwalificeerde&quot;segmentdefinities toe terwijl het aantal onder &quot;Laatste X dagen&quot;bij nul blijft binnen de sectie van de segmentdefinitiedetails?

Het aantal totaal gekwalificeerde segmentdefinities wordt getrokken uit de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als streaming segmentdefinities kwalificeert. Deze waarde wordt weergegeven voor definities van zowel batch- als streaming segmenten.

Het getal onder de &quot;Laatste X dagen&quot; **alleen** omvat doelgroepen die zijn gekwalificeerd in streamingsegmentatie, en **alleen** neemt toe als u gegevens in het systeem hebt gestreamd en het telt naar die het stromen definitie. Deze waarde is **alleen** weergegeven voor streamingsegmentdefinities. Dientengevolge, deze waarde **kan** weergeven als 0 voor definities van batchsegmenten.

Als u dus ziet dat het getal onder &quot;Laatste X dagen&quot; nul is en dat de lijngrafiek ook nul rapporteert, hebt u **niet** profielen naar het systeem gestreamd die voor die segmentdefinitie in aanmerking zouden komen.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is?

Het duurt tot één uur voordat een segmentdefinitie beschikbaar is.
