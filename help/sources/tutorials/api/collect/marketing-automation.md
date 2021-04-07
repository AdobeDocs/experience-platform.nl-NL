---
keywords: Experience Platform;home;populaire onderwerpen;marketingautomatiseringssysteem;Gegevens over marketingautomatisering verzamelen
solution: Experience Platform
title: Gegevens voor marketingautomatisering verzamelen met behulp van bronconnectors en API's
topic: overzicht
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een marketingautomatiseringssysteem en het overbrengen van gegevens naar Adobe Experience Platform met behulp van bronconnectors en API's.
exl-id: f3754bd0-ed31-4bf2-8f97-975bf6a9b076
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 0%

---

# Gegevens over marketingautomatisering verzamelen met bronconnectors en API&#39;s

In deze zelfstudie worden de stappen beschreven voor het ophalen van gegevens van een extern systeem voor marketingautomatisering en het opnemen ervan in het Platform via bronconnectors en de [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

## Aan de slag

Deze zelfstudie vereist dat u toegang hebt tot een systeem voor marketingautomatisering van derden via een geldige verbinding en informatie over het bestand dat u in het Platform wilt plaatsen, inclusief het pad en de structuur van het bestand. Als u deze informatie niet hebt, raadpleegt u de zelfstudie over [het verkennen van een systeem voor marketingautomatisering van derden met behulp van de Flow Service API](../explore/marketing-automation.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../../xdm/api/getting-started.md) voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Met de API voor batchverwerking kunt u gegevens als batchbestanden in het Experience Platform invoeren.
* [Sandboxen](../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met een marketingautomatiseringssysteem met de [!DNL Flow Service]-API tot stand te brengen.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van de Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in Experience Platform, inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

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

```https
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
        "name": "HubSpot source connection",
        "baseConnectionId": "c6d4ee17-6752-4e83-94ee-1767522e83fa",
        "description": "HubSpot source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De unieke verbinding-id van het externe marketingautomatiseringssysteem dat u benadert. |
| `params.path` | Het pad van het bronbestand dat u opent. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw marketingautomatiseringssysteem. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Sla deze waarde op zoals deze in latere stappen is vereist voor het maken van een doelverbinding.

```json
{
    "id": "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf",
    "etag": "\"5f00fba7-0000-0200-0000-5ed560520000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van de Platform tot stand te brengen waarin de brongegevens bevat zijn. Dit doel-XDM-schema breidt ook de klasse XDM [!DNL Individual Profile] uit.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan [Registratie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van het Schema uit te voeren.

**API-indeling**

```https
POST /schemaregistry/tenant/schemas
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
        "title": "HubSpot target XDM schema",
        "description": "HubSpot target XDM schema",
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

Een succesvolle reactie keert details van het pas gecreëerde schema met inbegrip van zijn uniek herkenningsteken (`$id`) terug. Sla deze id op zoals deze in latere stappen is vereist om een doeldataset, toewijzing en gegevensstroom te maken.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
    "meta:altId": "_{TENANT_ID}.schemas.da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "HubSpot target XDM schema",
    "type": "object",
    "description": "HubSpot target XDM schema",
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
        "repo:createdDate": 1591042937856,
        "repo:lastModifiedDate": 1591042937856,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "3f205600107156ffc394bef428e92cbe25b2faa34e15dd916c0d8bb58d9b7dd3",
        "meta:globalLibVersion": "1.10.4.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID"
}
```

## Een doelgegevensset maken

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan [de Dienst API van de Catalogus ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) uit te voeren, die identiteitskaart van het doelschema binnen de nuttige lading verstrekken.

**API-indeling**

```https
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
        "name": "HubSpot target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef.id` | De `$id` van het doel-XDM-schema. |
| `schemaRef.contentType` | De versie van het schema. Deze waarde moet `application/vnd.adobe.xed-full-notext+json;version=1` worden geplaatst, die de recentste minder belangrijke versie van het schema terugkeert. |

**Antwoord**

Een geslaagde reactie retourneert een array met de id van de nieuwe dataset in de notatie `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. Sla identiteitskaart van de doeldataset zoals het in recentere stappen wordt vereist om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5ed5639d798a22191b6987b2"
]
```

## Doelverbinding {#target-connection} maken

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart verstrekken van verbindingsspecificatie verbonden aan het meer van Gegevens. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan gegevens meer. Gebruikend [!DNL Flow Service] API, kunt u een doelverbinding tot stand brengen door deze herkenningstekens samen met de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```https
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
        "name": "HubSpot target connection",
        "description": "HubSpot target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5ed5639d798a22191b6987b2"
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
| `data.schema.version` | De versie van het schema. Deze waarde moet `application/vnd.adobe.xed-full+json;version=1` worden geplaatst, die de recentste minder belangrijke versie van het schema terugkeert. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | De verbindingsspecificatie-id die wordt gebruikt om verbinding te maken met het Data Lake. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

```json
{
    "id": "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65",
    "etag": "\"dd00a1a2-0000-0200-0000-5ed564850000\""
}
```

## Een toewijzing {#mapping} maken

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een verzoek van de POST aan [!DNL Conversion Service] API met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

**API-indeling**

```https
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Vid",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "Added_At",
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

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Sla deze waarde op zoals u deze later nodig hebt om een gegevensstroom te maken.

```json
{
    "id": "500a9b747fcf4908a21917d49bd61780",
    "version": 0,
    "createdDate": 1591043336298,
    "modifiedDate": 1591043336298,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Gegevensstroomspecificaties opzoeken {#specs}

Een dataflow is verantwoordelijk voor het verzamelen van gegevens uit bronnen, en het brengen van hen in Platform. Om een gegevensstroom tot stand te brengen, moet u eerst de dataflow specificaties verkrijgen die voor het verzamelen van de gegevens van de marketing automatisering verantwoordelijk zijn.

**API-indeling**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de dataflow specificatie verantwoordelijk voor het brengen van gegevens van uw bron in Platform terug. De reactie bevat de unieke flowspecificatie `id` die is vereist om een nieuwe gegevensstroom te maken.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
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
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
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
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
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

De laatste stap in de richting van het verzamelen van gegevens over marketingautomatisering is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source)
* [Doelverbinding-id](#target)
* [Toewijzing-id](#mapping)
* [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day` of `week`. De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde worden ingesteld op gelijk aan of groter dan `15`.

**API-indeling**

```https
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
        "name": "HubSpot dataflow",
        "description": "collecting Hubspot.Contacts",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf"
        ],
        "targetConnectionIds": [
            "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "500a9b747fcf4908a21917d49bd61780",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1591043454",
            "frequency":"once",
            "interval":"15"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `flowSpec.id` | De [flow specificatie-id](#specs) wordt opgehaald in de vorige stap. |
| `sourceConnectionIds` | De [bron verbindings ID](#source) die in een vroegere stap wordt teruggewonnen. |
| `targetConnectionIds` | De [doel verbindings ID](#target-connection) die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | De [toewijzingsid](#mapping) is in een eerdere stap opgehaald. |
| `transformations.params.deltaColum` | De opgegeven kolom die wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. De ondersteunde datumnotatie voor `deltaColumn` is `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | De toewijzing-id die aan uw database is gekoppeld. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day` of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

**Antwoord**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Raadpleeg de zelfstudie over [dataflows in de API controleren ](../monitor.md) voor meer informatie over het controleren van gegevensstromen

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om gegevens van een systeem van de marketing automatisering op een geplande basis te verzamelen. Binnenkomende gegevens kunnen nu worden gebruikt door downstreamservices voor Platforms zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)
