---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevens exporteren met API's
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# Profielgegevens exporteren met API&#39;s

In real time het Profiel van de Klant laat u toe om één enkele mening van individuele klanten te bouwen door gegevens uit veelvoudige bronnen, met inbegrip van zowel attributengegevens als gedragsgegevens te verenigen. De gegevens beschikbaar in het Profiel kunnen dan naar een dataset voor verdere verwerking worden uitgevoerd. Deze zelfstudie bevat stapsgewijze instructies voor het maken en beheren van exporttaken met de [segmentatie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Naast het maken van een exporttaak hebt u ook toegang tot profielgegevens via de API voor profieltoegang en projecties. Zie de zelfstudie over [de toegang tot het](../../profile/api/entities.md) profiel of de zelfstudie over het [configureren van Edge-doelen en -projecties](../../profile/api/edge-projections.md) voor meer informatie over deze andere toegangspatronen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het werken met profielgegevens. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

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

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Voor alle POST-, PUT- en PATCH-aanvragen is een extra header vereist:

- Inhoudstype: application/json

## Een exporttaak maken

Voor het exporteren van profielgegevens moet u eerst een gegevensset maken waarin de gegevens worden geëxporteerd en vervolgens een nieuwe exporttaak starten. Beide stappen kunnen worden verwezenlijkt gebruikend het Platform APIs van de Ervaring, met het eerste gebruikend de Dienst API van de Catalogus en het tweede gebruikend Real-time het Profiel van de Klant. Gedetailleerde instructies voor het voltooien van elke stap worden beschreven in de volgende secties.

- [Creeer een doeldataset](#create-a-target-dataset) - creeer een dataset om uitgevoerde gegevens te houden.
- [Start een nieuwe exporttaak](#initiate-export-job) - Vul de gegevensset met XDM Individuele profielgegevens.

### Een doelgegevensset maken

Bij het exporteren van profielgegevens moet eerst een doelgegevensset worden gemaakt. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset (`schemaRef.id` in de API steekproefaanvraag hieronder) wordt gebaseerd. Om een segment uit te voeren, moet de dataset op het Schema van de Unie van het Individuele Profiel XDM (`https://ns.adobe.com/xdm/context/profile__union`) worden gebaseerd. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de Individuele klasse van het Profiel XDM is. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve de sectie van het Profiel van de Klant in [real time van de Ontwikkelaar van het Registratie van het Schema gids](../../xdm/schema/composition.md#union).

De stappen die in deze zelfstudie volgen schetsen hoe te om een dataset tot stand te brengen die verwijzingen het Schema van de Unie van het Individuele Profiel XDM gebruikend Catalogus API. U kunt ook de gebruikersinterface van het Adobe Experience Platform gebruiken om een dataset te maken die verwijst naar het samenvoegingsschema. De stappen voor het gebruiken van UI worden geschetst in [deze zelfstudie UI voor het uitvoeren van segmenten](./create-dataset-export-segment.md) maar zijn ook hier van toepassing. Nadat u de bewerking hebt voltooid, kunt u terugkeren naar deze zelfstudie om door te gaan met de stappen voor het [starten van een nieuwe exporttaak](#initiate-export-job).

Als u al een compatibele dataset hebt en zijn identiteitskaart kent, kunt u rechtstreeks aan de stap voor het [in werking stellen van een nieuwe uitvoerbaan](#initiate-export-job)te werk gaan.

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
        "name": "Profile Data Export",
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

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde, unieke identiteitskaart van de pas gecreëerde dataset bevat. Een correct gevormde dataset ID wordt vereist om de gegevens van het Profiel met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Exporttaak starten

Zodra u een unie-persisterende dataset hebt, kunt u een uitvoerbaan tot stand brengen om de gegevens van het Profiel aan de dataset voort te zetten door een POST- verzoek aan het `/export/jobs` eindpunt in Real-time API van het Profiel van de Klant te richten en de details van de gegevens te verstrekken u in het lichaam van het verzoek wenst om uit te voeren.

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
| `fields` | *(Optioneel)* Beperkt de gegevensvelden die in de exportbewerking moeten worden opgenomen tot de gegevensvelden die in deze parameter zijn opgegeven. Dezelfde parameter is ook beschikbaar bij het maken van een segment, zodat de velden in het segment mogelijk al zijn gefilterd. Als u deze waarde weglaat, worden alle velden opgenomen in de geëxporteerde gegevens. |
| `mergePolicy` | *(Optioneel)* Hiermee geeft u het samenvoegbeleid op dat van toepassing is op de geëxporteerde gegevens. Neem deze parameter op wanneer er meerdere segmenten worden geëxporteerd. Als u deze waarde weglaat, zal de exportservice het samenvoegbeleid van het segment gebruiken. |
| `mergePolicy.id` | De id van het samenvoegbeleid. |
| `mergePolicy.version` | De specifieke versie van het samenvoegbeleid dat moet worden gebruikt. Als u deze waarde weglaat, wordt standaard de meest recente versie gebruikt. |
| `filter` | *(Optioneel)* Hiermee geeft u een of meer van de volgende filters op die u op het segment wilt toepassen voordat u het exporteert. |
| `filter.segments` | *(Optioneel)* Hiermee geeft u de segmenten op die u wilt exporteren. Als u deze waarde weglaat, worden alle gegevens van alle profielen geëxporteerd. Accepteert een array van segmentobjecten die elk de volgende velden bevatten:<ul><li>`segmentId`: **(Vereist als u`segments`)** Segment-id gebruikt voor profielen die moeten worden geëxporteerd.</li><li>`segmentNs` *(Optioneel)* Segmentnaamruimte voor de opgegeven `segmentID`.</li><li>`status` *(Optioneel)* Een array van tekenreeksen die een statusfilter voor de tekenreeks `segmentID`. Standaard heeft `status` deze waarde de waarde `["realized", "existing"]` die alle profielen vertegenwoordigt die in het segment op het huidige tijdstip vallen. Mogelijke waarden zijn: `"realized"`, `"existing"`, en `"exited"`.</br></br>Raadpleeg de zelfstudie over het [maken van segmenten voor meer informatie](./create-a-segment.md).</li></ul> |
| `filter.segmentQualificationTime` | *(Optioneel)* Filter op basis van de kwalificatietijd van het segment. De begintijd en/of eindtijd kunnen worden opgegeven. |
| `filter.segmentQualificationTime.startTime` | *(Optioneel)* Begintijd segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de begintijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.segmentQualificationTime.endTime` | *(Optioneel)* Eindtijd segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de eindtijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.fromIngestTimestamp ` | *(Optioneel)* Hiermee worden geëxporteerde profielen beperkt tot profielen die na deze tijdstempel zijn bijgewerkt. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. <ul><li>`fromIngestTimestamp` voor **profielen**, indien beschikbaar: Bevat alle samengevoegde profielen waarin de samengevoegde bijgewerkte tijdstempel groter is dan de opgegeven tijdstempel. Ondersteunt `greater_than` operand.</li><li>`fromTimestamp` voor **evenementen**: Alle gebeurtenissen die na deze tijdstempel worden ingevoerd, worden geëxporteerd volgens het resultaat van het profiel. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li> |
| `filter.emptyProfiles` | *(Optioneel)* Booleaans. Profielen kunnen profielrecords, ExperienceEvent-records of beide bevatten. Profielen zonder profielrecords en alleen ExperienceEvent-records worden &#39;emptyProfiles&#39; genoemd. Als u alle profielen in het profielarchief wilt exporteren, inclusief de &quot;emptyProfiles&quot;, stelt u de waarde van `emptyProfiles` in op `true`. Als `emptyProfiles` deze optie is ingesteld op `false`, worden alleen profielen geëxporteerd met profielrecords in de winkel. Als `emptyProfiles` kenmerk niet is opgenomen, worden standaard alleen profielen met profielrecords geëxporteerd. |
| `additionalFields.eventList` | *(Optioneel)* beheert de tijdreeksgebeurtenisvelden die worden geëxporteerd voor onderliggende of gekoppelde objecten door een of meer van de volgende instellingen op te geven:<ul><li>`eventList.fields`: Besturing van de velden die u wilt exporteren.</li><li>`eventList.filter`: Hiermee worden criteria opgegeven waarmee de resultaten van gekoppelde objecten worden beperkt. Hiermee wordt een minimumwaarde verwacht die vereist is voor het exporteren, meestal een datum.</li><li>`eventList.filter.fromIngestTimestamp`: Hiermee filtert u tijdreeksgebeurtenissen op de gebeurtenissen die na de opgegeven tijdstempel zijn ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li></ul> |
| `destination` | **(Vereist)** Doelgegevens voor de geëxporteerde gegevens:<ul><li>`destination.datasetId`: **(Vereist)** De id van de gegevensset waarin gegevens moeten worden geëxporteerd.</li><li>`destination.segmentPerBatch`: *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard op `false`. Een waarde van `false` exporteert alle segment-id&#39;s naar één batch-id. Een waarde van `true` exporteert één segment-id naar één batch-id. Merk op dat het plaatsen van de te zijn waarde `true` de prestaties van de partijuitvoer kan beïnvloeden.</li></ul> |
| `schema.name` | **(Vereist)** De naam van het schema dat is gekoppeld aan de gegevensset waarin gegevens moeten worden geëxporteerd. |

>[!NOTE] Als u alleen profielgegevens wilt exporteren, en geen gerelateerde ExperienceEvent-gegevens wilt opnemen, verwijdert u het object &quot;additionalFields&quot; uit de aanvraag.

**Antwoord**

Een succesvolle reactie keert een dataset terug die met de gegevens van het Profiel zoals die in het verzoek wordt gespecificeerd wordt bevolkt.

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

## Alle exporttaken weergeven

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
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
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

## Exportvoortgang volgen

Om de details van een specifieke uitvoerbaan te bekijken, of zijn status te controleren aangezien het verwerkt, kunt u een GET verzoek aan het `/export/jobs` eindpunt indienen en de `id` van de uitvoerbaan in de weg omvatten. De exporttaak is voltooid wanneer het `status` veld de waarde &quot;SUCCEEDED&quot; retourneert.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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
| `batchId` | De id van de batches die zijn gemaakt op basis van een geslaagde export en die moeten worden gebruikt voor opzoekdoeleinden bij het lezen van profielgegevens. |

## Een exporttaak annuleren

Met het Experience Platform kunt u een bestaande exporttaak annuleren. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de exporttaak niet is voltooid of vastgelopen in de verwerkingsfase. Als u een exporttaak wilt annuleren, kunt u een DELETE-aanvraag naar het `/export/jobs` eindpunt uitvoeren en de naam `id` van de exporttaak opnemen die u naar het aanvraagpad wilt annuleren.

**API-indeling**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` waarde van de exporttaak die u wilt openen. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 204 (Geen inhoud) en een lege antwoordinstantie die aangeeft dat de annuleringsbewerking is geslaagd.

## Volgende stappen

Zodra de export is voltooid, zijn uw gegevens beschikbaar in het Data Lake in Experience Platform. Vervolgens kunt u de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) gegevenstoegang gebruiken om toegang te krijgen tot de gegevens via de `batchId` koppeling die aan de export is gekoppeld. Afhankelijk van de grootte van de exportbewerking kunnen de gegevens in blokken staan en kan de batch uit meerdere bestanden bestaan.

Voor stapsgewijze instructies over het gebruik van de API voor gegevenstoegang voor het openen en downloaden van batchbestanden volgt u de zelfstudie [Gegevenstoegang](../../data-access/tutorials/dataset-data.md).

U kunt ook toegang krijgen tot geëxporteerde realtime klantprofielgegevens met Adobe Experience Platform Query Service. Gebruikend UI of RESTful API, staat de Dienst van de Vraag u toe om, vragen op gegevens binnen het meer van Gegevens te schrijven te bevestigen en in werking te stellen.

Voor meer informatie over hoe te om publieksgegevens te vragen, te herzien gelieve de documentatie [van de Dienst van de](../../query-service/home.md)Vraag.