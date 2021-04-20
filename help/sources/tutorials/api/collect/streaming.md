---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslaggegevens;streaming gegevens;streaming
solution: Experience Platform
title: Streaming gegevens verzamelen met bronconnectors en API's
topic: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het ophalen van streaminggegevens en het naar Platform brengen van deze gegevens via bronconnectors en API's.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# Streaming gegevens verzamelen met bronconnectors en API&#39;s

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een streamingbronaansluiting en het overbrengen van deze gegevens naar [!DNL Experience Platform] met de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze zelfstudie vereist dat u een geldige verbinding-id hebt voor een streamingconnector. Als u deze informatie niet hebt, raadpleegt u de volgende zelfstudies over het maken van een streamingbronverbinding voordat u deze zelfstudie probeert:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../create/streaming/http.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Handleiding](../../../../xdm/api/getting-started.md) voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen  [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): Streaming opname voor  [!DNL Platform] biedt gebruikers een methode om gegevens van client- en serverapparaten  [!DNL Experience Platform] in real-time te verzenden.
- [Sandboxen](../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om streaming gegevens met de [!DNL Flow Service]-API te kunnen verzamelen.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

- `Content-Type: application/json`

## Een bronverbinding maken {#source}

U kunt een bronverbinding tot stand brengen door een verzoek van de POST aan [!DNL Flow Service] API te doen. Een bronverbinding bestaat uit een verbinding-id, een pad naar het brongegevensbestand en een verbindingsspecificatie-id.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende enum waarden voor op dossier-gebaseerde schakelaars:

| Gegevensindeling | Enumwaarde |
| ----------- | ---------- |
| Gescheiden | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Voor alle op lijst-gebaseerde schakelaars, plaats de waarde aan `tabular`.

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `providerId` | De provider-id van de streamingconnector. |
| `connectionId` | De unieke verbindings-id van de streamingconnector. |
| `connectionSpec.id` | De verbindingsspecificatie-id die aan uw specifieke streamingconnector is gekoppeld. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## URL van streamingeindpunt ophalen {#get-endpoint}

Wanneer de bronverbinding is gemaakt, kunt u nu de URL van het streamingeindpunt ophalen.

**API-indeling**

```http
GET /flowservice/sourceConnections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` waarde van sourceConnections u eerder creeerde. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/sourceConnections/e96d6135-4b50-446e-922c-6dd66672b6b2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de waarde `inletUrl`.

```json
{
    "items": [
        {
            "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
            "createdAt": 1617743929826,
            "updatedAt": 1617743930363,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG}",
            "name": "Test source connector for streaming data",
            "description": "Test source connector for streaming data",
            "baseConnectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
            "state": "enabled",
            "data": {
                "format": "delimited",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "params": {
                "sourceId": "Streaming raw data",
                "inletUrl": "https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "inletId": "2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "dataType": "raw",
                "name": "hgtest"
            },
            "version": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "etag": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
                    "connectionSpec": {
                        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                        "version": "1.0"
                    }
                }
            }
        }
    ]
}
```


## Een doel-XDM-schema maken {#target-schema}

Als u de brongegevens wilt gebruiken in [!DNL Platform], moet u een doelschema maken om de brongegevens te structureren op basis van uw behoeften. Het doelschema wordt dan gebruikt om een [!DNL Platform] dataset tot stand te brengen waarin de brongegevens bevat zijn. Dit doel-XDM-schema breidt ook de klasse XDM [!DNL Individual Profile] uit.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan [Registratie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van het Schema uit te voeren.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

In het volgende voorbeeldverzoek wordt een XDM-schema gemaakt dat de klasse XDM [!DNL Individual Profile] uitbreidt.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

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
    "imsOrg": "{IMS_ORG}",
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

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan [de Dienst API van de Catalogus ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) uit te voeren, die identiteitskaart van het doelschema binnen de nuttige lading verstrekken.

**API-indeling**

```http
POST /catalog/dataSets
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
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
        },
        "name": "Test streaming dataset"
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `schemaRef.id` | De id van het doel-XDM-schema. |
| `schemaRef.contentType` | De versie van het schema. Deze waarde moet `application/vnd.adobe.xed-full-notext+json;version=1` worden geplaatst, die de recentste minder belangrijke versie van het schema terugkeert. |

**Antwoord**

Een geslaagde reactie retourneert een array met de id van de nieuwe dataset in de notatie `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. De doel dataset identiteitskaart wordt vereist in recentere stappen om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Doelverbinding {#target-connection} maken

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste specificatie-id voor de verbinding opgeven die is gekoppeld aan het datumpeer. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan gegevens meer. Gebruikend deze herkenningstekens, kunt u een doelverbinding tot stand brengen gebruikend [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | De verbindingsspecificatie-id die wordt gebruikt om verbinding te maken met het Data Lake. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Een toewijzing {#mapping} maken

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een verzoek van de POST aan de Dienst van de Omzetting met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `xdmSchema` | De `$id` van het doel-XDM-schema. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is later vereist om een gegevensstroom te maken.

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

## Gegevensstroomspecificaties opzoeken {#specs}

Een gegevensstroom is verantwoordelijk voor het verzamelen van gegevens uit bronnen en het brengen van hen in [!DNL Platform]. Om een gegevensstroom tot stand te brengen, moet u eerst de dataflow specificaties verkrijgen door een verzoek van de GET aan [!DNL Flow Service] API uit te voeren. Dataflow-specificaties zijn verantwoordelijk voor het verzamelen van gegevens van een streamingconnector.
**API-indeling**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de dataflow specificatie terug die voor het brengen van gegevens van uw het stromen schakelaar in [!DNL Platform] verantwoordelijk is. Deze id is vereist in de volgende stap om een nieuwe gegevensstroom te maken.

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
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
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
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
        }
    ]
}
```

## Een gegevensstroom maken

De laatste stap op weg naar het verzamelen van streaminggegevens is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

- [Bronverbinding-id](#source)
- [Doelverbinding-id](#target)
- [Toewijzing-id](#mapping)
- [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
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
| `flowSpec.id` | De [flow specificatie-id](#specs) wordt opgehaald in de vorige stap. |
| `sourceConnectionIds` | De [bron verbindings ID](#source) die in een vroegere stap wordt teruggewonnen. |
| `targetConnectionIds` | De [doel verbindings ID](#target-connection) die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | De [toewijzingsid](#mapping) is in een eerdere stap opgehaald. |

**Antwoord**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Onbewerkte gegevens plaatsen die {#ingest-data} moeten worden ingevoerd

Nu u uw stroom hebt gecreeerd, kunt u uw JSON bericht naar het het stromen eindpunt verzenden u eerder creeerde.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id`-waarde van de nieuwe streamingverbinding. |

**Verzoek**

Het voorbeeldverzoek neemt onbewerkte gegevens aan het het stromen eindpunt op dat eerder werd gecreeerd.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
          "day": 9
      }
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details van de nieuw opgenomen informatie.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record traceren via verschillende systemen en met foutopsporing. |
| `receivedTimeMs`: Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt voor het verzamelen van streaminggegevens via de streamingconnector. Binnenkomende gegevens kunnen nu worden gebruikt door downstreamservices [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)
