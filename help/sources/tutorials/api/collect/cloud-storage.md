---
keywords: Experience Platform;home;populaire onderwerpen;gegevens over cloudopslag
solution: Experience Platform
title: Een gegevensstroom maken voor Cloud Storage-bronnen met behulp van de Flow Service API
topic-legacy: overview
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van externe cloudopslag en het naar Platform brengen van deze gegevens via bronconnectors en API's.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# Maak een gegevensstroom voor bronnen voor cloudopslag met de [!DNL Flow Service] API

Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een bron voor cloudopslag en het naar Platform brengen van deze gegevens met [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Als u een gegevensstroom wilt maken, moet u al een geldige basis-verbindings-id met een bron voor cloudopslag hebben. Als u deze id niet hebt, raadpleegt u de [overzicht van bronnen](../../../home.md#cloud-storage) voor een lijst met bronnen voor cloudopslag waarmee u een basisverbinding kunt maken.

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Handleiding voor ontwikkelaars van het schema Register](../../../../xdm/api/getting-started.md): Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot; en de vereiste kopteksten voor het indienen van verzoeken (met speciale aandacht voor de Accept-koptekst en de mogelijke waarden ervan).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Met de API voor batchverwerking kunt u gegevens als batchbestanden in het Experience Platform invoeren.
- [Sandboxen](../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../landing/api-guide.md).

## Een bronverbinding maken {#source}

U kunt een bronverbinding tot stand brengen door een verzoek van de POST aan [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor bestandsgebaseerde bronnen:

| Gegevensindeling | Enumwaarde |
| ----------- | ---------- |
| Gescheiden | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Voor alle op tabellen gebaseerde bronnen stelt u de waarde in op `tabular`.

- [Een bronverbinding maken met behulp van aangepaste, gescheiden bestanden](#using-custom-delimited-files)
- [Een bronverbinding maken met gecomprimeerde bestanden](#using-compressed-files)

**API-indeling**

```http
POST /sourceConnections
```

### Een bronverbinding maken met behulp van aangepaste, gescheiden bestanden {#using-custom-delimited-files}

**Verzoek**

U kunt een gescheiden bestand met een aangepast scheidingsteken invoeren door een `columnDelimiter` als een eigenschap. Elke waarde van één teken is een toegestaan kolomscheidingsteken. Indien niet opgegeven, een komma `(,)` wordt gebruikt als standaardwaarde.

Met de volgende voorbeeldaanvraag wordt een bronverbinding voor een gescheiden bestandstype gemaakt met door tabs gescheiden waarden.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `baseConnectionId` | De unieke verbinding-id van het externe cloudopslagsysteem dat u benadert. |
| `data.format` | Een opsommingswaarde die het kenmerk data format definieert. |
| `data.columnDelimiter` | U kunt elk scheidingsteken voor kolommen van één teken gebruiken om platte bestanden te verzamelen. Deze eigenschap is alleen vereist bij het opnemen van CSV- of TSV-bestanden. |
| `params.path` | Het pad van het bronbestand dat u opent. |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan uw specifieke externe cloudopslagsysteem. Zie de [aanhangsel](#appendix) voor een lijst van verbindingsspecificaties-id&#39;s. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Een bronverbinding maken met gecomprimeerde bestanden {#using-compressed-files}

**Verzoek**

U kunt ook gecomprimeerde JSON- of gescheiden-bestanden opnemen door de bijbehorende `compressionType` als een eigenschap. De lijst met ondersteunde gecomprimeerde bestandstypen is:

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

Met de volgende voorbeeldaanvraag wordt een bronverbinding gemaakt voor een gecomprimeerd, gescheiden bestand met behulp van een `gzip` bestandstype.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType": "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `data.properties.compressionType` | Bepaalt het gecomprimeerde bestandstype voor inname. Deze eigenschap is alleen vereist bij het invoegen van gecomprimeerde JSON- of gescheiden bestanden. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van de Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doel-XDM-schema kan worden gemaakt door een verzoek van de POST uit te voeren naar de [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](../../../../xdm/api/schemas.md).

## Een doelgegevensset maken {#target-dataset}

Een doeldataset kan tot stand worden gebracht door een verzoek van de POST aan [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), op voorwaarde dat de id van het doelschema zich binnen de payload bevindt.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met behulp van de API](../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart verstrekken van verbindingsspecificatie verbonden aan het meer van Gegevens. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het meer van Gegevens. Met deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```http
POST /targetConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.schema.id` | De `$id` van het doel-XDM-schema. |
| `data.schema.version` | De versie van het schema. Deze waarde moet worden ingesteld `application/vnd.adobe.xed-full+json;version=1`, die de laatste secundaire versie van het schema retourneert. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | The fixed connection spec ID to the Data Lake. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id van de nieuwe doelverbinding (`id`). Deze id is vereist in latere stappen.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt.

Als u een toewijzingenset wilt maken, vraagt u een POST aan de `mappingSets` van het [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) terwijl u uw doel-XDM-schema aanbiedt `$id` en de details van de toewijzingssets die u wilt maken.

>[!TIP]
>
>U kunt complexe gegevenstypen, zoals arrays, toewijzen in JSON-bestanden met behulp van een bronconnector voor cloudopslag.

**API-indeling**

```http
POST /conversion/mappingSets
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdmSchema` | De id van het doel-XDM-schema. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing inclusief de unieke id (`id`). Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Gegevensstroomspecificaties ophalen {#specs}

Een dataflow is verantwoordelijk voor het verzamelen van gegevens uit bronnen, en het brengen van hen in Platform. Als u een gegevensstroom wilt maken, moet u eerst de gegevensstroomspecificaties ophalen die verantwoordelijk zijn voor het verzamelen van gegevens voor cloudopslag.

**API-indeling**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de dataflow specificatie verantwoordelijk voor het brengen van gegevens van uw bron in Platform terug. De reactie bevat de unieke stroomspecificatie `id` vereist om een nieuwe gegevensstroom tot stand te brengen.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Een gegevensstroom maken

De laatste stap op weg naar het verzamelen van gegevens voor cloudopslag is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

- [Bronverbinding-id](#source)
- [Doelverbinding-id](#target)
- [Toewijzing-id](#mapping)
- [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

>[!NOTE]
>
>Voor batch-opname selecteert elke volgende gegevensstroom bestanden die van uw bron moeten worden ingepakt op basis van hun **laatst gewijzigd** tijdstempel. Dit betekent dat de partijgegevens uitgezochte dossiers van de bron die of nieuw zijn of sinds de laatste dataflow looppas zijn gewijzigd.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day`, of `week`. De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde op gelijk aan of groter dan `15`.

>[!IMPORTANT]
>
>Het wordt ten zeerste aanbevolen om uw gegevensstroom voor eenmalige inname te plannen wanneer u de [FTP-aansluiting](../../../connectors/cloud-storage/ftp.md).

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | De [stroom-specificatie-id](#specs) opgehaald in de vorige stap. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source) opgehaald in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target-connection) opgehaald in een eerdere stap. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) opgehaald in een eerdere stap. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor meer informatie over hoe te om dataflows te controleren, zie het leerprogramma op [gegevens controleren in de API](../monitor.md)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronaansluiting gemaakt om gegevens van uw cloudopslag op een geplande basis te verzamelen. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten voor Platforms, zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)

## Aanhangsel {#appendix}

In de volgende sectie worden de verschillende connectors voor bronnen voor cloudopslag en de bijbehorende verbindingsspecificaties weergegeven.

### Verbindingsspecificatie

| Naam van connector | Verbindingsspecificatie |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Klodder) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Gebeurtenishubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
