---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslaggegevens;streaming gegevens;streaming
solution: Experience Platform
title: Een gegevensstroom voor streaming maken voor Raw-gegevens met de Flow Service API
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het ophalen van streaminggegevens en het overbrengen van deze gegevens naar het platform met behulp van bronconnectors en API's.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---

# Een streaminggegevensstroom maken voor onbewerkte gegevens met de API [!DNL Flow Service]

Dit leerprogramma behandelt de stappen om ruwe gegevens van een het stromen bronschakelaar terug te winnen en hen te brengen aan Experience Platform gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde framework waarmee Experience Platform gegevens voor klantervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ de ontwikkelaarsgids van de Registratie van het Schema ](../../../../xdm/api/getting-started.md): Omvat belangrijke informatie die u moet kennen om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het recordsysteem voor de gegevenslocatie en -lijn in het Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): De het stromen opname voor Platform verstrekt gebruikers een methode om gegevens van cliënt en server-zijapparaten naar Experience Platform in echt te verzenden - tijd.
- [ Sandboxes ](../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../landing/api-guide.md).

### Een bronverbinding maken {#source}

Deze zelfstudie vereist ook dat u een geldige bron-verbindings-id hebt voor een streamingconnector. Als u deze informatie niet hebt, raadpleegt u de volgende zelfstudies over het maken van een streamingbronverbinding voordat u deze zelfstudie probeert:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn. Dit doel-XDM-schema breidt ook de klasse XDM [!DNL Individual Profile] uit.

Om een doelXDM schema tot stand te brengen, doe een verzoek van de POST aan het `/schemas` eindpunt van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API formaat**

```http
POST /tenant/schemas
```

**Verzoek**

Met de volgende voorbeeldaanvraag wordt een XDM-schema gemaakt dat de klasse XDM [!DNL Individual Profile] uitbreidt.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**Reactie**

Een succesvolle reactie keert details van het pas gecreëerde schema met inbegrip van zijn uniek herkenningsteken (`$id`) terug. Deze id wordt vereist in recentere stappen om een doeldataset, afbeelding, en dataflow tot stand te brengen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een doelgegevensset maken

Met een doel-XDM-schema gemaakt en zijn unieke `$id` kunt u nu een doeldataset maken die uw brongegevens bevat. Om een doeldataset tot stand te brengen, doe een verzoek van de POST aan het `dataSets` eindpunt van de [ Dienst API van de Catalogus ](https://www.adobe.io/experience-platform-apis/references/catalog/), terwijl het verstrekken van identiteitskaart van het doelschema binnen de nuttige lading.

**API formaat**

```http
POST /catalog/dataSets
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de gegevensset die moet worden gemaakt. |
| `schemaRef.id` | De URI `$id` voor het XDM-schema waarop de gegevensset wordt gebaseerd. |
| `schemaRef.contentType` | De versie van het schema. Deze waarde moet worden ingesteld op `application/vnd.adobe.xed-full-notext+json;version=1` , die de laatste secundaire versie van het schema retourneert. Zie de sectie over [ schema versioning ](../../../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie. |

**Reactie**

Een geslaagde reactie retourneert een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"` . De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. De doel dataset identiteitskaart wordt vereist in recentere stappen om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Een doelverbinding maken {#target-connection}

De verbindingen van het doel leiden tot en leiden een bestemmingsverbinding aan Platform of om het even welke plaats waar de overgebrachte gegevens zullen landen. De verbindingen van het doel bevatten informatie betreffende gegevensbestemming, gegevensformaat, en identiteitskaart van de doelverbinding die wordt vereist om een gegevensstroom tot stand te brengen. De de verbindingsinstanties van het doel zijn specifiek voor een huurder en organisatie.

Als u een doelverbinding wilt maken, vraagt u een POST naar het `/targetConnections` -eindpunt van de [!DNL Flow Service] API. Als onderdeel van de aanvraag moet u de gegevensindeling opgeven, de `dataSetId` die in de vorige stap is opgehaald en de vaste id van de verbindingsspecificatie die aan [!DNL Data Lake] is gekoppeld. Deze id is `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

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
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.format` | De opgegeven indeling van de gegevens die u aan het datumpigment toevoegt. |
| `params.dataSetId` | Identiteitskaart van de doeldataset die in de vorige stap wordt geproduceerd. **Nota**: U moet een geldige datasetidentiteitskaart verstrekken wanneer het creëren van een doelverbinding. Een ongeldige dataset ID zal in een fout resulteren. |
| `connectionSpec.id` | De verbinding-specificatie-id die wordt gebruikt om verbinding te maken met het datumpeer. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt.

Om een mappingsreeks tot stand te brengen, doe een verzoek van de POST aan het `mappingSets` eindpunt van [[!DNL Data Prep]  API ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) terwijl het verstrekken van uw doelXDM schema `$id` en de details van de mappingsreeksen u wilt tot stand brengen.

**API formaat**

```http
POST /mappingSets
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `xdmSchema` | The `$id` of the target XDM schema. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Een lijst met gegevensstroomspecificaties ophalen {#specs}

Een gegevensstroom is verantwoordelijk voor het verzamelen van gegevens uit bronnen en het brengen van hen in Platform. Als u een gegevensstroom wilt maken, moet u eerst de dataflow-specificaties verkrijgen door een aanvraag voor GET naar de [!DNL Flow Service] API uit te voeren.

**API formaat**

```http
GET /flowSpecs
```

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van dataflow specificaties terug. De gegevensstroomspecificatie-id die u moet ophalen om een gegevensstroom te maken met behulp van [!DNL Amazon Kinesis] , [!DNL Azure Event Hubs] of [!DNL Google PubSub] , is `d69717ba-71b4-4313-b654-49f9cf126d7a` .

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
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
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## Een gegevensstroom maken

De laatste stap op weg naar het verzamelen van streaminggegevens is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

- [Source-verbinding-id](#source)
- [Doel-verbindings-id](#target)
- [Toewijzing-id](#mapping)
- [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | De [ identiteitskaart van de stroomspecificatie ](#specs) die in de vorige stap wordt teruggewonnen. |
| `sourceConnectionIds` | [ bron verbindingsidentiteitskaart ](#source) die in een vroegere stap wordt teruggewonnen. |
| `targetConnectionIds` | De [ identiteitskaart van de doelverbinding ](#target-connection) die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | [ afbeelding identiteitskaart ](#mapping) die in een vroegere stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Post-gegevens voor inname

Bekijk hieronder de voorbeeldlading voor voorbeelden van ruw of XDM-Volgzaam json die u voor opname kunt verzenden.

>[!NOTE]
>
>U moet een vertraging van minstens ~5 minuten toevoegen tussen het maken van een gegevensstroom en het invoeren van streaming gegevens. Hierdoor kan de gegevensstroom volledig worden ingeschakeld, voordat er gegevens worden ingevoerd.

De volgende voorbeelden zijn van toepassing op alle:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB  Ruwe gegevens ]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB  XDM gegevens ]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt voor het verzamelen van streaminggegevens via de streamingconnector. Binnenkomende gegevens kunnen nu worden gebruikt door downstream-platformservices zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace] . Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van Data Science Workspace](../../../../data-science-workspace/home.md)
