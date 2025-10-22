---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslaggegevens
solution: Experience Platform
title: Een gegevensstroom maken voor Cloud Storage-bronnen met behulp van de Flow Service API
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het ophalen van gegevens van externe cloudopslag en het naar Experience Platform brengen van deze gegevens via bronconnectors en API's.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 2ad0ffba128e8c51f173d24d4dd2404b9cbbb59a
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Een gegevensstroom maken voor bronnen voor cloudopslag met de API [!DNL Flow Service]

Dit leerprogramma behandelt de stappen om gegevens van een bron van de wolkenopslag terug te winnen en hen te brengen aan Experience Platform gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Als u een gegevensstroom wilt maken, moet u al een geldige basis-verbindings-id met een bron voor cloudopslag hebben. Als u dit identiteitskaart niet hebt, dan zie het [ overzicht van bronnen ](../../../home.md#cloud-storage) voor een lijst van de bronnen van de wolkenopslag die u een basisverbinding kunt tot stand brengen met.

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde raamwerk waarmee Experience Platform gegevens over de ervaring van klanten organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ de ontwikkelaarsgids van de Registratie van het Schema ](../../../../xdm/api/getting-started.md): Omvat belangrijke informatie die u moet kennen om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het recordsysteem voor gegevenslocatie en -lijn in Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): met de API voor batchverwerking kunt u gegevens als batchbestanden in Experience Platform invoeren.
- [ Sandboxes ](../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../landing/api-guide.md).

## Een bronverbinding maken {#source}

U kunt een bronverbinding maken door een POST-aanvraag in te dienen bij het `sourceConnections` eindpunt van [!DNL Flow Service] API en tegelijkertijd uw basis-verbindings-id, het pad naar het bronbestand dat u wilt invoeren en de bijbehorende verbindingsspecificatie-id van uw bron op te geven.

Wanneer u een bronverbinding maakt, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor bestandsgebaseerde bronnen:

| Gegevensindeling | Enumwaarde |
| ----------- | ---------- |
| Gescheiden | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Stel de waarde in op `tabular` voor alle op tabellen gebaseerde bronnen.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file",
          "cdcEnabled": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `baseConnectionId` | De basis verbindings-id van de bron voor cloudopslag. |
