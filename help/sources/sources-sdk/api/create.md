---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Een nieuwe verbindingsspecificatie maken met de Flow Service API
description: Het volgende document verstrekt stappen op hoe te om een verbindingsspecificatie tot stand te brengen gebruikend de Dienst API van de Stroom en een nieuwe bron door Zelfbediening Bronnen te integreren.
exl-id: 0b0278f5-c64d-4802-a6b4-37557f714a97
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---

# Een nieuwe verbindingsspecificatie maken met de opdracht [!DNL Flow Service] API

Een verbindingsspecificatie vertegenwoordigt de structuur van een bron. Het bevat informatie over de authentificatievereisten van een bron, bepaalt hoe de brongegevens kunnen worden onderzocht en worden geïnspecteerd, en verstrekt informatie over de attributen van een bepaalde bron. De `/connectionSpecs` in de [!DNL Flow Service] API staat u toe om de verbindingsspecificaties binnen uw organisatie programmatically te beheren.

In het volgende document worden de volgende stappen beschreven voor het maken van een verbindingsspecificatie met de opdracht [!DNL Flow Service] API en een nieuwe bron integreren via Self-Serve Sources (Batch SDK).

## Aan de slag

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Artefacten verzamelen

Als u een nieuwe batchbron wilt maken met behulp van Self-Serve Sources, moet u eerst coördineren met Adobe, een persoonlijke Git-opslagplaats aanvragen en op de details met betrekking tot het label, de beschrijving, de categorie en het pictogram voor uw bron uitlijnen met Adobe.

Zodra u de Git-opslagruimte hebt opgegeven, moet u deze als volgt structureren:

