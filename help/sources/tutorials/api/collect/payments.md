---
keywords: Experience Platform;home;popular topics;Collect payment data;payment data
solution: Experience Platform
title: Betalingsgegevens verzamelen via bronconnectors en API's
topic: overview
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het ophalen van gegevens van een betalingstoepassing en het opnemen ervan in het Platform via bronconnectors en API's.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 0%

---


# Betalingsgegevens verzamelen via bronconnectors en API&#39;s

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie worden de stappen beschreven voor het ophalen van gegevens van een betalingssysteem van derden en het opnemen ervan [!DNL Platform] via bronconnectors en de [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

## Aan de slag

Deze zelfstudie vereist dat u toegang hebt tot een betalingssysteem via een geldige verbinding, en dat u informatie hebt over het bestand waarin u het bestand wilt plaatsen [!DNL Platform] (inclusief het pad en de structuur van het bestand). Als u deze informatie niet hebt, raadpleegt u de zelfstudie over het [verkennen van een betalingstoepassing met behulp van de Flow Service API](../explore/payments.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Met de API voor batchverwerking kunt u gegevens invoeren in [!DNL Experience Platform] als batchbestanden.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met een betalingstoepassing met de [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Een ad-hoc XDM-klasse en -schema maken

Om externe gegevens door bronschakelaars in te brengen, moet een ad hoc klasse XDM en een schema voor de ruwe brongegevens worden gecreeerd. [!DNL Platform]

Als u een ad-hocklasse en -schema wilt maken, volgt u de stappen in de zelfstudie over het [ad-hocschema](../../../../xdm/tutorials/ad-hoc.md). Wanneer u een ad-hocklasse maakt, moeten alle velden in de brongegevens worden beschreven in de aanvraaginstantie.

Ga door met het volgen van de stappen die in de ontwikkelaarsgids worden beschreven tot u een ad-hocschema hebt gecreeerd. Haal de unieke id (`$id`) van het ad-hocschema op en sla deze op. Ga vervolgens verder met de volgende stap van deze zelfstudie.

## Een bronverbinding maken {#source}

Als een ad-hoc XDM-schema is gemaakt, kan nu een bronverbinding worden gemaakt met behulp van een verzoek van de POST aan de [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbindingsID, een brongegevensbestand, en een verwijzing naar het schema dat de brongegevens beschrijft.

Als u een bronverbinding wilt maken, moet u ook een opsommingswaarde voor het kenmerk voor de gegevensindeling definiëren.

Gebruik de volgende enum waarden voor op dossier-gebaseerde schakelaars:

| Data.format | Enumwaarde |
| ----------- | ---------- |
| Gescheiden bestanden | `delimited` |
| JSON-bestanden | `json` |
| Parketbestanden | `parquet` |

Voor alle op lijst-gebaseerde schakelaars gebruiken de enum waarde: `tabular`.

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
        "name": "Paypal source connection",
        "baseConnectionId": "24151d58-ffa7-4960-951d-58ffa7396097",
        "description": "Paypal",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/396f583b57577b2f2fca79c2cb88e9254992f5fa70ce5f1a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "PayPal.Catalog_Products"
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De unieke verbindings-id van de betalingstoepassing van derden waartoe u toegang hebt. |
| `data.schema.id` | Het `$id` ad-hoc XDM-schema. |
| `params.path` | Het pad van het bronbestand. |
| `connectionSpec.id` | De verbindingsspecificatie-id van uw betalingstoepassing. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is vereist in latere stappen om een doelverbinding te maken.

```json
{
    "id": "2c48a152-3d49-43cb-88a1-523d49e3cbcb",
    "etag": "\"8000c843-0000-0200-0000-5e8917ea0000\""
}
```

## Een doel-XDM-schema maken {#target-schema}

In eerdere stappen werd een ad-hoc XDM-schema gemaakt om de brongegevens te structureren. Als u de brongegevens in wilt gebruiken, moet u ook een doelschema maken om de brongegevens te structureren op basis van uw behoeften. [!DNL Platform] Het doelschema wordt dan gebruikt om een [!DNL Platform] dataset tot stand te brengen waarin de brongegevens bevat zijn. Dit doel-XDM-schema breidt ook de XDM- [!DNL Individual Profile] klasse uit.

Een doelXDM schema kan worden gecreeerd door een verzoek van de POST aan de Registratie API [van het](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schema uit te voeren. Als u de gebruikersinterface liever in wilt gebruiken, [!DNL Experience Platform]biedt de zelfstudie [van de](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html) Schema-editor stapsgewijze instructies voor het uitvoeren van vergelijkbare acties in de Schema-editor.

**API-indeling**

```https
POST /tenant/schemas
```

**Verzoek**

Met de volgende voorbeeldaanvraag wordt een XDM-schema gemaakt dat de XDM- [!DNL Individual Profile] klasse uitbreidt.

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
        "title": "Target schema for payments",
        "description": "Target schema for payments",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:altId": "_{TENANT_ID}.schemas.14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for payments",
    "type": "object",
    "description": "Target schema for Paypal",
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

Een doeldataset kan worden gecreeerd door een verzoek van de POST aan de Dienst API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogus uit te voeren, die identiteitskaart van het doelschema binnen de nuttige lading verstrekken.

**API-indeling**

```https
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
        "name": "Target dataset for payments",
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
    "@/dataSets/5e8918669cbbee18ad9771f3"
]
```

## Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Als u een doelverbinding wilt maken, moet u de vaste specificatie-id voor de verbinding opgeven die is gekoppeld aan het datumpeer. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan gegevens meer. Gebruikend deze herkenningstekens, kunt u een doelverbinding tot stand brengen gebruikend API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten. [!DNL Flow Service]

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
        "name": "Target Connection for payments",
        "description": "Target Connection for payments",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722"
            }
        },
        "params": {
            "dataSetId": "5e8918669cbbee18ad9771f3"
        },
            "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
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

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe doelverbinding. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "c8e12917-ac33-44d7-a129-17ac3364d7b7",
    "etag": "\"0f015874-0000-0200-0000-5e8918e60000\""
}
```

## Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht de doeldataset volgt aan. Dit wordt bereikt door een verzoek van de POST aan de [Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) van de Omzetting met gegevens uit te voeren die binnen de verzoeklading worden bepaald.

**API-indeling**

```https
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Product_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.name",
                "sourceAttribute": "Product_Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.description",
                "sourceAttribute": "Description",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.type",
                "sourceAttribute": "Type",
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
    "id": "b54a8dc38e8d4e31a2dc096e413ae8e5",
    "version": 0,
    "createdDate": 1586043319604,
    "modifiedDate": 1586043319604,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Specificaties voor gegevensstroom opzoeken {#specs}

Een gegevensstroom is verantwoordelijk voor het verzamelen van gegevens uit bronnen en het brengen van hen in [!DNL Platform]. Als u een gegevensstroom wilt maken, moet u eerst de gegevensstroomspecificaties verkrijgen door een GET-aanvraag voor de [!DNL Flow Service] API uit te voeren. Dataflow-specificaties zijn verantwoordelijk voor het verzamelen van gegevens van een externe database of een NoSQL-systeem.

**API-indeling**

```https
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

Een succesvol antwoord retourneert de details van de gegevensstroomspecificatie die verantwoordelijk is voor het plaatsen van gegevens van uw betalingstoepassing in [!DNL Platform]. Deze id is vereist in de volgende stap om een nieuwe gegevensstroom te maken.

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

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

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
        "name": "Dataflow between payments Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "2c48a152-3d49-43cb-88a1-523d49e3cbcb"
        ],
        "targetConnectionIds": [
            "c8e12917-ac33-44d7-a129-17ac3364d7b7"
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
                    "mappingId": "b54a8dc38e8d4e31a2dc096e413ae8e5",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency": "minute",
            "interval":"30"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `flowSpec.id` | De [flow-specificatie-id](#specs) die in de vorige stap is opgehaald. |
| `sourceConnectionIds` | De [bronverbindings-id](#source) die in een eerdere stap is opgehaald. |
| `targetConnectionIds` | De [doel-verbindings-id](#target-connection) die in een eerdere stap is opgehaald. |
| `transformations.params.mappingId` | De [toewijzings-id](#mapping) die in een eerdere stap is opgehaald. |
| `transformations.params.deltaColum` | De opgegeven kolom die wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. De ondersteunde datumnotatie voor `deltaColumn` is `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | De toewijzing-id die aan uw database is gekoppeld. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en groter dan of gelijk aan `15` andere frequentiewaarden moet zijn. |

**Antwoord**

Een geslaagde reactie retourneert de id `id` van de nieuwe gegevensstroom.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor meer informatie over hoe te om gegevensstromen te controleren, zie de zelfstudie over het [controleren van gegevensstromen in API ](../monitor.md)


## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om gegevens van een betalingstoepassing op een geplande basis te verzamelen. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)