| `data.format` | De indeling van de gegevens die u naar Experience Platform wilt verzenden. Ondersteunde waarden zijn: `delimited` , `JSON` en `parquet` . |
| `data.properties` | (Optioneel) Een set eigenschappen die u op uw gegevens kunt toepassen wanneer u een bronverbinding maakt. |
| `data.properties.columnDelimiter` | (Optioneel) Een scheidingsteken voor één tekenkolom dat u kunt opgeven bij het verzamelen van vlakke bestanden. Elke waarde van één teken is een toegestaan kolomscheidingsteken. Indien niet verstrekt, wordt een komma (`,`) gebruikt als standaardwaarde. **Nota**: Het `columnDelimiter` bezit kan slechts worden gebruikt wanneer het opnemen van afgebakende dossiers. |
| `data.properties.encoding` | (Optioneel) Een eigenschap die het coderingstype definieert dat moet worden gebruikt bij het invoeren van gegevens naar Experience Platform. De volgende coderingstypen worden ondersteund: `UTF-8` en `ISO-8859-1` . **Nota**: De `encoding` parameter is slechts beschikbaar wanneer het opnemen van afgebakende Csv- dossiers. Andere bestandstypen worden met de standaardcodering `UTF-8` opgenomen. |
| `data.properties.compressionType` | (Optioneel) Een eigenschap die het gecomprimeerde bestandstype voor inname definieert. De ondersteunde gecomprimeerde bestandstypen zijn: `bzip2` , `gzip` , `deflate` , `zipDeflate` , `tarGzip` en `tar` . **Nota**: Het `compressionType` bezit kan slechts worden gebruikt wanneer het opnemen van afgebakende of JSON- dossiers. |
| `params.path` | Het pad van het bronbestand dat u opent. Deze parameter verwijst naar een afzonderlijk bestand of naar een volledige map.  **Nota**: U kunt een asterisk in plaats van het dossier gebruiken - naam om de opname van een volledige omslag te specificeren. `/acme/summerCampaign/*.csv` voert bijvoorbeeld de gehele `/acme/summerCampaign/` -map in. |
| `params.type` | Het bestandstype van het brongegevensbestand dat u opgeeft. Gebruik het type `file` om een afzonderlijk bestand in te voeren en gebruik het type `folder` om een volledige map in te voeren. |
| `params.cdcEnabled` | Een booleaanse waarde die aangeeft of het vastleggen van de wijzigingshistorie is ingeschakeld. Bij gebruik met relationele schema&#39;s, baseert de vangst van veranderingsgegevens zich op de `_change_request_type` controlekolom (`u` — upsert, `d` — schrapping), die tijdens opneming maar niet opgeslagen in het doelschema wordt geëvalueerd. Deze eigenschap wordt ondersteund door de volgende bronnen voor cloudopslag: <ul><li>[!DNL Azure Blob]</li><li>[!DNL Data Landing Zone]</li><li>[!DNL Google Cloud Storage]</li><li>[!DNL SFTP]</li></ul>Voor een overzicht van dit vermogen, zie het [ overzicht van Data Mirror ](../../../../xdm/data-mirror/overview.md). Voor implementatiedetails, lees de gids bij het gebruiken van [ veranderingsgegevens vangen in bronnen ](../change-data-capture.md) en [ relationele schema&#39;s technische verwijzing ](../../../../xdm/schema/relational.md). |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan uw specifieke bron voor cloudopslag. Zie [ bijlage ](#appendix) voor een lijst van verbindingsspecificiteit IDs. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Reguliere expressies gebruiken om een specifieke set bestanden voor inname te selecteren {#regex}

U kunt reguliere expressies gebruiken om een bepaalde set bestanden van uw bron naar Experience Platform in te voeren wanneer u een bronverbinding maakt.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

In het onderstaande voorbeeld wordt een reguliere expressie gebruikt in het bestandspad om de opname op te geven van alle CSV-bestanden die `premium` in hun naam hebben.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Een bronverbinding configureren om gegevens recursief in te voeren

Wanneer u een bronverbinding maakt, kunt u de parameter `recursive` gebruiken om gegevens uit diep geneste mappen in te voeren.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

