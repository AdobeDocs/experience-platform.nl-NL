---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Stroomspecificaties bijwerken met behulp van de Flow Service API
description: Het volgende document bevat stappen voor het ophalen en bijwerken van stroomspecificaties met behulp van de Flow Service API voor Self-Serve Sources (Batch SDK).
exl-id: 67a0cd3e-ac18-43a4-aa22-8f6376d5cc3f
source-git-commit: 21bccacf3555881ae731d0e60ff7d7677f18732d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Stroomspecificaties bijwerken met de API [!DNL Flow Service]

Als u een nieuwe id voor de verbindingsspecificatie hebt gegenereerd, moet u deze id toevoegen aan een stroomspecificatie om een gegevensstroom te kunnen maken.

De specificaties van de stroom bevatten informatie die een stroom bepaalt, met inbegrip van bron en doel verbindings IDs die het steunt, transformatiespecificaties die nodig zijn om op de gegevens worden toegepast, en het plannen van parameters die worden vereist om een stroom te produceren. U kunt stroomspecificaties bewerken met het eindpunt `/flowSpecs` .

In het volgende document worden stappen beschreven voor het ophalen en bijwerken van stroomspecificaties met de [!DNL Flow Service] API voor Self-Serve Sources (Batch SDK).

## Aan de slag

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een stroomspecificatie opzoeken {#lookup}

Bronnen die zijn gemaakt met de `generic-rest-extension` -sjabloon, gebruiken allemaal de `RestStorageToAEP` flow specification. Deze flowspecificatie kan worden opgehaald door een aanvraag voor een GET in te dienen bij het `/flowSpecs/` -eindpunt en de eigenschap `flowSpec.id` of `6499120c-0b15-42dc-936e-847ea3c24d72` op te geven.

**API formaat**

```http
GET /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Verzoek**

Met de volgende aanvraag wordt de verbindingsspecificatie `6499120c-0b15-42dc-936e-847ea3c24d72` opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Reactie**

Een geslaagde reactie retourneert de details van de queried flow specificatie.

```json
{
  "items": [
      {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "createdAt": 1633080822911,
          "updatedAt": 1633080822911,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "{SANDBOX_ID}",
          "sandboxName": "{SANDBOX_NAME}",
          "imsOrgId": "{ORG_ID}",
          "name": "RestStorageToAEP",
          "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
          "version": "1.0",
          "sourceConnectionSpecIds": [
              "2d46966e-4fcc-4015-9f9e-a67594e395a3"
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
      },
  ]
}
```

## Een stroomspecificatie bijwerken {#update}

U kunt de velden van een verbindingsspecificatie bijwerken via een PUT-bewerking. Wanneer het bijwerken van een verbindingsspecificatie door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die zouden worden vereist wanneer het creëren van een nieuwe verbindingsspecificatie in een verzoek van de POST.

>[!IMPORTANT]
>
>U moet de lijst van `sourceConnectionSpecIds` van de stroomspecificatie bijwerken die aan een nieuwe bron beantwoordt telkens als een nieuwe bron wordt gecreeerd. Dit zorgt ervoor dat uw nieuwe bron door een bestaande stroomspecificatie wordt gesteund, zodat kunt u het proces van de gegevensstroom tot stand brengen met uw nieuwe bron voltooien.

**API formaat**

```http
PUT /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**Verzoek**

De volgende aanvraag werkt de stroomspecificatie van `6499120c-0b15-42dc-936e-847ea3c24d72` bij en bevat de verbindingsspecificatie-id `f6c0de0c-0a42-4cd9-9139-8768bf2f1b55` .

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
`     "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "name": "RestStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
      ]
    }'
```

**Reactie**

Een geslaagde reactie retourneert de details van de aangevraagde flowspecificatie, inclusief de bijgewerkte lijst van `sourceConnectionSpecIds` .

```json
{
    "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "RestStorageToAEP",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
```

## Volgende stappen

Als de nieuwe verbindingsspecificatie aan de juiste stroomspecificatie is toegevoegd, kunt u nu doorgaan met testen en uw nieuwe bron verzenden. Zie de gids op [ het testen en het voorleggen van een nieuwe bron ](./submit.md) voor meer informatie.
