---
title: Concepten maken van de API voor Flow Service Entities
description: Leer hoe u concepten van uw basisverbinding, bronverbinding, doelverbinding en gegevensstroom maakt met de Flow Service API
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 0%

---

# Concepten van uw [!DNL Flow Service] -entiteiten maken met de API

U kunt de `mode=draft` vraagparameter in [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) gebruiken om uw [!DNL Flow Service] entiteiten zoals uw basisverbindingen, bronverbindingen, doelverbindingen, en dataflows aan een ontwerpstaat te plaatsen.

Concepten kunnen later met nieuwe informatie worden bijgewerkt en vervolgens worden gepubliceerd zodra ze gereed zijn, met de parameter `op=publish` query.

Deze zelfstudie bevat stappen voor het instellen van [!DNL Flow Service] -entiteiten op een conceptstatus en biedt u de mogelijkheid om uw workflows te pauzeren en op te slaan zodat deze later kunnen worden voltooid.

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../landing/api-guide.md).

### Controleren op ondersteuning voor conceptmodus

U moet ook controleren of de verbinding-specificatie-id en de bijbehorende flow-specificatie-id van de bron die u gebruikt, zijn ingeschakeld voor de conceptmodus.

>[!BEGINTABS]

>[!TAB  bekijk de details van de verbindingsspecificatie ]

+++verzoek
Met de volgende aanvraag wordt de informatie over de verbindingsspecificatie voor [!DNL Azure File Storage] opgehaald:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een succesvolle reactie keert de informatie van de verbindingsspecificatie voor uw bron terug. Controleer of de waarde van `items[0].attributes.isDraftModeSupported` is ingesteld op `true` om te controleren of de conceptmodus voor uw bron wordt ondersteund.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

>[!TAB  de specificatiedetails van de opzoekstroom ]

+++verzoek
Met het volgende verzoek worden de gegevens over de stroomspecificaties voor een bron voor cloudopslag opgehaald:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een succesvolle reactie keert de stroom specifieke informatie voor uw bron terug. Controleer of de waarde van `items[0].attributes.isDraftModeSupported` is ingesteld op `true` om te controleren of de conceptmodus voor uw bron wordt ondersteund.

