---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevens over marketingautomatisering verzamelen via bronconnectors en API's
topic: overview
translation-type: tm+mt
source-git-commit: 2f7961a4ca0bc0fec2ed1f50f5101e4dd734a282

---


# Gegevens over marketingautomatisering verzamelen via bronconnectors en API&#39;s

Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een marketingautomatiseringssysteem en het inbrengen van gegevens naar Platform via bronconnectors en API&#39;s.

## Aan de slag

Deze zelfstudie vereist dat u informatie hebt over het bestand dat u naar Platform wilt verzenden, inclusief het pad en de structuur van het bestand. Als u deze informatie niet hebt, raadpleegt u de zelfstudie over het [verkennen van een marketingautomatiseringstoepassing met behulp van de Flow Service API](../../api/create/marketing-automation/hubspot.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht in de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [Catalogusservice](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen het Platform van de Ervaring.
* [Inname](../../../../ingestion/batch-ingestion/overview.md)in batch: Met de API voor inname van batch kunt u gegevens als batchbestanden in het Experience Platform opnemen.
* [Sandboxen](../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met een systeem van de marketing automatisering te verbinden gebruikend de Dienst API van de Stroom.

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
        "name": "Marketing automation source connection",
        "baseConnectionId": "2fce94c1-9a93-4971-8e94-c19a93097129",
        "description": "Marketing automation source connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/80a6e931bd5e00190b72daafb4e1e4f7913a114808be9ac0",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
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
| `baseConnectionId` | De verbinding-id van uw marketingautomatiseringstoepassing |
| `data.schema.id` | Het `$id` ad-hoc XDM-schema. |
| `params.path` | Het pad van het bronbestand. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw marketingautomatiseringstoepassing. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Sla deze waarde op zoals deze in latere stappen is vereist voor het maken van een doelverbinding.

```json
{
    "id": "c315c0ae-a339-44c4-95c0-aea33964c420",
    "etag": "\"67010af9-0000-0200-0000-5e9795c40000\""
}
```

## Een doel-XDM-schema maken {#target}

In eerdere stappen werd een ad-hoc XDM-schema gemaakt om de brongegevens te structureren. Voor de brongegevens die in Platform worden gebruikt, moet een doelschema ook worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doel-XDM-schema kan worden gemaakt door een POST-verzoek uit te voeren naar de [schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Als u de gebruikersinterface in het Platform van de Ervaring liever zou gebruiken, verstrekt de zelfstudie [van de Redacteur van het](../../../../xdm/tutorials/create-schema-ui.md) Schema geleidelijke instructies voor het uitvoeren van gelijkaardige acties in de Redacteur van het Schema.

**API-indeling**

```https
POST /schemaregistry/tenant/schemas
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
        "title": "Target schema for marketing automation",
        "description": "Target schema for marketing automation",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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

Een geslaagde reactie retourneert details van het nieuwe schema, inclusief de unieke id (`$id`). Sla deze id op zoals deze in latere stappen is vereist om een doeldataset, toewijzing en gegevensstroom te maken.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:altId": "_{TENANT_ID}.schemas.63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for marketing automation",
    "type": "object",
    "description": "Target schema for marketing automation",
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
        "repo:createdDate": 1586992941717,
        "repo:lastModifiedDate": 1586992941717,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CREATED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{CREATED_USER_ID}",
        "eTag": "d11e63a422b84a843cdd58d0ba8a16ce0a2068eda49ab380c1605ddd10efdf23",
        "meta:globalLibVersion": "1.9.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een doelgegevensset maken

Een doeldataset kan worden tot stand gebracht door een POST- verzoek aan de Dienst API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogus uit te voeren, die identiteitskaart van het doelschema binnen de lading verstrekken.

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
        "name": "Target dataset for marketing automation",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
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
    "@/dataSets/5e9797ac6d771118ad8356db"
]
```

## Een databaseverbinding maken

Om een doelverbinding tot stand te brengen en externe gegevens in Platform in te voeren, moet een datasetbasisverbinding eerst worden verworven.

Om een verbinding van de datasetbasis tot stand te brengen, volg de stappen die in het [gegevensbestand van de basisverbinding](../create-dataset-base-connection.md)worden geschetst.

Ga na de stappen die in de ontwikkelaarsgids worden geschetst verder tot u een verbinding van de datasetbasis hebt gecreeerd. Haal de unieke id (`$id`) van de basisverbinding op en sla deze op. Ga vervolgens verder met de volgende stap van deze zelfstudie.

## Een doelverbinding maken

U hebt nu de unieke herkenningstekens voor een gegevenssetbasisverbinding, een doelschema, en een doeldataset. Gebruikend deze herkenningstekens, kunt u een doelverbinding tot stand brengen gebruikend de Dienst API van de Stroom om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

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
        "baseConnectionId": "44b1c1e43-a5ee-4d86-9c1e-43a5eebd8601",
        "name": "Target Connection for marketing automation",
        "description": "Target Connection for marketing automation",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e9797ac6d771118ad8356db
        },
            "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De id van de gegevenssetbasisverbinding. |
| `data.schema.id` | Het `$id` doel-XDM-schema. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | De id van de verbindingsspecificatie voor uw marketingautomatisering. |

>[!IMPORTANT] Wanneer het creëren van een doelverbinding, zorg ervoor om de waarde van de gegevenssetbasisverbinding voor de basisverbinding `id` in tegenstelling tot verbindingsidentiteitskaart van uw derde bronschakelaar te gebruiken.

```json
{
    "id": "fd82157f-0eea-4c81-8215-7f0eeaec8139",
    "etag": "\"5301d5ac-0000-0200-0000-5e97981a0000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een POST-verzoek uit te voeren naar de Conversion Service API met gegevenstoewijzingen die zijn gedefinieerd in de payload van de aanvraag.

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
        "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "Properties_Lastname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "repositoryCreatedBy",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Portal_Id",
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

Een geslaagde reactie retourneert details van de nieuwe toewijzing, inclusief de unieke id (`id`). Sla deze waarde op zoals u deze later nodig hebt om een gegevensstroom te maken.

```json
{
    "id": "280a3cc950894945bf815c5fc60f3803",
    "version": 0,
    "createdDate": 1586993661034,
    "modifiedDate": 1586993661034,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Specificaties voor gegevensstroom opzoeken {#specs}

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

Een succesvolle reactie keert de details van de gegevensstroomspecificatie terug die voor het brengen van gegevens van uw systeem van de marketing automatisering in Platform verantwoordelijk is. Sla de waarde van het `id` veld op zoals vereist in de volgende stap om een nieuwe gegevensstroom te maken.

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

De laatste stap in de richting van het verzamelen van gegevens over marketingautomatisering is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source)
* [Doelverbinding-id](#target)
* [Toewijzing-id](#mapping)
* [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

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
        "name": "Dataflow for marketing automation",
        "description": "Dataflow for marketing automation",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c315c0ae-a339-44c4-95c0-aea33964c420"
        ],
        "targetConnectionIds": [
            "fd82157f-0eea-4c81-8215-7f0eeaec8139"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "280a3cc950894945bf815c5fc60f3803",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "<START TIME>",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | Dataflow-specificatie-id. |
| `sourceConnectionIds` | Bronverbinding-id. |
| `targetConnectionIds` | Doel-verbindings-id. |
| `transformations.params.mappingId` | Toewijzings-id. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om gegevens van een systeem van de marketing automatisering op een geplande basis te verzamelen. De inkomende gegevens kunnen nu door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant in real time en de Werkruimte van de Wetenschap van Gegevens worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)