---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: API-eindpunt voor taken exporteren
topic: guide
type: Documentation
description: In realtime klantprofiel kunt u één weergave van individuele klanten in Adobe Experience Platform samenstellen door gegevens uit meerdere bronnen samen te voegen, inclusief kenmerkgegevens en gedragsgegevens. De gegevens van het profiel kunnen dan naar een dataset voor verdere verwerking worden uitgevoerd.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 0%

---

# Eindpunt van taken exporteren

[!DNL Real-time Customer Profile] laat u toe om één enkele mening van individuele klanten te bouwen door gegevens uit veelvoudige bronnen, met inbegrip van zowel attributengegevens als gedragsgegevens te verenigen. De gegevens van het profiel kunnen dan naar een dataset voor verdere verwerking worden uitgevoerd. De publiekssegmenten van [!DNL Profile]-gegevens kunnen bijvoorbeeld worden geëxporteerd voor activering en profielkenmerken kunnen worden geëxporteerd voor rapportage.

Dit document bevat stapsgewijze instructies voor het maken en beheren van exporttaken met de [profiel-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Deze handleiding behandelt het gebruik van exporttaken in [!DNL Profile API]. Voor informatie over hoe te om uitvoerbanen voor de Dienst van de Segmentatie van Adobe Experience Platform te beheren, zie de gids over [uitvoerbanen in de Segmentatie API](../../profile/api/export-jobs.md).

Naast het creëren van een uitvoerbaan, kunt u tot [!DNL Profile] gegevens ook toegang hebben gebruikend het `/entities` eindpunt, ook gekend als &quot;[!DNL Profile Access]&quot;. Zie [eindpuntgids voor entiteiten](./entities.md) voor meer informatie. Raadpleeg de [gebruikershandleiding](../ui/user-guide.md) voor informatie over hoe u toegang krijgt tot [!DNL Profile]-gegevens via de gebruikersinterface.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van [!DNL Real-time Customer Profile] API. Lees voordat u doorgaat de [Aan de slag-handleiding](getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Een exporttaak maken

Voor het exporteren van [!DNL Profile]-gegevens moet eerst een gegevensset worden gemaakt waarin de gegevens worden geëxporteerd en vervolgens een nieuwe exporttaak worden gestart. Beide stappen kunnen worden verwezenlijkt gebruikend Experience Platform APIs, met het eerste gebruikend de Dienst API van de Catalogus en het laatste gebruikend Real-time het Profiel van de Klant. Gedetailleerde instructies voor het voltooien van elke stap worden beschreven in de volgende secties.

### Een doelgegevensset maken

Bij het exporteren van [!DNL Profile]-gegevens moet eerst een doelgegevensset worden gemaakt. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset (`schemaRef.id` in het API steekproefverzoek hieronder) wordt gebaseerd. Voor het exporteren van profielgegevens moet de gegevensset zijn gebaseerd op het [!DNL XDM Individual Profile] Unieschema (`https://ns.adobe.com/xdm/context/profile__union`). Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen. In dit geval is dat de klasse [!DNL XDM Individual Profile]. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve de [vaksectie in de grondbeginselen van schema samenstellings gids](../../xdm/schema/composition.md#union).

De stappen die in deze zelfstudie volgen schetsen hoe te om een dataset tot stand te brengen die [!DNL XDM Individual Profile] het Schema van de Unie gebruikend [!DNL Catalog] API van verwijzingen voorziet. U kunt de [!DNL Platform] gebruikersinterface ook gebruiken om een dataset tot stand te brengen die verwijzingen het unieschema. De stappen voor het gebruiken van UI worden geschetst in [deze zelfstudie UI voor het uitvoeren van segmenten](../../segmentation/tutorials/create-dataset-export-segment.md) maar zijn hier eveneens van toepassing. Nadat u de instructie hebt voltooid, kunt u terugkeren naar deze zelfstudie om door te gaan met de stappen voor het starten van een nieuwe exporttaak](#initiate).[

Als u reeds een compatibele dataset hebt en zijn identiteitskaart kent, kunt u aan de stap voor [het in werking stellen van een nieuwe de uitvoerbaan](#initiate) direct te werk gaan.

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
          "persisted": true
        }
      }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een beschrijvende naam voor de gegevensset. |
| `schemaRef.id` | Identiteitskaart van de verenigingsmening (schema) dat de dataset zal worden geassocieerd met. |
| `fileDescription.persisted` | Een Booleaanse waarde; als de waarde is ingesteld op `true`, kan de gegevensset blijven staan in de samenvoegweergave. |

**Antwoord**

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde, unieke identiteitskaart van de pas gecreëerde dataset bevat. Een correct gevormde dataset ID wordt vereist om de gegevens van het Profiel met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Exporttaak {#initiate} starten

Zodra u een unie-persisterende dataset hebt, kunt u een uitvoerbaan tot stand brengen om de gegevens van het Profiel aan de dataset voort te zetten door een verzoek van de POST aan het `/export/jobs` eindpunt in Real-time het Profiel van de Klant te richten API en de details van de gegevens te verstrekken u in het lichaam van het verzoek wenst om uit te voeren.

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
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `fields` | *(Optioneel)* Beperkt de gegevensvelden die in de exportbewerking moeten worden opgenomen tot de gegevensvelden die in deze parameter zijn opgegeven. Als u deze waarde weglaat, worden alle velden opgenomen in de geëxporteerde gegevens. |
| `mergePolicy` | *(Optioneel)* Hiermee geeft u het samenvoegbeleid op dat de geëxporteerde gegevens moet regelen. Neem deze parameter op wanneer er meerdere segmenten worden geëxporteerd. |
| `mergePolicy.id` | De id van het samenvoegbeleid. |
| `mergePolicy.version` | De specifieke versie van het samenvoegbeleid dat moet worden gebruikt. Als u deze waarde weglaat, wordt standaard de meest recente versie gebruikt. |
| `additionalFields.eventList` | *(Optioneel)* beheert de tijdlijngebeurtenisvelden die worden geëxporteerd voor onderliggende of gekoppelde objecten door een of meer van de volgende instellingen op te geven:<ul><li>`eventList.fields`: Besturing van de velden die u wilt exporteren.</li><li>`eventList.filter`: Hiermee worden criteria opgegeven waarmee de resultaten van gekoppelde objecten worden beperkt. Hiermee wordt een minimumwaarde verwacht die vereist is voor het exporteren, meestal een datum.</li><li>`eventList.filter.fromIngestTimestamp`: Hiermee filtert u tijdreeksgebeurtenissen naar gebeurtenissen die na de opgegeven tijdstempel zijn ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li></ul> |
| `destination` | **(Vereist)** Doelgegevens voor de geëxporteerde gegevens:<ul><li>`destination.datasetId`:  **(Vereist)** De id van de gegevensset waarin gegevens moeten worden geëxporteerd.</li><li>`destination.segmentPerBatch`:  *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard op  `false`. De waarde `false` exporteert alle segment-id&#39;s naar één batch-id. Met de waarde `true` wordt één segment-id naar één batch-id geëxporteerd. Het instellen van de waarde op `true` kan van invloed zijn op de exportprestaties van batches.</li></ul> |
| `schema.name` | **(Vereist)** De naam van het schema verbonden aan de dataset waar de gegevens moeten worden uitgevoerd. |

>[!NOTE]
>
>Als u alleen profielgegevens wilt exporteren en geen gerelateerde tijdreeksgegevens wilt opnemen, verwijdert u het object &quot;additionalFields&quot; uit de aanvraag.

**Antwoord**

Een succesvolle reactie keert een dataset terug die met de gegevens van het Profiel zoals die in het verzoek wordt gespecificeerd wordt bevolkt.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
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
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Alle exporttaken weergeven

U kunt een lijst van alle uitvoerbanen voor een bepaalde organisatie terugkeren IMS door een verzoek van de GET aan het `export/jobs` eindpunt uit te voeren. Het verzoek steunt ook de vraagparameters `limit` en `offset`, zoals hieronder getoond.

**API-indeling**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `start` | Verschuif de pagina met geretourneerde resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: `start=4` |
| `limit` | Beperk het aantal geretourneerde resultaten. Voorbeeld: `limit=10` |
| `page` | Retourneer een specifieke pagina met resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: `page=2` |
| `sort` | Sorteer de resultaten op een specifiek veld in oplopende ( **`asc`**) of aflopende ( **`desc`**) volgorde. De sorteerparameter werkt niet bij het retourneren van meerdere pagina&#39;s met resultaten. Voorbeeld: `sort=updateTime:asc` |

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

De reactie bevat een `records`-object dat de exporttaken bevat die door uw IMS-organisatie zijn gemaakt.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
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

Als u de details van een specifieke exporttaak wilt bekijken of de status van de taak wilt controleren terwijl deze wordt verwerkt, kunt u een GET-verzoek indienen bij het `/export/jobs`-eindpunt en `id` van de exporttaak opnemen in het pad. De exporttaak is voltooid wanneer het veld `status` de waarde &quot;SUCCEEDED&quot; retourneert.

**API-indeling**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` van de exporttaak die u wilt openen. |

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
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
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

Met Experience Platform kunt u een bestaande exporttaak annuleren. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de exporttaak niet is voltooid of vastgelopen in het verwerkingsstadium. Als u een exporttaak wilt annuleren, kunt u een DELETE-verzoek uitvoeren naar het `/export/jobs`-eindpunt en de `id` van de exporttaak opnemen die u wilt annuleren naar het aanvraagpad.

**API-indeling**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` van de exporttaak die u wilt openen. |

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

Nadat het exporteren is voltooid, zijn uw gegevens beschikbaar in het Data Lake in Experience Platform. U kunt de [API van de Toegang van Gegevens ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dan gebruiken om tot de gegevens toegang te hebben gebruikend `batchId` verbonden aan de uitvoer. Afhankelijk van de grootte van de exportbewerking kunnen de gegevens in blokken staan en kan de batch uit meerdere bestanden bestaan.

Voor geleidelijke instructies op hoe te om de Toegang API van Gegevens te gebruiken om tot partijdossiers toegang te hebben en te downloaden, volg [de zelfstudie van de Toegang van Gegevens](../../data-access/tutorials/dataset-data.md).

U kunt ook toegang krijgen tot geëxporteerde realtime klantprofielgegevens met Adobe Experience Platform Query Service. Gebruikend UI of RESTful API, staat de Dienst van de Vraag u toe om, vragen op gegevens binnen het meer van Gegevens te schrijven te bevestigen en in werking te stellen.

Voor meer informatie over hoe te om publieksgegevens te vragen, te herzien [de documentatie van de Dienst van de Vraag](../../query-service/home.md).

## Aanhangsel

De volgende sectie bevat aanvullende informatie over exporttaken in de profiel-API.

### Aanvullende voorbeelden voor het laden van exporten

Met de voorbeeld-API-aanroep in de sectie over het starten van een exporttaak](#initiate) wordt een taak gemaakt die zowel profiel- (record) als gebeurtenis- (tijdreeks) gegevens bevat. [ Deze sectie verstrekt extra voorbeelden van de verzoeklading om uw uitvoer te beperken tot één gegevenstype of andere.

Met de volgende payload wordt een exporttaak gemaakt die alleen profielgegevens bevat (geen gebeurtenissen):

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Als u een exporttaak wilt maken die alleen gebeurtenisgegevens bevat (geen profielkenmerken), ziet de payload er mogelijk ongeveer als volgt uit:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
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
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Segmenten exporteren

U kunt ook het eindpunt van exporttaken gebruiken om doelsegmenten te exporteren in plaats van [!DNL Profile]-gegevens. Zie de handleiding over [exporttaken in de segmentatie-API](../../segmentation/api/export-jobs.md) voor meer informatie.