* Bronnen
   * {your_source}
      * Artefacten
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefacten (bestandsnamen) | Beschrijving | Voorbeeld |
| --- | --- | --- |
| {your_source} | De naam van de bron. Deze map moet alle artefacten bevatten die betrekking hebben op uw bron, in uw persoonlijke Git-opslagplaats. | `mailchimp-members` |
| {your_source}-category.txt | De categorie waartoe uw bron behoort, opgemaakt als een tekstbestand. De lijst van beschikbare broncategorieën die door Zelfbediening Bronnen (de Band SDK) worden gesteund omvat: <ul><li>Reclame</li><li>Analytics</li><li>Toestemming en voorkeuren</li><li>CRM</li><li>Klant geslaagd</li><li>Database</li><li>e-commerce</li><li>Marketing Automation</li><li>Betalingen</li><li>Protocollen</li></ul> **Opmerking**: Neem contact op met uw Adobe als u van mening bent dat de bron niet in een van de bovenstaande categorieën past. | `mailchimp-members-category.txt` Geef in het bestand de categorie van de bron op, bijvoorbeeld: `marketingAutomation`. |
| {your_source}-description.txt | Een korte beschrijving van de bron. | [!DNL Mailchimp Members] is een marketingautomatiseringsbron die u kunt gebruiken om [!DNL Mailchimp Members] gegevens naar Experience Platform. |
| {your_source}-icon.svg | De afbeelding die moet worden gebruikt om uw bron weer te geven in de catalogus met bronnen in het Experience Platform. Dit pictogram moet een SVG-bestand zijn. |
| {your_source}-label.txt | De naam van de bron zoals deze moet worden weergegeven in de catalogus met bronnen van het Experience Platform. | Mailchimp-leden |
| {your_source}-connectionSpec.json | Een JSON-bestand dat de verbindingsspecificatie van uw bron bevat. Dit bestand is in eerste instantie niet vereist omdat u de verbindingsspecificatie invult als u deze handleiding invult. | `mailchimp-members-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Tijdens de testperiode van uw verbindingsspecificatie, in plaats van zeer belangrijke waarden, kunt u gebruiken `text` in het verbindingsdossier.

Nadat u de benodigde bestanden hebt toegevoegd aan uw persoonlijke Git-opslagplaats, moet u een pull-aanvraag (PR) maken die door Adobe kan worden gecontroleerd. Wanneer uw PR wordt goedgekeurd en samengevoegd, zult u van identiteitskaart worden voorzien die voor uw verbindingsspecificatie kan worden gebruikt om naar het etiket, de beschrijving, en het pictogram van uw bron te verwijzen.

Voer vervolgens de onderstaande stappen uit om uw verbindingsspecificatie te configureren. Voor extra begeleiding op de verschillende functionaliteiten die u aan uw bron kunt toevoegen, zoals geavanceerd het plannen, douaneschema, of verschillende paginatypen, te herzien gelieve de gids op [bronspecificaties configureren](../config/sourcespec.md).

## Sjabloon voor verbindingsspecificatie kopiëren

Nadat u de vereiste artefacten hebt verzameld, kopieert en plakt u de onderstaande sjabloon voor de verbindingsspecificatie naar de teksteditor van uw keuze en werkt u de kenmerken tussen haakjes bij `{}` met informatie die relevant is voor uw specifieke bron.

```json
{
  "name": "generic-rest-extension",
  "type": "generic-rest",
  "description": "{DESCRIPTION}",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "uiAttributes": {
      "apiFeatures": {
        "explorePaginationSupported": false
      }
    }
  },
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "clientId": {
            "description": "Client id of user account.",
            "type": "string"
          },
          "clientSecret": {
            "description": "Client secret of user account.",
            "type": "string",
            "format": "password"
          },
          "accessToken": {
            "description": "Access Token",
            "type": "string",
            "format": "password"
          },
          "refreshToken": {
            "description": "Refresh Token",
            "type": "string",
            "format": "password"
          },
          "expirationDate": {
            "description": "Date of token expiry.",
            "type": "string",
            "format": "date",
            "uiAttributes": {
              "hidden": true
            }
          },
          "accessTokenUrl": {
            "description": "Access token url to fetch access token.",
            "type": "string"
          },
          "requestParameterOverride": {
            "type": "object",
            "description": "Specify parameter to override.",
            "properties": {
              "accessTokenField": {
                "description": "Access token field name to override.",
                "type": "string"
              },
              "refreshTokenField": {
                "description": "Refresh token field name to override.",
                "type": "string"
              },
              "expireInField": {
                "description": "ExpireIn field name to override.",
                "type": "string"
              },
              "authenticationMethod": {
                "description": "Authentication method override.",
                "type": "string",
                "enum": [
                  "GET",
                  "POST"
                ]
              },
              "clientId": {
                "description": "ClientId field name override.",
                "type": "string"
              },
              "clientSecret": {
                "description": "ClientSecret field name override.",
                "type": "string"
              }
            }
          }
        },
        "required": [
          "host",
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
          "username": {
            "description": "Username to connect rest endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect rest endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "protocols"
        },
        "icon": {
          "key": "genericRestIcon"
        },
        "description": {
          "key": "genericRestDescription"
        },
        "label": {
          "key": "genericRestLabel"
        }
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "Http method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "query parameters in json format",
              "example": "{'key':'value','key1':'value1'} in JSON format"
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "header parameters in json format",
          "example": "{'user':'c26f50c88dc035610e6753f807e28e9','x-api-key':'apiKey'}"
        },
        "contentPath": {
          "type": "object",
          "description": "Params required for main collection content.",
          "properties": {
            "path": {
              "description": "path to main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "Params required for sub-array content.",
          "properties": {
            "path": {
              "description": "path to sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "Params required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "Pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "number of records per page to fetch.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "pointer property name",
              "example": "pointer"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "Params required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
  "exploreSpec": {
    "name": "Resource",
    "type": "Resource",
    "requestSpec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object"
    },
    "responseSpec": {
      "$schema": "http: //json-schema.org/draft-07/schema#",
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
```

## Een verbindingsspecificatie maken {#create}

Nadat u de sjabloon voor de verbindingsspecificatie hebt verkregen, kunt u nu een nieuwe verbindingsspecificatie ontwerpen door de juiste waarden in te vullen die overeenkomen met de bron.

Een verbindingsspecificatie kan in drie verschillende delen worden verdeeld: de verificatiespecificaties, de bronspecificaties en de verkennende specificaties.

Zie de volgende documenten voor instructies over hoe u de waarden van elk deel van een verbindingsspecificatie kunt vullen:

* [Uw verificatiespecificatie configureren](../config/authspec.md)
* [Uw bronspecificatie configureren](../config/sourcespec.md)
* [Uw verkenningsspecificatie configureren](../config/explorespec.md)

Als de opgegeven gegevens zijn bijgewerkt, kunt u de nieuwe verbindingsspecificatie verzenden door een verzoek van de POST in te dienen bij de `/connectionSpecs` van het [!DNL Flow Service] API.

**API-indeling**

```http
POST /connectionSpecs
```

**Verzoek**

Het volgende verzoek is een voorbeeld van een volledig geschreven verbindingsspecificatie voor een [!DNL MailChimp] bron:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MailChimp Members source",
      "description": "MailChimp Members source using generic-rest and SDK",
      "type": "generic-rest",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
          "uiAttributes": {
              "apiFeatures": {
                  "explorePaginationSupported": false
              }
          }
      },
      "authSpec": [
          {
              "name": "OAuth2 Refresh Code",
              "type": "OAuth2RefreshCode",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "authorizationTestUrl": {
                          "description": "Authorization test url to validate accessToken.",
                          "type": "string"
                      },
                      "accessToken": {
                          "description": "Access Token of mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "accessToken"
                  ]
              }
          },
          {
              "name": "Basic Authentication",
              "type": "BasicAuthentication",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines auth params required for connecting to rest service.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "username": {
                          "description": "Username to connect mailChimp endpoint.",
                          "type": "string"
                      },
                      "password": {
                          "description": "Password to connect mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "username",
                      "password"
                  ]
              }
          }
      ],
      "sourceSpec": {
          "attributes": {
              "uiAttributes": {
                  "isSource": true,
                  "isPreview": true,
                  "isBeta": true,
                  "icon": {
                      "key": "mailchimpMembersIcon"
                  },
                  "description": {
                      "key": "mailchimpMembersDescription"
                  },
                  "label": {
                      "key": "mailchimpMembersLabel"
                  }
              },
              "urlParams": {
                  "host": "https://${domain}.api.mailchimp.com",
                  "path": "/3.0/lists/${listId}/members",
                  "method": "GET"
              },
              "contentPath": {
                  "path": "$.members",
                  "skipAttributes": [
                    "_links",
                    "total_items",
                    "list_id"
                  ],
                  "overrideWrapperAttribute": "member"
                },
              "paginationParams": {
                  "type": "OFFSET",
                  "limitName": "count",
                  "limitValue": "100",
                  "offSetName": "offset"
              },
              "scheduleParams": {
                  "scheduleStartParamName": "since_last_changed",
                  "scheduleEndParamName": "before_last_changed",
                  "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                  "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
              }
          },
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "description": "Define user input parameters to fetch resource values.",
              "properties": {
                  "listId": {
                      "type": "string",
                      "description": "listId for which members need to fetch."
                  }
              }
          }
      },
      "exploreSpec": {
          "name": "Resource",
          "type": "Resource",
          "requestSpec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object"
          },
          "responseSpec": {
              "$schema": "http: //json-schema.org/draft-07/schema#",
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
  }'
```

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbindingsspecificatie geretourneerd, inclusief de unieke `id`.

```json
{
    "id": "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55",
    "createdAt": 1633388930134,
    "updatedAt": 1633388930134,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "MailChimp Members source",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "type": "generic-rest",
    "authSpec": [
        {
            "name": "OAuth2 Refresh Code",
            "type": "OAuth2RefreshCode",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path"
                    },
                    "authorizationTestUrl": {
                        "description": "Authorization test url to validate accessToken.",
                        "type": "string"
                    },
                    "accessToken": {
                        "description": "Access Token of mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "accessToken"
                ]
            }
        },
        {
            "name": "Basic Authentication",
            "type": "BasicAuthentication",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "defines auth params required for connecting to rest service.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path."
                    },
                    "username": {
                        "description": "Username to connect mailChimp endpoint.",
                        "type": "string"
                    },
                    "password": {
                        "description": "Password to connect mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "username",
                    "password"
                ]
            }
        }
    ],
    "sourceSpec": {
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "Define user input parameters to fetch resource values.",
            "properties": {
                "listId": {
                    "type": "string",
                    "description": "listId for which members need to fetch."
                }
            }
        },
        "attributes": {
            "uiAttributes": {
                "isSource": true,
                "isPreview": true,
                "isBeta": true,
                "icon": {
                    "key": "mailchimpMembersIcon"
                },
                "description": {
                    "key": "mailchimpMembersDescription"
                },
                "label": {
                    "key": "mailchimpMembersLabel"
                }
            },
            "urlParams": {
                "path": "/3.0/lists/${listId}/members",
                "method": "GET"
            },
            "contentPath": {
                    "path": "$.members",
                    "skipAttributes": [
                      "_links",
                      "total_items",
                      "list_id"
                    ],
                    "overrideWrapperAttribute": "member"
                  },
            "paginationParams": {
                "type": "OFFSET",
                "limitName": "count",
                "limitValue": "100",
                "offSetName": "offset"
            },
            "scheduleParams": {
                "scheduleStartParamName": "since_last_changed",
                "scheduleEndParamName": "before_last_changed",
                "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
            }
        }
    },
    "exploreSpec": {
        "name": "Resource",
        "type": "Resource",
        "requestSpec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object"
        },
        "responseSpec": {
            "$schema": "http: //json-schema.org/draft-07/schema#",
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
    },
    "attributes": {
        "uiAttributes": {
            "apiFeatures": {
                "explorePaginationSupported": false
            }
        }
    }
}
```

## Volgende stappen

Nu u een nieuwe verbindingsspecificatie hebt gecreeerd, moet u zijn overeenkomstige identiteitskaart van de verbindingsspecificatie aan een bestaande stroomspecificatie toevoegen. Zie de zelfstudie aan [bijwerken, stroomspecificaties](./update-flow-specs.md) voor meer informatie .

Als u wijzigingen wilt aanbrengen in de verbindingsspecificatie die u hebt gemaakt, raadpleegt u de zelfstudie over [bijwerken, verbindingsspecificaties](./update-connection-specs.md).