```json {line-numbers="true" start-line="1" highlight="167"}
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
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
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
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "isDraftModeSupported": true,
        "frequency": "batch",
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

+++

>[!ENDTABS]



## Concepten van basisverbindingen maken {#create-a-draft-base-connection}

Als u een conceptbasisverbinding wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt van de [!DNL Flow Service] API en geeft u `mode=draft` op als een queryparameter.

**API formaat**

```http
POST /connections?mode=draft
```

| Parameter | Beschrijving |
| --- | --- |
| `mode` | Een door de gebruiker opgegeven queryparameter die de status van de basisverbinding bepaalt. Als u een basisverbinding wilt instellen als concept, stelt u `mode` in op `draft` . |

**Verzoek**

Met het volgende verzoek wordt een conceptbasisverbinding voor de [!DNL Azure File Storage] -bron gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Reactie**

Een geslaagde reactie retourneert de basis-verbindings-id en het bijbehorende label voor de conceptbasisverbinding. U kunt deze id later gebruiken om uw basisverbinding bij te werken en te publiceren.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Uw basisverbinding voor concepten publiceren {#publish-your-draft-base-connection}

Zodra uw concept klaar is om te worden gepubliceerd, dient u een POST-verzoek in bij het `/connections` -eindpunt en verstrekt u de id van de conceptbasisverbinding die u wilt publiceren, alsmede een handeling voor het publiceren.

**API formaat**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `op` | Een handelingsverrichting die de staat van de gevraagde basisverbinding bijwerkt. Stel `op` in op `publish` als u een conceptbasisverbinding wilt publiceren. |

**Verzoek**

In het volgende verzoek wordt de conceptbasisverbinding voor [!DNL Azure File Storage] gepubliceerd die in een eerdere stap is gemaakt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert identiteitskaart en het overeenkomstige etiket voor uw gepubliceerde basisverbinding terug.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Concepten van bronverbindingen maken {#create-a-draft-source-connection}

Als u een conceptbronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API en geeft u `mode=draft` op als een queryparameter.

**API formaat**

```http
POST /sourceConnections?mode=draft
```

| Parameter | Beschrijving |
| --- | --- |
| `mode` | Een door de gebruiker opgegeven queryparameter die de status van de bronverbinding bepaalt. Als u een bronverbinding wilt instellen als concept, stelt u `mode` in op `draft` . |

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Reactie**

Een geslaagde reactie retourneert de bron-verbindings-id en de bijbehorende tag voor de conceptbronverbinding. U kunt deze id later gebruiken om uw bronverbinding bij te werken en te publiceren.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Uw conceptbronverbinding publiceren {#publish-your-draft-source-connection}

>[!NOTE]
>
>U kunt geen bronverbinding publiceren als de bijbehorende basisverbinding zich nog in het concept bevindt. Controleer of uw basisverbinding eerst is gepubliceerd voordat u uw bronverbinding publiceert.

Zodra uw concept klaar is om te worden gepubliceerd, dient u een POST-verzoek in bij het `/sourceConnections` -eindpunt en verstrekt u de id van de conceptbronverbinding die u wilt publiceren, alsmede een handeling voor het publiceren.

**API formaat**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `op` | Een handelingsverrichting die de staat van de gevraagde bronverbinding bijwerkt. Als u een conceptbronverbinding wilt publiceren, stelt u `op` in op `publish` . |

**Verzoek**

In het volgende verzoek wordt de conceptbronverbinding voor [!DNL Azure File Storage] gepubliceerd die in een eerdere stap is gemaakt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert identiteitskaart en het overeenkomstige etiket voor uw gepubliceerde bronverbinding terug.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Concepten van doelverbinding maken {#create-a-draft-target-connection}

Als u een conceptdoelverbinding wilt maken, vraagt u een POST-aanvraag naar het `/targetConnections` -eindpunt van de [!DNL Flow Service] API en geeft u `mode=draft` op als een queryparameter.

**API formaat**

```http
POST /targetConnections?mode=draft
```

| Parameter | Beschrijving |
| --- | --- |
| `mode` | Een door de gebruiker opgegeven queryparameter die de status van de doelverbinding bepaalt. Als u een doelverbinding wilt instellen als concept, stelt u `mode` in op `draft` . |

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Reactie**

Een geslaagde reactie retourneert de doel-verbindings-id en de bijbehorende tag voor de conceptdoelverbinding. U kunt deze id later gebruiken om uw doelverbinding bij te werken en te publiceren.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Conceptdoelverbinding publiceren {#publish-your-draft-target-connection}

>[!NOTE]
>
>U kunt geen doelverbinding publiceren als de bijbehorende basisverbinding zich nog in de conceptstatus bevindt. Controleer of uw basisverbinding eerst is gepubliceerd voordat u de doelverbinding publiceert.

Zodra uw concept klaar is om te worden gepubliceerd, dient u een POST-verzoek in bij het `/targetConnections` -eindpunt en verstrekt u de id van de conceptdoelverbinding die u wilt publiceren, alsmede een handeling voor het publiceren.

**API formaat**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `op` | Een handelingsverrichting die de staat van de gevraagde doelverbinding bijwerkt. Als u een conceptdoelverbinding wilt publiceren, stelt u `op` in op `publish` . |

**Verzoek**

In het volgende verzoek wordt de conceptdoelverbinding voor [!DNL Azure File Storage] gepubliceerd die in een eerdere stap is gemaakt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert identiteitskaart en het overeenkomstige etiket voor uw gepubliceerde doelverbinding terug.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Concepten van gegevensstroom maken {#create-a-draft-dataflow}

Als u een gegevensstroom als concept wilt instellen, vraagt u een POST-verzoek om het `/flows` -eindpunt terwijl u de `mode=draft` als queryparameter toevoegt. Op deze manier kunt u een gegevensstroom maken en deze opslaan als concept.

**API formaat**

```http
POST /flows?mode=draft
```

| Parameter | Beschrijving |
| --- | --- |
| `mode` | Een door de gebruiker opgegeven queryparameter die de status van de gegevensstroom bepaalt. Als u een gegevensstroom wilt instellen als concept, stelt u `mode` in op `draft` . |

**Verzoek**

Met het volgende verzoek wordt een concept-gegevensstroom gemaakt.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Reactie**

Een geslaagde reactie retourneert de stroom-id en de bijbehorende tag voor de conceptgegevensstroom. U kunt deze id later gebruiken om uw gegevensstroom bij te werken en te publiceren.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Uw conceptgegevensstroom publiceren {#publish-your-draft-dataflow}

>[!NOTE]
>
>U kunt geen gegevensstroom publiceren als zijn bijbehorende bron en doelverbindingen nog in ontwerpstaat zijn. Zorg ervoor dat uw bron- en doelverbindingen eerst worden gepubliceerd voordat u uw gegevensstroom publiceert.

Zodra uw concept klaar is om te worden gepubliceerd, dient u een POST-verzoek in bij het `/flows` -eindpunt terwijl u de id opgeeft van de conceptgegevensstroom die u wilt publiceren, en een handeling voor het publiceren.

**API formaat**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `op` | Een handelingsverrichting die de staat van de gevraagde dataflow bijwerkt. Als u een conceptgegevensstroom wilt publiceren, stelt u `op` in op `publish` . |

**Verzoek**

Met het volgende verzoek wordt uw conceptgegevensstroom gepubliceerd.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een geslaagde reactie retourneert de id en de bijbehorende `etag` gegevensstroom.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u geleerd hoe u concepten van uw [!DNL Flow Service] -entiteiten kunt maken en deze concepten kunt publiceren. Voor meer informatie over bronnen, te lezen gelieve het [ overzicht van bronnen ](../../home.md).