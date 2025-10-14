---
solution: Experience Platform
title: API-eindpunt voor segmentexporttaken
description: De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt het /export/job eindpunt in de API van de Dienst van de Segmentatie van Adobe Experience Platform gebruiken, die u toestaat om, uitvoerbanen programmatically terug te winnen tot stand te brengen en te annuleren.
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---

# Het eindpunt van segmentexporttaken

De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt het `/export/jobs` eindpunt in de Adobe Experience Platform Segmentation API gebruiken, die u toestaat programmatically om, uitvoerbanen terug te winnen tot stand te brengen en te annuleren.

>[!NOTE]
>
>Deze handleiding behandelt het gebruik van exporttaken in de [!DNL Segmentation API] . Voor informatie over hoe te om uitvoerbanen voor [!DNL Real-Time Customer Profile] gegevens te beheren, zie de gids over [&#x200B; de uitvoerbanen in het Profiel API &#x200B;](../../profile/api/export-jobs.md)

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met exporttaken ophalen {#retrieve-list}

U kunt een lijst van alle uitvoerbanen voor uw organisatie terugwinnen door een verzoek van de GET tot het `/export/jobs` eindpunt te richten.

**API formaat**

Het `/export/jobs` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle uitvoerbanen beschikbaar voor uw organisatie terugwinnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**de parameters van de Vraag**

+++ Een lijst met beschikbare queryparameters.

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `limit` | Hiermee geeft u het aantal geretourneerde exporttaken op. | `limit=10` |
| `offset` | Hiermee bepaalt u de verschuiving van de resultatenpagina&#39;s. | `offset=1540974701302_96` |
| `status` | Hiermee filtert u de resultaten op basis van de status. De ondersteunde waarden zijn NEW, SUCCEEDED en FAILED. | `status=NEW` |

+++

**Verzoek**

Het volgende verzoek zal de laatste twee uitvoerbanen binnen uw organisatie terugwinnen.

+++ Een voorbeeldverzoek om exporttaken op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

De volgende reactie keert HTTP status 200 met een lijst van met succes voltooide uitvoerbanen terug, die op de vraagparameter wordt gebaseerd in de verzoekweg wordt verstrekt.

+++ Een voorbeeldreactie bij het ophalen van exporttaken.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `destination` | Doelgegevens voor de geëxporteerde gegevens:<ul><li>`datasetId`: De id van de gegevensset waarin gegevens zijn geëxporteerd.</li><li>`segmentPerBatch`: Een Booleaanse waarde die aangeeft of segment-id&#39;s worden geconsolideerd. De waarde &quot;false&quot; betekent dat alle segment-id&#39;s worden geëxporteerd naar één batch-id. De waarde &quot;true&quot; houdt in dat één segment-id wordt geëxporteerd naar één batch-id. **Nota:** het plaatsen van de waarde aan waar kan partijuitvoerprestaties beïnvloeden.</li></ul> |
| `fields` | Een lijst met de geëxporteerde velden, gescheiden door komma&#39;s. |
| `schema.name` | De naam van het schema verbonden aan de dataset waar het gegeven moet worden uitgevoerd. |
| `filter.segments` | De segmenten die worden geëxporteerd. De volgende velden worden opgenomen:<ul><li>`segmentId`: De segment-id waarnaar profielen worden geëxporteerd.</li><li>`segmentNs`: segmentnaamruimte voor de opgegeven `segmentID` .</li><li>`status`: Een array van tekenreeksen die een statusfilter voor de `segmentID` verschaft. Standaard heeft `status` de waarde `["realized"]` die alle profielen vertegenwoordigt die op dat moment in het segment vallen. Mogelijke waarden zijn: `realized` en `exited` . De waarde `realized` betekent dat het profiel voor het segment in aanmerking komt. De waarde `exiting` betekent dat het profiel het segment verlaat.</li></ul> |
| `mergePolicy` | Voeg beleidsinformatie voor de uitgevoerde gegevens samen. |
| `metrics.totalTime` | Een veld dat de totale tijd aangeeft waarop de exporttaak is uitgevoerd. |
| `metrics.profileExportTime` | Een veld waarin de exporttijd van de profielen wordt aangegeven. |
| `page` | Informatie over de paginering van de gewenste exporttaken. |
| `link.next` | Een koppeling naar de volgende pagina met exporttaken. |

+++

## Een nieuwe exporttaak maken {#create}

U kunt een nieuwe exportbaan tot stand brengen door een verzoek van de POST aan het `/export/jobs` eindpunt te doen.

**API formaat**

```http
POST /export/jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe uitvoerbaan, die door de parameters wordt gevormd die in de lading worden verstrekt.

+++ Een voorbeeldverzoek om een exporttaak te maken.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `fields` | Een lijst met de geëxporteerde velden, gescheiden door komma&#39;s. Als deze optie leeg blijft, worden alle velden geëxporteerd. |
| `mergePolicy` | Hier geeft u het samenvoegbeleid op dat van toepassing is op de geëxporteerde gegevens. Neem deze parameter op wanneer er meerdere segmenten worden geëxporteerd. Als deze optie niet wordt opgegeven, zal het exportbeleid hetzelfde zijn als het opgegeven segment. |
| `filter` | Een object dat aangeeft welke segmenten afhankelijk van de hieronder vermelde subeigenschappen in de exporttaak moeten worden opgenomen op basis van id, kwalificatietijd of ingangstijd. Als deze optie leeg blijft, worden alle gegevens geëxporteerd. |
| `filter.segments` | Hiermee geeft u de segmenten op die u wilt exporteren. Als u deze waarde weglaat, worden alle gegevens van alle profielen geëxporteerd. Accepteert een array van segmentobjecten die elk de volgende velden bevatten:<ul><li>`segmentId`: **(Vereist als u `segments` gebruikt)** Segment-id voor profielen die moeten worden geëxporteerd.</li><li>`segmentNs` *(Optioneel)* Segmentnaamruimte voor de opgegeven `segmentID` .</li><li>`status` *(Facultatief)* Een serie van koorden die een statusfilter voor `segmentID` verstrekken. Standaard heeft `status` de waarde `["realized"]` die alle profielen vertegenwoordigt die op dat moment in het segment vallen. Mogelijke waarden zijn: `realized` en `exited` .  De waarde `realized` betekent dat het profiel voor het segment in aanmerking komt. De waarde `exiting` betekent dat het profiel het segment verlaat.</li></ul> |
| `filter.segmentQualificationTime` | Filter op basis van segmentkwalificatietijd. De begintijd en/of eindtijd kunnen worden opgegeven. |
| `filter.segmentQualificationTime.startTime` | Begintijd van segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de begintijd van een segment-id-kwalificatie opgegeven. Tijdstempel moet in [&#x200B; RFC 3339 &#x200B;](https://tools.ietf.org/html/rfc3339) formaat worden verstrekt. |
| `filter.segmentQualificationTime.endTime` | Eindtijd van segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de eindtijd van een segment-id-kwalificatie opgegeven. Tijdstempel moet in [&#x200B; RFC 3339 &#x200B;](https://tools.ietf.org/html/rfc3339) formaat worden verstrekt. |
| `filter.fromIngestTimestamp ` | Hiermee worden geëxporteerde profielen beperkt tot profielen die na deze tijdstempel zijn bijgewerkt. Tijdstempel moet in [&#x200B; RFC 3339 &#x200B;](https://tools.ietf.org/html/rfc3339) formaat worden verstrekt. <ul><li>`fromIngestTimestamp` voor **profielen**, als verstrekt: Omvat alle samengevoegde profielen waar samengevoegde bijgewerkte timestamp groter is dan bepaalde timestamp. Ondersteunt `greater_than` operand.</li><li>`fromIngestTimestamp` voor **gebeurtenissen**: Alle gebeurtenissen die na dit timestamp worden opgenomen zullen worden uitgevoerd die aan het resulterende profielresultaat beantwoorden. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li> |
| `filter.emptyProfiles` | Een booleaanse waarde die aangeeft of er voor lege profielen moet worden gefilterd. Profielen kunnen profielrecords, ExperienceEvent-records of beide bevatten. Profielen zonder profielrecords en alleen ExperienceEvent-records worden &#39;emptyProfiles&#39; genoemd. Als u alle profielen wilt exporteren in het profielarchief, inclusief de &quot;emptyProfiles&quot;, stelt u de waarde van `emptyProfiles` in op `true` . Als `emptyProfiles` is ingesteld op `false` , worden alleen profielen met profielrecords in de winkel geëxporteerd. Als het kenmerk `emptyProfiles` niet is opgenomen, worden standaard alleen profielen met profielrecords geëxporteerd. |
| `additionalFields.eventList` | Bepaalt de tijdlijngebeurtenisvelden die worden geëxporteerd voor onderliggende of gekoppelde objecten door een of meer van de volgende instellingen op te geven:<ul><li>`fields` : hiermee bepaalt u de velden die u wilt exporteren.</li><li>`filter` - Geeft criteria op die de resultaten beperken die van gekoppelde objecten worden opgenomen. Hiermee wordt een minimumwaarde verwacht die vereist is voor het exporteren, meestal een datum.</li><li>`filter.fromIngestTimestamp`: hiermee worden gebeurtenissen uit de tijdreeks gefilterd op gebeurtenissen die na de opgegeven tijdstempel zijn ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li><li>`filter.toIngestTimestamp`: hiermee wordt de tijdstempel gefilterd naar de tijdstempel die vóór de opgegeven tijdstempel is ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li></ul> |
| `destination` | **(Vereist)** Informatie over de uitgevoerde gegevens:<ul><li>`datasetId`: **(Vereist)** identiteitskaart van de dataset waar het gegeven moet worden uitgevoerd.</li><li>`segmentPerBatch`: *(Facultatief)* Een waarde Van Boole die, als niet verstrekt, aan &quot;vals&quot;in gebreke blijft. De waarde &quot;false&quot; exporteert alle segment-id&#39;s naar één batch-id. De waarde &quot;waar&quot; exporteert één segment-id naar één batch-id. Merk op dat het plaatsen van de waarde om &quot;waar&quot;te zijn de prestaties van de partijuitvoer kan beïnvloeden.</li></ul> |
| `schema.name` | **(Vereist)** De naam van het schema verbonden aan de dataset waar het gegeven moet worden uitgevoerd. |
| `evaluationInfo.segmentation` | *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard op `false` wordt ingesteld. De waarde `true` geeft aan dat segmentatie moet worden uitgevoerd op de exporttaak. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van de nieuwe exporttaak.

+++ Een voorbeeldreactie bij het maken van een exporttaak.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een door het systeem gegenereerde alleen-lezen waarde die de exporttaak identificeert die zojuist is gemaakt. |

Als `destination.segmentPerBatch` was ingesteld op `true` , heeft het bovenstaande `destination` -object een `batches` array, zoals hieronder wordt getoond:

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

+++

## Een specifieke exporttaak ophalen {#get}

U kunt gedetailleerde informatie over een specifieke uitvoerbaan terugwinnen door een verzoek van de GET aan het `/export/jobs` eindpunt te richten en identiteitskaart van de de uitvoerbaan te verstrekken u in de verzoekweg wenst terug te winnen.

**API formaat**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` van de exporttaak die u wilt openen. |

**Verzoek**

+++ Een voorbeeldaanvraag om een exporttaak op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over de opgegeven exporttaak.

+++ Een voorbeeldreactie bij het ophalen van een exporttaak.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `destination` | Doelgegevens voor de geëxporteerde gegevens:<ul><li>`datasetId`: De id van de gegevensset waarin de gegevens zijn geëxporteerd.</li><li>`segmentPerBatch`: Een Booleaanse waarde die aangeeft of segment-id&#39;s worden geconsolideerd. De waarde `false` betekent dat alle segment-id&#39;s zich in één batch-id bevonden. De waarde `true` betekent dat één segment-id wordt geëxporteerd naar één batch-id.</li></ul> |
| `fields` | Een lijst met de geëxporteerde velden, gescheiden door komma&#39;s. |
| `schema.name` | De naam van het schema verbonden aan de dataset waar het gegeven moet worden uitgevoerd. |
| `filter.segments` | De segmenten die worden geëxporteerd. De volgende velden worden opgenomen:<ul><li>`segmentId`: segment-id voor profielen die moeten worden geëxporteerd.</li><li>`segmentNs`: segmentnaamruimte voor de opgegeven `segmentID` .</li><li>`status`: Een array van tekenreeksen die een statusfilter voor de `segmentID` verschaft. Standaard heeft `status` de waarde `["realized"]` die alle profielen vertegenwoordigt die op dat moment in het segment vallen. Mogelijke waarden zijn: `realized` en `exited` .  De waarde `realized` betekent dat het profiel voor het segment in aanmerking komt. De waarde `exiting` betekent dat het profiel het segment verlaat.</li></ul> |
| `mergePolicy` | Voeg beleidsinformatie voor de uitgevoerde gegevens samen. |
| `metrics.totalTime` | Een veld dat de totale tijd aangeeft waarop de exporttaak is uitgevoerd. |
| `metrics.profileExportTime` | Een veld waarin de exporttijd van de profielen wordt aangegeven. |
| `totalExportedProfileCounter` | Het totale aantal profielen dat is geëxporteerd naar alle batches. |

+++

## Een specifieke exporttaak annuleren of verwijderen {#delete}

U kunt verzoeken om de opgegeven exporttaak te verwijderen door een DELETE-aanvraag in te dienen bij het `/export/jobs` -eindpunt en de id op te geven van de exporttaak die u wilt verwijderen in het aanvraagpad.

**API formaat**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` van de exporttaak die u wilt verwijderen. |

**Verzoek**

+++ Een voorbeeldaanvraag om een exporttaak te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 204 met het volgende bericht:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe exporttaken werken.