In het onderstaande voorbeeld geeft de parameter `recursive: true` [!DNL Flow Service] de informatie dat alle submappen tijdens het innameproces recursief moeten worden gelezen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Een doel-XDM-schema maken {#target-schema}

Als u de brongegevens in Experience Platform wilt gebruiken, moet u een doelschema maken om de brongegevens naar wens te structureren. Het doelschema wordt dan gebruikt om een dataset van Experience Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een POST- verzoek aan de [ Registratie API van het Schema ](https://www.adobe.io/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](../../../../xdm/api/schemas.md).

## Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een POST- verzoek aan de [ Dienst API van de Catalogus uit te voeren ](https://developer.adobe.com/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](../../../../catalog/api/create-dataset.md).

## Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart verstrekken van verbindingsspecificatie verbonden aan het meer van Gegevens. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het meer van Gegevens. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

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
| `data.schema.id` | The `$id` of the target XDM schema. |
| `data.schema.version` | De versie van het schema. Deze waarde moet worden ingesteld `application/vnd.adobe.xed-full+json;version=1` , die de laatste secundaire versie van het schema retourneert. |
| `params.dataSetId` | Identiteitskaart van de doeldataset die in de vorige stap wordt geproduceerd. **Nota**: U moet een geldige datasetidentiteitskaart verstrekken wanneer het creëren van een doelverbinding. Een ongeldige dataset ID zal in een fout resulteren. |
| `connectionSpec.id` | De verbinding-specificatie-id die wordt gebruikt om verbinding te maken met het datumpeer. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt.

Om een mappingsreeks tot stand te brengen, doe een POST- verzoek aan het `mappingSets` eindpunt van [[!DNL Data Prep]  API ](https://developer.adobe.com/experience-platform-apis/references/data-prep/) terwijl het verstrekken van uw doelXDM schema `$id` en de details van de mappingsreeksen u wilt tot stand brengen.

>[!TIP]
>
>U kunt complexe gegevenstypen, zoals arrays, toewijzen in JSON-bestanden met behulp van een bronconnector voor cloudopslag.

**API formaat**

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

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

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

Een dataflow is verantwoordelijk voor het verzamelen van gegevens uit bronnen, en het brengen van deze naar Experience Platform. Als u een gegevensstroom wilt maken, moet u eerst de gegevensstroomspecificaties ophalen die verantwoordelijk zijn voor het verzamelen van gegevens voor cloudopslag.

**API formaat**

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

>[!NOTE]
>
>De JSON-responslading hieronder is verborgen voor bondigheid. Selecteer &quot;payload&quot; om de antwoordlading weer te geven.

+++ nuttige lading weergeven

**Reactie**

Een succesvolle reactie retourneert de details van de gegevensstroomspecificatie die verantwoordelijk zijn voor het plaatsen van gegevens van uw bron naar Experience Platform. De reactie bevat de unieke flowspecificatie `id` die is vereist om een nieuwe gegevensstroom te maken.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
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
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
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
    }
  },
  "transformationSpec": [
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
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Een gegevensstroom maken

De laatste stap op weg naar het verzamelen van gegevens voor cloudopslag is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

- [Source-verbinding-id](#source)
- [Doel-verbindings-id](#target)
- [Toewijzing-id](#mapping)
- [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

>[!NOTE]
>
>Voor batch-opname, selecteert elke volgende dataflow dossiers die van uw bron worden opgenomen die op hun **worden gebaseerd laatste gewijzigde** timestamp. Dit betekent dat de partijgegevens uitgezochte dossiers van de bron die of nieuw zijn of sinds de laatste dataflow looppas zijn gewijzigd.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day` of `week` . De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde worden ingesteld op gelijk aan of groter dan `15` .

>[!IMPORTANT]
>
>Het wordt sterk geadviseerd om uw dataflow voor eenmalige opname te plannen wanneer het gebruiken van de [ schakelaar van FTP ](../../../connectors/cloud-storage/ftp.md).

**API formaat**

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
        "name": "Cloud Storage flow to Experience Platform",
        "description": "Cloud Storage flow to Experience Platform",
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
| `flowSpec.id` | De [ identiteitskaart van de stroomspecificatie ](#specs) die in de vorige stap wordt teruggewonnen. |
| `sourceConnectionIds` | [ bron verbindingsidentiteitskaart ](#source) die in een vroegere stap wordt teruggewonnen. |
| `targetConnectionIds` | De [ identiteitskaart van de doelverbinding ](#target-connection) die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt teruggewonnen. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day` of `week` . |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. De minimaal toegestane intervalwaarde voor elke frequentie is als volgt:<ul><li>**Eenmaal**: n/a</li><li>**Minuut**: 15</li><li>**Uur**: 1</li><li>**Dag**: 1</li><li>**Week**: 1</li></ul> |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor meer informatie over hoe te om dataflows te controleren, zie het leerprogramma op [ controledataflows in API ](../monitor.md)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronaansluiting gemaakt om gegevens van uw cloudopslag op een geplande basis te verzamelen. Binnenkomende gegevens kunnen nu worden gebruikt door downstream Experience Platform-services, zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace] . Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van Data Science Workspace](../../../../data-science-workspace/home.md)

## Bijlage {#appendix}

In de volgende sectie worden de verschillende connectors voor bronnen voor cloudopslag en de bijbehorende verbindingsspecificaties weergegeven.

### Verbindingsspecificatie

| Naam van connector | Verbindingsspecificatie |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Klodder) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Event Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
