---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;export jobs;api;
solution: Experience Platform
title: Eindpunt van taken exporteren
topic: developer guide
description: De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt het /export/job eindpunt in de Segmentatie API van Adobe Experience Platform gebruiken, die u toestaat programmatically om, uitvoerbanen terug te winnen tot stand te brengen en te annuleren.
translation-type: tm+mt
source-git-commit: 783fa7ff0c22143a21c4f666c956c8b4d956189e
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 1%

---


# Eindpunt van taken exporteren

De banen van de uitvoer zijn asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten. U kunt het `/export/jobs` eindpunt in de Adobe Experience Platform Segmentation API gebruiken, die u toestaat programmatically om, uitvoerbanen terug te winnen tot stand te brengen en te annuleren.

>[!NOTE]
>
>Deze handleiding heeft betrekking op het gebruik van exportbanen in de [!DNL Segmentation API]Unie. Zie de handleiding over [!DNL Real-time Customer Profile] exporttaken in de profiel-API voor informatie over het beheren van exporttaken voor [gegevens](../../profile/api/export-jobs.md)

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Voordat u verdergaat, bekijkt u eerst de gids [](./getting-started.md) Aan de slag voor belangrijke informatie die u moet weten om oproepen naar de API met succes te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Een lijst met exporttaken ophalen {#retrieve-list}

U kunt een lijst van alle uitvoerbanen voor uw organisatie terugwinnen IMS door een verzoek van de GET aan het `/export/jobs` eindpunt te doen.

**API-indeling**

Het `/export/jobs` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te helpen verminderen. Het maken van een vraag aan dit eindpunt zonder parameters zal alle uitvoerbanen beschikbaar voor uw organisatie terugwinnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{LIMIT}` | Hiermee geeft u het aantal geretourneerde exporttaken op. |
| `{OFFSET}` | Hiermee bepaalt u de verschuiving van de resultatenpagina&#39;s. |
| `{STATUS}` | Filtert de resultaten op basis van status. De ondersteunde waarden zijn &quot;NEW&quot;, &quot;SUCCEEDED&quot; en &quot;FAILED&quot;. |

**Verzoek**

De volgende aanvraag haalt de laatste twee exporttaken binnen uw IMS-organisatie op.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie keert HTTP status 200 met een lijst van met succes voltooide uitvoerbanen terug, die op de vraagparameter wordt gebaseerd in de verzoekweg wordt verstrekt.

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
                        "status": ["realized", "existing"]
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
| `destination` | Doelgegevens voor de geëxporteerde gegevens:<ul><li>`datasetId`: De id van de gegevensset waarin gegevens zijn geëxporteerd.</li><li>`segmentPerBatch`: Een Booleaanse waarde die aangeeft of segment-id&#39;s worden geconsolideerd. De waarde &quot;false&quot; betekent dat alle segment-id&#39;s worden geëxporteerd naar één batch-id. De waarde &quot;true&quot; houdt in dat één segment-id wordt geëxporteerd naar één batch-id. **Opmerking:** Het instellen van de waarde op true kan van invloed zijn op de exportprestaties van batches.</li></ul> |
| `fields` | Een lijst met de geëxporteerde velden, gescheiden door komma&#39;s. |
| `schema.name` | De naam van het schema verbonden aan de dataset waar het gegeven moet worden uitgevoerd. |
| `filter.segments` | De segmenten die worden geëxporteerd. De volgende velden worden opgenomen:<ul><li>`segmentId`: De segment-id waarnaar profielen worden geëxporteerd.</li><li>`segmentNs`: Segmentnaamruimte voor de opgegeven naamruimte `segmentID`.</li><li>`status`: Een array van tekenreeksen die een statusfilter voor de `segmentID`tekenreeks bieden. Standaard heeft `status` deze waarde de waarde `["realized", "existing"]` die alle profielen vertegenwoordigt die in het segment op het huidige tijdstip vallen. Mogelijke waarden zijn: &quot;gerealiseerd&quot;, &quot;bestaand&quot; en &quot;verlaten&quot;. Een waarde van &quot;gerealiseerd&quot; betekent dat het profiel het segment binnengaat. Een waarde van &quot;bestaand&quot; betekent dat het profiel zich in het segment blijft bevinden. De waarde &quot;exiting&quot; houdt in dat het profiel het segment verlaat.</li></ul> |
| `mergePolicy` | Voeg beleidsinformatie voor de uitgevoerde gegevens samen. |
| `metrics.totalTime` | Een veld dat de totale tijd aangeeft waarop de exporttaak is uitgevoerd. |
| `metrics.profileExportTime` | Een veld waarin de exporttijd van de profielen wordt aangegeven. |
| `page` | Informatie over de paginering van de gewenste exporttaken. |
| `link.next` | Een koppeling naar de volgende pagina met exporttaken. |

## Een nieuwe exporttaak maken {#create}

U kunt een nieuwe uitvoerbaan tot stand brengen door een verzoek van de POST aan het `/export/jobs` eindpunt te doen.

**API-indeling**

```http
POST /export/jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe uitvoerbaan, die door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `filter.segments` | Hiermee geeft u de segmenten op die u wilt exporteren. Als u deze waarde weglaat, worden alle gegevens van alle profielen geëxporteerd. Accepteert een array van segmentobjecten die elk de volgende velden bevatten:<ul><li>`segmentId`: **(Vereist bij gebruik van `segments`)** Segment-id voor profielen die moeten worden geëxporteerd.</li><li>`segmentNs` *(Optioneel)* Segmentnaamruimte voor de opgegeven `segmentID`.</li><li>`status` *(Optioneel)* Een array van tekenreeksen die een statusfilter voor de `segmentID`tekenreeks bieden. Standaard heeft `status` deze waarde de waarde `["realized", "existing"]` die alle profielen vertegenwoordigt die in het segment op het huidige tijdstip vallen. Mogelijke waarden zijn: `"realized"`, `"existing"`en `"exited"`.  Een waarde van &quot;gerealiseerd&quot; betekent dat het profiel het segment binnengaat. Een waarde van &quot;bestaand&quot; betekent dat het profiel zich in het segment blijft bevinden. De waarde &quot;exiting&quot; houdt in dat het profiel het segment verlaat.</li></ul> |
| `filter.segmentQualificationTime` | Filter op basis van segmentkwalificatietijd. De begintijd en/of eindtijd kunnen worden opgegeven. |
| `filter.segmentQualificationTime.startTime` | Begintijd van segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de begintijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.segmentQualificationTime.endTime` | Eindtijd van segmentkwalificatie voor een segment-id voor een bepaalde status. Er is geen filter voor de eindtijd van een segment-id-kwalificatie opgegeven. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. |
| `filter.fromIngestTimestamp ` | Hiermee worden geëxporteerde profielen beperkt tot profielen die na deze tijdstempel zijn bijgewerkt. Het tijdstempel moet worden opgegeven in de [RFC 339](https://tools.ietf.org/html/rfc3339) -indeling. <ul><li>`fromIngestTimestamp` voor **profielen**, indien beschikbaar: Bevat alle samengevoegde profielen waarin de samengevoegde bijgewerkte tijdstempel groter is dan de opgegeven tijdstempel. Ondersteunt `greater_than` operand.</li><li>`fromIngestTimestamp` voor **evenementen**: Alle gebeurtenissen die na deze tijdstempel worden ingevoerd, worden geëxporteerd volgens het resultaat van het profiel. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li> |
| `filter.emptyProfiles` | Een booleaanse waarde die aangeeft of er voor lege profielen moet worden gefilterd. Profielen kunnen profielrecords, ExperienceEvent-records of beide bevatten. Profielen zonder profielrecords en alleen ExperienceEvent-records worden &#39;emptyProfiles&#39; genoemd. Als u alle profielen in het profielarchief wilt exporteren, inclusief de &quot;emptyProfiles&quot;, stelt u de waarde in op `emptyProfiles` op `true`. Als `emptyProfiles` deze optie is ingesteld op `false`, worden alleen profielen met profielrecords in de winkel geëxporteerd. Als `emptyProfiles` kenmerk niet is opgenomen, worden standaard alleen profielen met profielrecords geëxporteerd. |
| `additionalFields.eventList` | Bepaalt de tijdlijngebeurtenisvelden die worden geëxporteerd voor onderliggende of gekoppelde objecten door een of meer van de volgende instellingen op te geven:<ul><li>`fields`: Besturing van de velden die u wilt exporteren.</li><li>`filter`: Hiermee worden criteria opgegeven waarmee de resultaten van gekoppelde objecten worden beperkt. Hiermee wordt een minimumwaarde verwacht die vereist is voor het exporteren, meestal een datum.</li><li>`filter.fromIngestTimestamp`: Hiermee filtert u tijdreeksgebeurtenissen naar gebeurtenissen die na de opgegeven tijdstempel zijn ingevoegd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li><li>`filter.toIngestTimestamp`: Hiermee wordt de tijdstempel gefilterd op de tijdstempel die vóór de opgegeven tijdstempel is ingevoerd. Dit is niet de tijd van de gebeurtenis zelf, maar de tijd van inname voor de gebeurtenissen.</li></ul> |
| `destination` | **(Vereist)** Informatie over de geëxporteerde gegevens:<ul><li>`datasetId`: **(Vereist)** De id van de gegevensset waarin gegevens moeten worden geëxporteerd.</li><li>`segmentPerBatch`: *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard &quot;false&quot; is. De waarde &quot;false&quot; exporteert alle segment-id&#39;s naar één batch-id. De waarde &quot;waar&quot; exporteert één segment-id naar één batch-id. Merk op dat het plaatsen van de waarde &quot;waar&quot;kan beïnvloeden partijuitvoerprestaties.</li></ul> |
| `schema.name` | **(Vereist)** De naam van het schema dat is gekoppeld aan de gegevensset waarin gegevens moeten worden geëxporteerd. |
| `evaluationInfo.segmentation` | *(Optioneel)* Een Booleaanse waarde die, indien niet opgegeven, standaard op `false`. Een waarde van `true` geeft aan dat segmentatie moet worden uitgevoerd op de exporttaak. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met details van de nieuwe exporttaak.

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
    "imsOrgId": "{IMS_ORG}",
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

Als deze `destination.segmentPerBatch` was ingesteld op `true`, zou het bovenstaande `destination` object een `batches` array hebben, zoals hieronder wordt getoond:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
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

## Een specifieke exporttaak ophalen {#get}

U kunt gedetailleerde informatie over een specifieke de uitvoerbaan terugwinnen door een verzoek van de GET aan het `/export/jobs` eindpunt te doen en identiteitskaart van de de uitvoerbaan te verstrekken u in de verzoekweg wenst terug te winnen.

**API-indeling**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` waarde van de exporttaak die u wilt openen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over de opgegeven exporttaak.

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
    "imsOrgId": "{IMS_ORG}",
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
| `destination` | Doelgegevens voor de geëxporteerde gegevens:<ul><li>`datasetId`: De id van de gegevensset waarin de gegevens zijn geëxporteerd.</li><li>`segmentPerBatch`: Een Booleaanse waarde die aangeeft of segment-id&#39;s worden geconsolideerd. Een waarde van `false` betekent alle segment-id&#39;s in één batch-id. Een waarde van `true` betekent dat één segment-id wordt geëxporteerd naar één batch-id.</li></ul> |
| `fields` | Een lijst met de geëxporteerde velden, gescheiden door komma&#39;s. |
| `schema.name` | De naam van het schema verbonden aan de dataset waar het gegeven moet worden uitgevoerd. |
| `filter.segments` | De segmenten die worden geëxporteerd. De volgende velden worden opgenomen:<ul><li>`segmentId`: Segment-id voor profielen die moeten worden geëxporteerd.</li><li>`segmentNs`: Segmentnaamruimte voor de opgegeven naamruimte `segmentID`.</li><li>`status`: Een array van tekenreeksen die een statusfilter voor de `segmentID`tekenreeks bieden. Standaard heeft `status` deze waarde de waarde `["realized", "existing"]` die alle profielen vertegenwoordigt die in het segment op het huidige tijdstip vallen. Mogelijke waarden zijn: &quot;gerealiseerd&quot;, &quot;bestaand&quot; en &quot;verlaten&quot;.  Een waarde van &quot;gerealiseerd&quot; betekent dat het profiel het segment binnengaat. Een waarde van &quot;bestaand&quot; betekent dat het profiel zich in het segment blijft bevinden. De waarde &quot;exiting&quot; houdt in dat het profiel het segment verlaat.</li></ul> |
| `mergePolicy` | Voeg beleidsinformatie voor de uitgevoerde gegevens samen. |
| `metrics.totalTime` | Een veld dat de totale tijd aangeeft waarop de exporttaak is uitgevoerd. |
| `metrics.profileExportTime` | Een veld waarin de exporttijd van de profielen wordt aangegeven. |
| `totalExportedProfileCounter` | Het totale aantal profielen dat is geëxporteerd naar alle batches. |

## Een specifieke exporttaak annuleren of verwijderen {#delete}

U kunt verzoeken om de opgegeven exporttaak te verwijderen door een DELETE-aanvraag in te dienen bij het `/export/jobs` eindpunt en de id op te geven van de exporttaak die u wilt verwijderen in het aanvraagpad.

**API-indeling**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | De `id` naam van de exporttaak die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 204 met het volgende bericht:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe exporttaken werken.