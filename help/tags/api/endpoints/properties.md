---
title: Het eindpunt Eigenschappen
description: Leer hoe te om vraag aan het /properties eindpunt in Reactor API te maken.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 1%

---

# Het eindpunt Eigenschappen

Een eigenschap is een containerconstructie die de meeste andere bronnen bevat die beschikbaar zijn in de Reactor-API. U beheert eigenschappen programmatically gebruikend het `/properties` eindpunt.

In de middelhiërarchie, is een bezit de eigenaar van het volgende:

* [Builds](./builds.md)
* [Callbacks](./callbacks.md)
* [Gegevenselementen](./data-elements.md)
* [Omgevingen](./environments.md)
* [Extensies](./extensions.md)
* [Gastheren](./properties.md)
* [Bibliotheken](./libraries.md)
* [Regelcomponenten](./rule-components.md)
* [Regels](./rules.md)

Een eigenschap behoort tot exact één [bedrijf](./companies.md). Een bedrijf kan vele eigenschappen hebben.

Voor meer algemene informatie over eigenschappen en hun rol in markeringsbeheer, zie het overzicht op [bedrijven en eigenschappen](../../ui/administration/companies-and-properties.md).

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Een lijst met eigenschappen ophalen {#list}

U kunt een lijst van eigenschappen terugwinnen die tot bedrijf door bedrijfsidentiteitskaart in de weg van een verzoek van de GET te omvatten behoren.

**API-indeling**

```http
GET /companies/{COMPANY_ID}/properties
```

| Parameter | Beschrijving |
| --- | --- |
| `COMPANY_ID` | De `id` van het bedrijf dat eigenaar is van de eigenschappen die u wilt vermelden. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde eigenschappen worden gefiltreerd gebaseerd op de volgende attributen:<ul><li>`copying`</li><li>`created_at`</li><li>`enabled`</li><li>`name`</li><li>`platform`</li><li>`token`</li><li>`updated_at`</li></ul>Zie de gids op [het filtreren reacties](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van eigenschappen voor het gespecificeerde bedrijf terug.

```json
{
  "data": [
    {
      "id": "PR29e066628dcf4ba0a16780b2e339821c",
      "type": "properties",
      "attributes": {
        "created_at": "2020-12-14T17:51:28.215Z",
        "enabled": true,
        "name": "Kessel Example Property",
        "updated_at": "2020-12-14T17:51:28.215Z",
        "platform": "web",
        "development": false,
        "token": "30a138ca7f5b",
        "domains": [
          "example.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments",
        "extensions": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions",
        "rules": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules",
        "self": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    },
    {
      "id": "PR0c559a62480142a7b9be4a118d1a0448",
      "type": "properties",
      "attributes": {
        "created_at": "2020-08-14T15:29:34.241Z",
        "enabled": true,
        "name": "new prop",
        "updated_at": "2020-08-14T15:29:34.241Z",
        "platform": "web",
        "development": true,
        "token": "b6cee01dedb7",
        "domains": [
          "google.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments",
        "extensions": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions",
        "rules": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules",
        "self": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## Een eigenschap opzoeken {#lookup}

U kunt een eigenschap opzoeken door de id ervan op te geven in het pad van een GET-aanvraag.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de eigenschap.

```json
{
  "data": {
    "id": "PR48ade10e6acf4385ba96214e9f5d31e1",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:18.725Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:18.725Z",
      "platform": "web",
      "development": false,
      "token": "c54ba5e843e6",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments",
      "extensions": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions",
      "rules": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules",
      "self": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Een eigenschap maken {#create}

U kunt een nieuwe eigenschap maken door een POST-aanvraag in te dienen.

**API-indeling**

```http
POST /company/{COMPANY_ID}/properties
```

| Parameter | Beschrijving |
| --- | --- |
| `COMPANY_ID` | De `id` van het bedrijf waarop u de eigenschap definieert. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een nieuwe eigenschap voor de opgegeven eigenschap gemaakt. De vraag associeert ook het bezit met een bestaande uitbreiding door het `relationships` bezit. Zie de gids op [relaties](../guides/relationships.md) voor meer informatie.

```shell
curl -X POST \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Example Property",
            "platform": "web"
            "domains": [
              "example.com"
            ],
            "privacy": "gdpr",
            "rule_component_sequencing_enabled": false,
            "ssl_enabled": false,
            "undefined_vars_return_empty": true
          },
          "type": "properties"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.name` | **(Vereist)** Een leesbare naam voor de eigenschap. |
| `attributes.platform` | **(Vereist)** Het platform voor de eigenschap. Kan `web` zijn voor wegeigenschappen of `mobile` of `edge` voor mobiele eigenschappen. |
| `attributes.domains` | **(Vereist voor wegeigenschappen)** Een array van URL-domeinen voor de eigenschap. |
| `attributes.development` | Een Booleaanse waarde die aangeeft of dit een ontwikkeleigenschap is. |
| `attributes.privacy` | Een tekenreeks die kan worden gebruikt om te verwijzen naar overwegingen met betrekking tot privacy voor de eigenschap. |
| `attributes.rule_component_sequencing_enabled` | Een Booleaanse waarde voor of regelcomponentsequencing moet worden ingeschakeld voor deze eigenschap. |
| `attributes.ssl_enabled` | Een Booleaanse waarde die aangeeft of SSL (Secure Sockets Layer) moet worden ingeschakeld voor deze eigenschap. |
| `attributes.undefined_vars_return_empty` | Een Booleaanse waarde die aangeeft of ongedefinieerde variabelen als leeg moeten worden geretourneerd voor deze eigenschap. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `properties` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de nieuwe eigenschap.

```json
{
  "data": {
    "id": "PR505e39de0d0042d1b22321e7767edb4d",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:31:31.579Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:31:31.579Z",
      "platform": "web",
      "development": false,
      "token": "a969ffc6f872",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments",
      "extensions": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions",
      "rules": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules",
      "self": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Een eigenschap bijwerken {#update}

U kunt een eigenschap bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag.

**API-indeling**

```http
PATCH /properties/{PROPERTY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek worden `name` en `domains` bijgewerkt voor een bestaande eigenschap.

```shell
curl -X PUT \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Property B",
            "domains": [
              "example.com"
            ]
          },
          "id": "PR541dbb24bad54dceb04710d7a9e7a740",
          "type": "properties"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de eigenschap moeten worden bijgewerkt. De volgende kenmerken kunnen worden bijgewerkt voor een eigenschap: <ul><li>`development`</li><li>`domains`</li><li>`name`</li><li>`platform`</li><li>`privacy`</li><li>`rule_component_sequencing_enabled`</li><li>`ssl_enabled`</li><li>`undefined_vars_return_empty`</li></ul> |
| `id` | De `id` van de eigenschap die u wilt bijwerken. Dit zou de `{PROPERTY_ID}` waarde moeten aanpassen die in de verzoekweg wordt verstrekt. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `properties` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de bijgewerkte eigenschap.

```json
{
  "data": {
    "id": "PR541dbb24bad54dceb04710d7a9e7a740",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:37.386Z",
      "enabled": true,
      "name": "Kessel Property B",
      "updated_at": "2020-12-14T17:51:43.062Z",
      "platform": "web",
      "development": false,
      "token": "3f2d8630a8d3",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments",
      "extensions": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions",
      "rules": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules",
      "self": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Een eigenschap verwijderen

U kunt een eigenschap verwijderen door de id ervan op te nemen in het pad van een DELETE-aanvraag.

**API-indeling**

```http
DELETE /properties/{PROPERTY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responstekst om aan te geven dat de eigenschap is verwijderd.

## Notities voor een eigenschap beheren {#notes}

Eigenschappen zijn &#39;opmerkelijke&#39; bronnen, wat betekent dat u op tekst gebaseerde notities kunt maken en ophalen voor elke afzonderlijke bron. Zie [Notitie eindpuntgids](./notes.md) voor meer informatie over hoe te om nota&#39;s voor eigenschappen en andere compatibele middelen te beheren.

## Gerelateerde bronnen voor een eigenschap ophalen {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een bezit terug te winnen. Wanneer [het opzoeken van een bezit](#lookup), zijn deze verhoudingen vermeld onder het `relationships` bezit.

Zie de [relatiehandleiding](../guides/relationships.md) voor meer informatie over relaties in de Reactor-API.

### Verwante callbacks voor een eigenschap weergeven {#callbacks}

U kunt van [callbacks](./callbacks.md) een lijst maken die op een bezit door `/callbacks` aan de weg van een raadplegingsverzoek toe te voegen worden geregistreerd.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van het bezit waarvan callbacks u wilt een lijst maken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van callbacks terug die door het gespecificeerde bezit worden bezeten.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante gegevenselementen weergeven voor een eigenschap {#data-elements}

U kunt een lijst maken van [gegevenselementen](./data-elements.md) die door een bezit door `/data_elements` aan de weg van een raadplegingsverzoek toe te voegen worden bezeten.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/data_elements
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de gegevenselementen wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met gegevenselementen die het eigendom zijn van de opgegeven eigenschap.

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante omgevingen weergeven voor een eigenschap {#environments}

U kunt een lijst maken van [milieu&#39;s](./environments.md) die door een bezit door `/environments` aan de weg van een raadplegingsverzoek toe te voegen worden bezeten.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/environments
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de omgevingen wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met omgevingen die eigendom zijn van de opgegeven eigenschap.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante extensies weergeven voor een eigenschap {#extensions}

U kunt een lijst maken van [extensions](./extensions.md) die door een bezit door `/extensions` aan de weg van een raadplegingsverzoek toe te voegen worden bezeten.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/extensions
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de extensies wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met extensies die eigendom zijn van de opgegeven eigenschap.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante hosts voor een eigenschap weergeven {#hosts}

U kunt van [hosts](./hosts.md) een lijst maken die door een bezit door `/hosts` aan de weg van een raadplegingsverzoek toe te voegen worden gebruikt.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de hosts wilt vermelden. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van gastheren terug die door het gespecificeerde bezit worden gebruikt.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante regels voor een eigenschap weergeven {#rules}

U kunt van [rules](./rules.md) een lijst maken die door een bezit door `/rules` aan de weg van een raadplegingsverzoek toe te voegen worden gebruikt.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/rules
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de regels wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van regels terug die door een gespecificeerde bezit worden gebruikt.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Verwante onderneming opzoeken voor een onroerend goed {#company}

U kunt het bedrijf opzoeken dat een bezit door `/company` aan de weg van een raadplegingsverzoek toe te voegen bezit.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}/company
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van het bezit waarvan bedrijf u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84/company \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert de details van het gespecificeerde bedrijf van het bezit terug.

```json
{
  "data": {
    "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.711Z",
      "name": "Reactor QE",
      "org_id": "08364A825824E04F0A494115@AdobeOrg",
      "updated_at": "2020-08-13T17:13:30.711Z",
      "token": "f9fd106ab399",
      "cjm_enabled": true,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "properties": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties",
        "manage_app_configurations"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ]
      }
    }
  }
}
```
