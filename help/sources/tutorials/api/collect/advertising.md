---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Reclamegegevens verzamelen via bronconnectors en API's
topic: overview
translation-type: tm+mt
source-git-commit: 577027e52041d642e03ca5abf5cb8b05c689b9f2
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 0%

---


# Reclamegegevens verzamelen via bronconnectors en API&#39;s

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie worden de stappen beschreven voor het ophalen van gegevens van een externe advertentietoepassing en het doorsturen van deze gegevens naar Platform via bronconnectors en API&#39;s.

## Aan de slag

Deze zelfstudie vereist dat u informatie hebt over het bestand dat u naar Platform wilt verzenden, inclusief het pad en de structuur van het bestand. Als u deze informatie niet hebt, raadpleegt u de zelfstudie over het [verkennen van een advertentietoepassing met behulp van de Flow Service API](../../api/create/advertising/ads.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht in de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [Catalogusservice](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen het Platform van de Ervaring.
* [Inname](../../../../ingestion/batch-ingestion/overview.md)in batch: Met de API voor inname van batch kunt u gegevens als batchbestanden in het Experience Platform opnemen.
* [Sandboxen](../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met een advertentiesysteem tot stand te brengen met behulp van de Flow Service API.

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

Ga door met het volgen van de stappen die in de ontwikkelaarsgids worden beschreven tot u een ad-hocschema hebt gecreeerd. De unieke id (`$id`) van het ad-hocschema is vereist om door te gaan naar de volgende stap van deze zelfstudie.

## Een bronverbinding maken {#source}

Als een ad-hoc XDM-schema is gemaakt, kan nu een bronverbinding worden gemaakt met een POST-aanvraag voor de Flow Service API. Een bronverbinding bestaat uit een basisverbinding, een brongegevensbestand, en een verwijzing naar het schema dat de brongegevens beschrijft.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor op **bestanden gebaseerde connectors**:

| Data.format | Enumwaarde |
| ----------- | ---------- |
| Gescheiden bestanden | `delimited` |
| JSON-bestanden | `json` |
| Parketbestanden | `parquet` |

Voor alle op **lijst-gebaseerde schakelaars** gebruik de enum waarde: `tabular`.

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
        "name": "Advertising source connection",
        "baseConnectionId": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
        "description": "Advertising source connection",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/9056f97e74edfa68ccd811380ed6c108028dcb344168746d",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "v201809.AD_PERFORMANCE_REPORT"
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De unieke verbindings-id van de externe advertentietoepassing waartoe u toegang hebt. |
| `data.schema.id` | Het `$id` ad-hoc XDM-schema. |
| `params.path` | Het pad van het bronbestand. |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan uw specifieke externe advertentietoepassing. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Sla deze waarde op zoals deze in latere stappen is vereist voor het maken van een doelverbinding.

```json
{
    "id": "ca7b8baa-587e-4223-bb8b-aa587e4223e3",
    "etag": "\"5701cdf0-0000-0200-0000-5e9680af0000\""
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
        "title": "Target schema for advertising",
        "description": "Target schema for advertising",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/b9bf50e91f28528e5213c7ed8583018f48970d69040c37dc",
    "meta:altId": "_{TENANT_ID}.schemas.b9bf50e91f28528e5213c7ed8583018f48970d69040c37dc",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for advertising",
    "type": "object",
    "description": "Target schema for advertising",
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
        "repo:createdDate": 1586042956286,
        "repo:lastModifiedDate": 1586042956286,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "952e8912724d7f43cbc1471e3987bc5b6899519c186126b7c50619f2dddf8650"
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
        "name": "Target dataset for advertising",
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
    "@/dataSets/5e9681e389b80418ad4b3df0"
]
```

## Een doelverbinding maken

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste specificatie-id voor de verbinding opgeven die is gekoppeld aan het datumpeer. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan gegevens meer. Gebruikend deze herkenningstekens, kunt u een doelverbinding tot stand brengen gebruikend de Dienst API van de Stroom om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

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
        "name": "Target Connection for advertising",
        "description": "Target Connection for advertising",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b9bf50e91f28528e5213c7ed8583018f48970d69040c37dc",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e9681e389b80418ad4b3df0"
        },
            "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.schema.id` | Het `$id` doel-XDM-schema. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | The fixed connection spec ID to data Lake. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

```json
{
    "id": "41af25df-cd99-4372-af25-dfcd99b37291",
    "etag": "\"4d01178a-0000-0200-0000-5e9683380000\""
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/b9bf50e91f28528e5213c7ed8583018f48970d69040c37dc",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
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
| --- | --- |
| `xdmSchema` | De id van het doel-XDM-schema. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing, inclusief de unieke id (`id`). Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "febec6a6785e45ea9ed594422cc483d7",
    "version": 0,
    "createdDate": 1589398562232,
    "modifiedDate": 1589398562232,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Specificaties voor gegevensstroom opzoeken {#specs}

Een dataflow is verantwoordelijk voor het verzamelen van gegevens uit bronnen, en het brengen van hen in Platform. Als u een gegevensstroom wilt maken, moet u eerst de gegevensstroomspecificaties verkrijgen die verantwoordelijk zijn voor het verzamelen van advertentiegegevens.

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

Een succesvol antwoord keert de details van de gegevensstroomspecificatie terug die voor het brengen van gegevens van uw reclamesysteem in Platform verantwoordelijk is. Sla de waarde van het `id` veld op zoals vereist in de volgende stap om een nieuwe gegevensstroom te maken.

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

De laatste stap op weg naar het verzamelen van reclamegegevens is het creëren van een dataflow. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source)
* [Doelverbinding-id](#target)
* [Toewijzing-id](#mapping)
* [Dataflow-specificatie-id](#specs)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day`, of `week`. De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde worden ingesteld op gelijk aan of groter dan `15`.

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
        "name": "Advertising dataflow",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "ca7b8baa-587e-4223-bb8b-aa587e4223e3"
        ],
        "targetConnectionIds": [
            "41af25df-cd99-4372-af25-dfcd99b37291"
        ],
        "transformations": [
            {
            "name": "Mapping",
            "params": {
                "mappingId": "febec6a6785e45ea9ed594422cc483d7",
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

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | De flow-specificatie-id die in de vorige stap is opgehaald. |
| `sourceConnectionIds` | De bronverbindings-id die in een eerdere stap is opgehaald. |
| `targetConnectionIds` | De doel verbindings ID die in een vroegere stap wordt teruggewonnen. |
| `transformations.params.mappingId` | De toewijzing-id die in een eerdere stap is opgehaald. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in epoche tijd in seconden. |
| `scheduleParams.frequency` | De volgende frequentiewaarden kunnen worden geselecteerd: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en groter dan of gelijk aan `15` andere frequentiewaarden moet zijn. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om gegevens van een reclamesysteem op een geplande basis te verzamelen. De inkomende gegevens kunnen nu door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant in real time en de Werkruimte van de Wetenschap van Gegevens worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)