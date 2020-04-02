---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een segment evalueren
topic: tutorial
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# Evalueer en open segmentresultaten

Dit document biedt een zelfstudie voor het evalueren van segmenten en het benaderen van segmentresultaten met de [segmentatie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het maken van doelsegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Adobe Experience Platform Segmentation Service](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
- [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste koppen

Deze zelfstudie vereist ook dat u de [verificatiezelfstudie](../../tutorials/authentication.md) hebt voltooid om oproepen naar platform-API&#39;s te kunnen uitvoeren. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken aan platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

> [!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Voor alle POST-, PUT- en PATCH-aanvragen is een extra header vereist:

- Inhoudstype: application/json

## Een segment evalueren

Zodra u hebt ontwikkeld, getest en uw segmentdefinitie bewaard, kunt u het segment door of geplande evaluatie of op bestelling evaluatie dan evalueren.

[De geplande evaluatie](#scheduled-evaluation) (die ook als &quot;geplande segmentatie&quot;wordt bekend) staat u toe om een terugkomende planning voor het runnen van een uitvoerbaan in een specifieke tijd tot stand te brengen, terwijl de [op bestelling evaluatie](#on-demand-evaluation) het creëren van een segmentbaan impliceert om het publiek onmiddellijk te bouwen. De stappen voor elk worden hieronder geschetst.

Als u nog niet een segment [creeert creeert een segment gebruikend de Realtime leerprogramma](./create-a-segment.md) van het Profiel van de Klant of creeerde een segmentdefinitie gebruikend [de Bouwer](../ui/overview.md)van het Segment, gelieve dit te doen alvorens met dit leerprogramma te werk te gaan.

## Geplande evaluatie

Via een geplande evaluatie kan uw IMS-organisatie een terugkerend schema maken om exporttaken automatisch uit te voeren.

> [!NOTE] De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor Individueel Profiel XDM worden toegelaten. Als uw organisatie meer dan vijf samenvoegingsbeleid voor Individueel Profiel XDM binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

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

### Werk de planningstijd bij

De timing van het programma kan worden bijgewerkt door een verzoek van de PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg te doen.

**API-indeling**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Verzoek**

In het volgende verzoek wordt de opmaak [van](http://jsonpatch.com/) JSON-patch gebruikt om de [uitsnijdexpressie](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) voor het schema bij te werken. In dit voorbeeld wordt het schema nu geactiveerd om 10:15:00 UTC.

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
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Antwoord**

Een geslaagde update retourneert een lege reactiehoofdtekst en HTTP Status 204 (Geen inhoud).

## Evaluatie op aanvraag

De evaluatie op bestelling staat u toe om een segmentbaan tot stand te brengen om een publiekssegment te produceren wanneer u het vereist. In tegenstelling tot geplande evaluatie, zal dit slechts gebeuren wanneer gevraagd en niet terugkerend.

### Een segmenttaak maken

Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt. Het verwijst naar een segmentdefinitie, evenals om het even welk samenvoegbeleid dat controleert hoe het Profiel van de Klant in real time overlappende attributen over uw profielfragmenten samenvoegt. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over het segment, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen.

U kunt een nieuwe segmentbaan tot stand brengen door een POST- verzoek aan het `/segment/jobs` eindpunt in Real-time API van het Profiel van de Klant te doen.

**API-indeling**

```http
POST /segment/jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe segmentbaan die op de twee segmentdefinities wordt gebaseerd die in de lading worden verstrekt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentId` | De id van een segmentdefinitie waaruit het publiek moet worden opgebouwd. Ten minste één segment-id moet in de payload-array worden opgegeven. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde segmentbaan, met inbegrip van zijn, read-only, systeem-geproduceerde waarde terug die aan deze segmentbaan uniek is. `id`

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de nieuwe segmenttaak die voor opzoekdoeleinden wordt gebruikt. |
| `status` | De huidige status van de segmenttaak. Wordt &quot;VERWERKEN&quot; totdat de verwerking is voltooid, waarna het &quot;SUCCEEDED&quot; of &quot;FAILED&quot; wordt. |

### Status segmenttaak opzoeken

U kunt `id` voor een specifieke segmentbaan gebruiken om een raadplegingsverzoek (GET) uit te voeren om de huidige status van de baan te bekijken.

**API-indeling**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | De `id` waarde van de segmenttaak die u wilt openen. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvolle reactie retourneert de details van de segmentatietaak en geeft verschillende informatie afhankelijk van de huidige status van de taak. U kunt het raadplegingsverzoek herhalen tot het &quot;SUCCEEDED&quot; `status` bereikt, waarbij u het segment naar een dataset kunt uitvoeren.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentedProfileCounter` | Het totale aantal samengevoegde profielen dat voor het segment in aanmerking komt. |
| `segmentedProfileByNamespaceCounter` | Een uitsplitsing van de profielen die in aanmerking komen voor het segment naar naamruimtecode van de identiteit. Een lijst met naamruimtecodes voor identiteiten vindt u in het overzicht [van de](../../identity-service/namespaces.md)naamruimte. |

## Segmentresultaten interpreteren

Wanneer de segmentbanen met succes in werking worden gesteld, wordt de `segmentMembership` kaart bijgewerkt voor elk profiel inbegrepen binnen het segment. `segmentMembership` slaat ook om het even welke vooraf beoordeelde publiekssegmenten op die in Platform worden opgenomen, die voor integratie met andere oplossingen zoals de Manager van de Audience van Adobe toestaan.

In het volgende voorbeeld wordt getoond hoe het `segmentMembership` kenmerk eruitziet voor elke afzonderlijke profielrecord:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `lastQualificationTime` | De tijdstempel op het moment dat de bevestiging van het segmentlidmaatschap werd uitgevoerd en het profiel het segment inging of verlaat. |
| `status` | De status van segmentdeelname als onderdeel van het huidige verzoek. Moet gelijk zijn aan een van de volgende bekende waarden: <ul><li>`existing`: Entiteit blijft deel uitmaken van het segment.</li><li>`realized`: De entiteit gaat het segment in.</li><li>`exited`: Entiteit verlaat het segment.</li></ul> |

## Resultaten van toegangssegmenten

De resultaten van een segmentbaan kunnen op één van twee manieren worden betreden: u kunt tot individuele profielen toegang hebben of een volledig publiek naar een dataset uitvoeren.

In de volgende secties worden deze opties gedetailleerder beschreven.

## Een profiel opzoeken

Als u het specifieke profiel kent waartoe u toegang wilt hebben, kunt u dit doen gebruikend de Real-time API van het Profiel van de Klant. De volledige stappen voor toegang tot individuele profielen zijn beschikbaar in de gegevens van het Profiel van de Klant van de [Toegang in real time gebruikend het profiel API](../../profile/api/entities.md) leerprogramma.

## Een segment exporteren

Nadat een segmentatietaak met succes is voltooid (de waarde van het `status` attribuut is &quot;SUCCEEDED&quot;), kunt u uw publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld.

De volgende stappen zijn vereist om uw publiek te exporteren:

- [Creeer een doeldataset](#create-a-target-dataset) - creeer de dataset om publieksleden te houden.
- [Produceer publieksprofielen in de dataset](#generate-profiles-for-audience-members) - bevolk de dataset met Individuele Profielen XDM die op de resultaten van een segmentbaan worden gebaseerd.
- [Voortgang](#monitor-export-progress) export controleren - controleer de huidige voortgang van het exportproces.
- [Lees publieksgegevens](#next-steps) - Haal de resulterende afzonderlijke XDM-profielen op die de leden van uw publiek vertegenwoordigen.

### Een doelgegevensset maken

Wanneer het uitvoeren van een publiek, moet een doeldataset eerst worden gecreeerd. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset (`schemaRef.id` in de API steekproefaanvraag hieronder) wordt gebaseerd. Om een segment uit te voeren, moet de dataset op het Schema van de Unie van het Individuele Profiel XDM (`https://ns.adobe.com/xdm/context/profile__union`) worden gebaseerd. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de Individuele klasse van het Profiel XDM is. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve de sectie van het Profiel van de Klant in [real time van de Ontwikkelaar van het Registratie van het Schema gids](../../xdm/api/getting-started.md).

Er zijn twee manieren om de noodzakelijke dataset tot stand te brengen:

- **API&#39;s gebruiken:** De stappen die in deze zelfstudie volgen schetsen hoe te om een dataset tot stand te brengen die verwijzingen het Schema van de Unie van het Individuele Profiel XDM gebruikend Catalogus API.
- **De interface gebruiken:** Als u de gebruikersinterface van het Adobe Experience Platform wilt gebruiken om een dataset te maken die verwijst naar het union-schema, voert u de stappen in de [UI-zelfstudie](../ui/overview.md) uit en gaat u terug naar deze zelfstudie om door te gaan met de stappen voor het [genereren van profielen](#generate-xdm-profiles-for-audience-members)van publiek.

Als u reeds een compatibele dataset hebt en zijn identiteitskaart kent, kunt u aan de stap voor het [produceren van publieksprofielen](#generate-xdm-profiles-for-audience-members)direct te werk gaan.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, die configuratieparameters in de lading verstrekken.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "aspect": "production"
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een beschrijvende naam voor de gegevensset. |
| `schemaRef.id` | Identiteitskaart van de verenigingsmening (schema) dat de dataset zal worden geassocieerd met. |
| `fileDescription.persisted` | Een waarde Van Boole die wanneer reeks aan `true`, toelaat de dataset om in de verenigingsmening voort te bestaan. |

**Antwoord**

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde unieke identiteitskaart van de pas gecreëerde dataset bevat. Een behoorlijk gevormde dataset identiteitskaart wordt vereist om publieksleden met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Profielen genereren voor publieksleden

Zodra u een unie-persisterende dataset hebt, kunt u een uitvoerbaan tot stand brengen om de publieksleden aan de dataset voort te zetten door een POST- verzoek aan het `/export/jobs` eindpunt in het Real-time Profiel van de Klant te richten API en de dataset identiteitskaart en de segmentinformatie voor de segmenten te verstrekken die u wenst om uit te voeren.

**API-indeling**

```http
POST /export/jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe de uitvoerbaan, die configuratieparameters in de lading verstrekt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `fields` | *(Optioneel)* Beperkt de gegevensvelden die in de exportbewerking moeten worden opgenomen tot de gegevensvelden die in deze parameter zijn opgegeven. Dezelfde parameter is ook beschikbaar bij het maken van een segment, zodat de velden in het segment mogelijk al zijn gefilterd. Als u deze waarde weglaat, worden alle velden opgenomen in de geëxporteerde gegevens |
| `mergePolicy` | *(Optioneel)* Hiermee geeft u het samenvoegbeleid op dat van toepassing is op de geëxporteerde gegevens. Neem deze parameter op wanneer er meerdere segmenten worden geëxporteerd. Als u deze waarde weglaat, zal de exportservice het samenvoegbeleid van het segment gebruiken. |
| `mergePolicy.id` | De id van het samenvoegbeleid |
| `mergePolicy.version` | De specifieke versie van het samenvoegbeleid dat moet worden gebruikt. Als u deze waarde weglaat, wordt standaard de meest recente versie gebruikt. |
| `filter` | *(Optioneel)* Hiermee geeft u een of meer van de volgende filters op die vóór het exporteren op het segment moeten worden toegepast: |
| `filter.segments` | *(Optioneel)* Hiermee geeft u de segmenten op die u wilt exporteren. Als u deze waarde weglaat, worden alle gegevens van alle profielen geëxporteerd. Accepteert een array van segmentobjecten die elk de volgende velden bevatten: |
| `filter.segments.segmentId` | **(Vereist bij gebruik van`segments`)** Segment-id voor profielen die moeten worden geëxporteerd. |
| `filter.segments.segmentNs` | *(Optioneel)* Segmentnaamruimte voor de opgegeven `segmentID`. |
| `filter.segments.status` | *(Optioneel)* Een array van tekenreeksen die een statusfilter voor de `segmentID`tekenreeks bieden. Standaard heeft `status` deze waarde de waarde `["realized", "existing"]` die alle profielen vertegenwoordigt die in het segment op het huidige tijdstip vallen. Mogelijke waarden zijn: `"realized"`, `"existing"`, en `"exited"`. |
| `filter.segmentQualificationTime` | *(Optioneel)* Filter op basis van de kwalificatietijd van het segment. De begintijd en/of eindtijd kunnen worden opgegeven. |
| `filter.segmentQualificationTime.startTime` | *(Optioneel)* Begintijd segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de begintijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.segmentQualificationTime.endTime` | *(Optioneel)* Eindtijd segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de eindtijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.fromIngestTimestamp` | *(Optioneel)* Hiermee worden geëxporteerde profielen beperkt tot profielen die na deze tijdstempel zijn bijgewerkt. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.fromIngestTimestamp` voor **profielen**, indien beschikbaar | Bevat alle samengevoegde profielen waarin de samengevoegde bijgewerkte tijdstempel groter is dan de opgegeven tijdstempel. Ondersteunt `greater_than` operand. |
| `filter.fromTimestamp` for events | Alle gebeurtenissen die na deze tijdstempel worden ingevoerd, worden geëxporteerd volgens het resultaat van het profiel. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen. |
| `filter.emptyProfiles` | *(Optioneel)* Booleaans. Profielen kunnen profielrecords, ExperienceEvent-records of beide bevatten. Profielen zonder profielrecords en alleen ExperienceEvent-records worden &#39;emptyProfiles&#39; genoemd. Als u alle profielen in het profielarchief wilt exporteren, inclusief de &quot;emptyProfiles&quot;, stelt u de waarde van `emptyProfiles` in op `true`. Als `emptyProfiles` deze optie is ingesteld op `false`, worden alleen profielen geëxporteerd met profielrecords in de winkel. Als `emptyProfiles` kenmerk niet is opgenomen, worden standaard alleen profielen met profielrecords geëxporteerd. |
| `additionalFields.eventList` | *(Optioneel)* beheert de tijdreeksgebeurtenisvelden die worden geëxporteerd voor onderliggende of gekoppelde objecten door een of meer van de volgende instellingen op te geven: |
| `additionalFields.eventList.fields` | Besturing van de velden die u wilt exporteren. |
| `additionalFields.eventList.filter` | Hiermee worden criteria opgegeven waarmee de resultaten van gekoppelde objecten worden beperkt. Hiermee wordt een minimumwaarde verwacht die vereist is voor het exporteren, meestal een datum. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Hiermee filtert u tijdreeksgebeurtenissen op de gebeurtenissen die na de opgegeven tijdstempel zijn ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen. |
| `destination` | **(Vereist)** Doelinformatie voor de geëxporteerde gegevens |
| `destination.datasetId` | **(Vereist)** De id van de gegevensset waarin gegevens moeten worden geëxporteerd. |
| `destination.segmentPerBatch` | *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard op `false`. Een waarde van `false` exporteert alle segment-id&#39;s naar één batch-id. Een waarde van `true` exporteert één segment-id naar één batch-id. Merk op dat het plaatsen van de te zijn waarde `true` de prestaties van de partijuitvoer kan beïnvloeden. |
| `schema.name` | **(Vereist)** De naam van het schema dat is gekoppeld aan de gegevensset waarin gegevens moeten worden geëxporteerd. |

**Antwoord**

Een succesvolle reactie keert een dataset terug die met profielen wordt bevolkt die voor de laatste voltooide looppas van de segmentbaan kwalificeerden. Alle profielen die voorheen in de dataset bestonden maar tijdens de laatste voltooide uitvoering van de segmenttaak niet in aanmerking kwamen voor het segment, zijn verwijderd.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Als het verzoek `destination.segmentPerBatch` niet was opgenomen (indien aanwezig, standaard ingesteld op `false`) of als de waarde was ingesteld op `false`, zou het `destination` object in de bovenstaande reactie geen `batches` array hebben en in plaats daarvan slechts één array bevatten, `batchId`zoals hieronder wordt weergegeven. Die enige partij zou alle segment IDs omvatten, terwijl de reactie hierboven één enkele segmentidentiteitskaart per partijidentiteitskaart toont.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Alle exporttaken weergeven

U kunt een lijst van alle uitvoerbanen voor een bepaalde organisatie terugkeren IMS door een GET verzoek aan het `export/jobs` eindpunt uit te voeren. Het verzoek steunt ook de vraagparameters `limit` en `offset`, zoals hieronder getoond.

**API-indeling**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `limit` | Geef het aantal records op dat moet worden geretourneerd. |
| `offset` | Verplaats de pagina met resultaten die door het opgegeven getal moeten worden geretourneerd. |


**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat een `records` object dat de exporttaken bevat die door uw IMS-organisatie zijn gemaakt.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Exportvoortgang volgen

Als de processen van de uitvoerbaan, kunt u zijn status controleren door een GET verzoek aan het `/export/jobs` eindpunt en met inbegrip `id` van de uitvoerbaan in de weg te doen. De exporttaak is voltooid wanneer het `status` veld de waarde &quot;SUCCEEDED&quot; retourneert.

**API-indeling**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` waarde van de exporttaak die u wilt openen. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `batchId` | De id van de batches die zijn gemaakt op basis van een geslaagde export en die moeten worden gebruikt voor opzoekdoeleinden bij het lezen van de publieksgegevens. |

## Volgende stappen

Zodra de export is voltooid, zijn uw gegevens beschikbaar in het Data Lake in Experience Platform. Vervolgens kunt u de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) gegevenstoegang gebruiken om toegang te krijgen tot de gegevens via de `batchId` koppeling die aan de export is gekoppeld. Afhankelijk van de grootte van het segment, kunnen de gegevens in brokken zijn en de partij kan uit verscheidene dossiers bestaan.

Voor stapsgewijze instructies over het gebruik van de API voor gegevenstoegang voor het openen en downloaden van batchbestanden volgt u de zelfstudie [Gegevenstoegang](../../data-access/tutorials/dataset-data.md).

U kunt geëxporteerde segmentgegevens ook openen met Adobe Experience Platform Query Service. Gebruikend UI of RESTful API, staat de Dienst van de Vraag u toe om, vragen op gegevens binnen het meer van Gegevens te schrijven te bevestigen en in werking te stellen.

Voor meer informatie over hoe te om publieksgegevens te vragen, te herzien gelieve de documentatie [van de Dienst van de](../../query-service/home.md)Vraag.
