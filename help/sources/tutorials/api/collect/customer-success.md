---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevens verzamelen van een systeem met succesmeldingen van klanten via bronconnectors en API's
topic: overview
translation-type: tm+mt
source-git-commit: c216e321fd913773578107df027d953f10d99a36

---


# Gegevens verzamelen van een systeem met succesmeldingen van klanten via bronconnectors en API&#39;s

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een CS-systeem (Customer Success) en het opnemen ervan in Platform via bronconnectors en API&#39;s.

## Aan de slag

Voor deze zelfstudie hebt u toegang tot een CS-systeem van derden via een geldige basisverbinding en informatie over het bestand dat u in Platform wilt plaatsen, inclusief het pad en de structuur van het bestand. Als u deze informatie niet hebt, raadpleegt u de zelfstudie over het [verkennen van een database of een NoSQL-systeem met behulp van de Flow Service API](../explore/customer-success.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht in de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [Catalogusservice](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen het Platform van de Ervaring.
* [Inname](../../../../ingestion/batch-ingestion/overview.md)in batch: Met de API voor inname van batch kunt u gegevens als batchbestanden in het Experience Platform opnemen.
* [Sandboxen](../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met een CS-systeem tot stand te brengen met behulp van de Flow Service API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief de bronnen die bij Flow Service horen, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Een ad-hoc XDM-klasse en -schema maken

Als u externe gegevens via bronconnectors wilt overbrengen naar Platform, moet u een ad-hoc XDM-klasse en -schema maken voor de onbewerkte brongegevens.

Als u een ad-hocklasse en -schema wilt maken, volgt u de stappen in de zelfstudie over het [ad-hocschema](../../../../xdm/tutorials/ad-hoc.md). Wanneer u een ad-hocklasse maakt, moeten alle velden in de brongegevens worden beschreven in de aanvraaginstantie.

Ga door met het volgen van de stappen die in de ontwikkelaarsgids worden beschreven tot u een ad-hocschema hebt gecreeerd. Haal de unieke id (`$id`) van het ad-hocschema op en sla deze op. Ga vervolgens verder met de volgende stap van deze zelfstudie.

## Een bronverbinding maken {#source}

Als een ad-hoc XDM-schema is gemaakt, kan nu een bronverbinding worden gemaakt met een POST-aanvraag voor de Flow Service API. Een bronverbinding bestaat uit een basisverbinding, een brongegevensbestand, en een verwijzing naar het schema dat de brongegevens beschrijft.

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
        "name": "Source connection for CS",
        "baseConnectionId": "60a5c8b9-3c30-43ba-a5c8-b93c3093ba66",
        "description": "Source Connection for CS to ingest Account",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/classes/51dd6dce662f8aebe4353c74bbb49c77cb3cbcd6c6b29021",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Account"
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De id van een basisverbinding voor een CS-systeem |
| `data.schema.id` | Het `$id` ad-hoc XDM-schema. |
| `params.path` | Het pad van het bronbestand. |
| `connectionSpec.id` | De id van de verbindingsspecificatie voor een CS-systeem. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is vereist in latere stappen om een doelverbinding te maken.

```json
{
    "id": "01b7cbea-cf18-4552-b7cb-eacf18055294",
    "etag": "\"2103ac94-0000-0200-0000-5e543ad70000\""
}
```

## Een doel-XDM-schema maken {#target}

In eerdere stappen werd een ad-hoc XDM-schema gemaakt om de brongegevens te structureren. Voor de brongegevens die in Platform worden gebruikt, moet een doelschema ook worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn. Dit doel-XDM-schema breidt ook de klasse Individueel profiel XDM uit.

Een doel-XDM-schema kan worden gemaakt door een POST-verzoek uit te voeren naar de [schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

Als u de gebruikersinterface in het Platform van de Ervaring liever zou gebruiken, verstrekt de zelfstudie [van de Redacteur van het](../../../../xdm/tutorials/create-schema-ui.md) Schema geleidelijke instructies voor het uitvoeren van gelijkaardige acties in de Redacteur van het Schema.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

Met de volgende voorbeeldaanvraag wordt een XDM-schema gemaakt dat de klasse Individueel profiel XDM uitbreidt.

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
        "title": "Target schema for CS",
        "description": "Target schema for CS",
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
    }'
```

**Antwoord**

Een geslaagde reactie retourneert details van het nieuwe schema, inclusief de unieke id (`$id`). Deze id wordt vereist in recentere stappen om een doeldataset, afbeelding, en dataflow tot stand te brengen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
    "meta:altId": "_{TENANT_ID}.schemas.deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for CS",
    "type": "object",
    "description": "Target schema for CS",
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
        "repo:createdDate": 1582578764554,
        "repo:lastModifiedDate": 1582578764554,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "213e4bf7cbac74e3a9e6f988da321e2f7353acacd9ea651a5652bd49b28b8d2a"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een doelgegevensset maken

Een doeldataset kan worden tot stand gebracht door een POST- verzoek aan de Dienst API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogus uit te voeren, die identiteitskaart van het doelschema binnen de lading verstrekken.

**API-indeling**

```http
POST /dataSets
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
        "name": "Target Dataset for CS",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef.id` | Het `$id` doel-XDM-schema. |

**Antwoord**

Een succesvolle reactie keert een serie terug die identiteitskaart van de pas gecreëerde dataset in het formaat bevat `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. Sla identiteitskaart van de doeldataset zoals het in recentere stappen wordt vereist om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5e543e8a60b15218ad44b95f"
]
```

## Een databaseverbinding maken

Om externe gegevens in Platform in te voeren, moet eerst een verbinding van de datasetbasis van het Platform van de Ervaring worden verworven.

Om een verbinding van de datasetbasis tot stand te brengen, volg de stappen die in het [gegevensbestand van de basisverbinding](../create-dataset-base-connection.md)worden geschetst.

Ga na de stappen die in de ontwikkelaarsgids worden geschetst verder tot u een verbinding van de datasetbasis hebt gecreeerd. Haal de unieke id (`$id`) op en sla deze op en ga verder met het gebruik ervan als basis-verbindings-id in de volgende stap om een doelverbinding te maken.

## Een doelverbinding maken

U hebt nu met u de unieke herkenningstekens voor een gegevenssetbasisverbinding, een doelschema, en een doeldataset. U kunt nu een doelverbinding tot stand brengen gebruikend de Dienst API van de Stroom om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```http
POST /targetConnections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for CS",
        "description": "Target Connection for CS",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
            "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De id van de gegevenssetbasisverbinding. |
| `data.schema.id` | Het `$id` doel-XDM-schema. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | De id van de verbindingsspecificatie voor het successysteem van uw klant. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe doelverbinding. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "5ebaf0b3-66dc-46bf-baf0-b366dc76bfd5",
    "etag": "\"5d02211d-0000-0200-0000-5e543f0f0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een POST-verzoek uit te voeren naar de Conversion Service API met gegevenstoewijzingen die zijn gedefinieerd in de payload van de aanvraag.

**API-indeling**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `xdmSchema` | Het `$id` doel-XDM-schema. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing, inclusief de unieke id (`id`). Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/efea012ad5deefcdf51afd23ceb3583f",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## Specificaties voor gegevensstroom opzoeken {#specs}

Een gegevensstroom is verantwoordelijk voor het verzamelen van gegevens uit bronnen en het brengen van hen in Platform. Om een gegevensstroom tot stand te brengen, moet u eerst de dataflow specificaties verkrijgen door een GET verzoek aan de Dienst API van de Stroom uit te voeren. Dataflow-specificaties zijn verantwoordelijk voor het verzamelen van gegevens van een externe database of een NoSQL-systeem.

**API-indeling**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de dataflow specificatie terug die voor het brengen van gegevens van uw systeem CS in Platform verantwoordelijk is. Deze id is vereist in de volgende stap om een nieuwe gegevensstroom te maken.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
            }
        }
    ]
}
```

## Een gegevensstroom maken

De laatste stap in de richting van het verzamelen van gegevens is het maken van een gegevensstroom. Op dit punt moeten de volgende vereiste waarden worden voorbereid:

* [Bronverbinding-id](#source)
* [Doelverbinding-id](#target)
* [Toewijzing-id](#mapping)
* [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

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
        "name": "Dataflow between database or NoSQL Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "01b7cbea-cf18-4552-b7cb-eacf18055294"
        ],
        "targetConnectionIds": [
            "5ebaf0b3-66dc-46bf-baf0-b366dc76bfd5"
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
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

**Antwoord**

Een geslaagde reactie retourneert de id `id` van de nieuwe gegevensstroom.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om gegevens van een systeem van CS op een geplande basis te verzamelen. De inkomende gegevens kunnen nu door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant in real time en de Werkruimte van de Wetenschap van Gegevens worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)