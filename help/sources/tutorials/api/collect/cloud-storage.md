---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevens voor cloudopslag verzamelen via bronconnectors en API's
topic: overview
translation-type: tm+mt
source-git-commit: 4a66be0b49bdcd765fd5dcbd0e646d35df54c7e4
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---


# Gegevens voor cloudopslag verzamelen via bronconnectors en API&#39;s

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie worden de stappen beschreven voor het ophalen van gegevens van externe cloudopslag en het doorsturen van deze gegevens naar Platform via bronconnectors en API&#39;s.

## Aan de slag

Deze zelfstudie vereist dat u toegang hebt tot cloudopslag van derden via een geldige verbinding en informatie over het bestand dat u in Platform wilt plaatsen, inclusief het pad en de structuur van het bestand. Als u deze informatie niet hebt, raadpleegt u de zelfstudie over het [verkennen van cloudopslag van derden met de Flow Service API](../explore/cloud-storage.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht in de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Handleiding](../../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
- [Catalogusservice](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen het Platform van de Ervaring.
- [Inname](../../../../ingestion/batch-ingestion/overview.md)in batch: Met de API voor inname van batch kunt u gegevens als batchbestanden in het Experience Platform opnemen.
- [Sandboxen](../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met een cloudopslag met de Flow Service API tot stand te brengen.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief de bronnen die bij Flow Service horen, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

- Inhoudstype: `application/json`

## Een ad-hoc XDM-klasse en -schema maken

Als u externe gegevens via bronconnectors wilt overbrengen naar Platform, moet u een ad-hoc XDM-klasse en -schema maken voor de onbewerkte brongegevens.

Als u een ad-hocklasse en -schema wilt maken, volgt u de stappen in de zelfstudie over het [ad-hocschema](../../../../xdm/tutorials/ad-hoc.md). Wanneer u een ad-hocklasse maakt, moeten alle velden in de brongegevens worden beschreven in de aanvraaginstantie.

Ga door met het volgen van de stappen die in de ontwikkelaarsgids worden beschreven tot u een ad-hocschema hebt gecreeerd. De unieke id (`$id`) van het ad-hocschema is vereist om door te gaan naar de volgende stap van deze zelfstudie.

## Een bronverbinding maken {#source}

Als een ad-hoc XDM-schema is gemaakt, kan nu een bronverbinding worden gemaakt met een POST-aanvraag voor de Flow Service API. Een bronverbinding bestaat uit een verbindingsID, een brongegevensbestand, en een verwijzing naar het schema dat de brongegevens beschrijft.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende opsommingswaarden voor op **bestanden gebaseerde connectors**:

| Data.format | Enumwaarde |
| ----------- | ---------- |
| Gescheiden bestanden | `delimited` |
| JSON-bestanden | `json` |
| Parketbestanden | `parquet` |

Voor alle op **lijst-gebaseerde schakelaars** gebruik de enum waarde: `tabular`.

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
        "name": "Test source connection for a Cloud Storage connector",
        "baseConnectionId": "ac33bd66-1565-4915-b3bd-6615657915c4",
        "description": "Test source connection for a Cloud Storage connector",
        "data": {
            "format": "delimited",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/22a4ab59462a64de551d42dd10ec1f19d8d7246e3f90072a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/backfil/data8.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `baseConnectionId` | De unieke verbinding-id van het externe cloudopslagsysteem dat u benadert. |
| `data.schema.id` | De id van het ad-hoc XDM-schema. |
| `params.path` | Het pad van het bronbestand dat u opent. |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan uw specifieke externe cloudopslagsysteem. Zie de [bijlage](#appendix) voor een lijst van verbindingsspecificaties - IDs. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is later vereist om een gegevensstroom te maken.

```json
{
    "id": "8bae595c-8548-4716-ae59-5c85480716e9",
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Een doel-XDM-schema maken {#target}

In eerdere stappen werd een ad-hoc XDM-schema gemaakt om de brongegevens te structureren. Voor de brongegevens die in Platform worden gebruikt, moet een doelschema ook worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doel-XDM-schema kan worden gemaakt door een POST-verzoek uit te voeren naar de [schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

Als u de gebruikersinterface in het Platform van de Ervaring liever zou gebruiken, verstrekt de zelfstudie [van de Redacteur van het](../../../../xdm/tutorials/create-schema-ui.md) Schema geleidelijke instructies voor het uitvoeren van gelijkaardige acties in de Redacteur van het Schema.

**API-indeling**

```http
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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
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

Een geslaagde reactie retourneert details van het nieuwe schema, inclusief de unieke id (`$id`). Deze id wordt vereist in recentere stappen om een doeldataset, afbeelding, en dataflow tot stand te brengen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:altId": "_{TENANT_ID}.schemas.e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Cloud Storage connector",
    "type": "object",
    "description": "Target schema for Cloud Storage",
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
        "repo:createdDate": 1589398474190,
        "repo:lastModifiedDate": 1589398474190,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "f07723475e933dc30ed411d97986a36f13aa20c820463dd8cf7b74e63f4e7801",
        "meta:globalLibVersion": "1.10.1.1"
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
        "name": "Target dataset for a Cloud Storage connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `schemaRef.id` | De id van het doel-XDM-schema. |

**Antwoord**

Een succesvolle reactie keert een serie terug die identiteitskaart van de pas gecreëerde dataset in het formaat bevat `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. De doel dataset identiteitskaart wordt vereist in recentere stappen om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5ebc4be8590b1b191a8dc4ca"
]
```

## Een doelverbinding maken

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste specificatie-id voor de verbinding opgeven die is gekoppeld aan het datumpeer. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan gegevens meer. Gebruikend deze herkenningstekens, kunt u een doelverbinding tot stand brengen gebruikend de Dienst API van de Stroom om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ebc4be8590b1b191a8dc4ca"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data.schema.id` | Het `$id` doel-XDM-schema. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | The fixed connection spec ID to data Lake. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe doelverbinding. Deze id is vereist in latere stappen.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een POST- verzoek aan de Dienst van de Omzetting met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
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
                "destinationXdmPath": "_id",
                "sourceAttribute": "id",
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert de details van de specificatie dataFlow die verantwoordelijk is voor het plaatsen van gegevens van uw cloudopslag in Platform. De reactie bevat een unieke flow-specificatie-id. Deze id is vereist in de volgende stap om een nieuwe gegevensstroom te maken.

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

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

Als u een opname wilt plannen, moet u eerst de begintijdwaarde instellen op Tijd in seconden. Vervolgens moet u de frequentiewaarde instellen op een van de vijf opties: `once`, `minute`, `hour`, `day`, of `week`. De intervalwaarde geeft de periode tussen twee opeenvolgende inname aan en het maken van een eenmalige inname vereist geen interval dat moet worden ingesteld. Voor alle andere frequenties moet de intervalwaarde worden ingesteld op gelijk aan of groter dan `15`.

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
        "name": "Cloud Storage flow to AEP",
        "description": "Cloud Storage flow to AEP",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8bae595c-8548-4716-ae59-5c85480716e9"
        ],
        "targetConnectionIds": [
            "1f5af99c-f1ef-4076-9af9-9cf1ef507678"
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
            "startTime": "1589398646",
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

Aan de hand van deze zelfstudie hebt u een bronaansluiting gemaakt om gegevens van uw cloudopslag op een geplande basis te verzamelen. De inkomende gegevens kunnen nu door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant in real time en de Werkruimte van de Wetenschap van Gegevens worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)

## Aanhangsel

In de volgende sectie worden de verschillende connectors voor bronnen voor cloudopslag en de bijbehorende verbindingsspecificaties weergegeven.

### Verbindingsspecificatie

| Naam van connector | Verbindingsspecificatie |
| -------------- | --------------- |
| Amazon S3 (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Azure Blob (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Azure Data Lake Storage Gen2 (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Azure Event Hubs (Event Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Azure-bestandsopslag | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| Google Cloud-opslag | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |