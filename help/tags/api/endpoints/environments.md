---
title: Environments endpoint
description: Learn how to make calls to the /environments endpoint in the Reactor API.
exl-id: 4c22f799-8338-4cf0-980a-3900d725ab5d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---

# Environments endpoint

Wanneer een [bibliotheek](./libraries.md) wordt gecompileerd in een [build](./builds.md) in de Reactor-API is de exacte inhoud van de build afhankelijk van de omgevingsinstellingen en de bronnen in de bibliotheek. De omgeving bepaalt met name het volgende:

1. **Doel**: De plaats waar u de bouwstijl wilt worden opgesteld. Dit wordt bepaald door een [host](./hosts.md) voor het milieu.
1. **Archief**: U kunt ervoor kiezen om de build op te halen als een implementeerbare set bestanden of om de build op te slaan in een archiefindeling. Dit wordt gecontroleerd door de `archive` milieu.

Het doel en archiefformaat dat door het milieu wordt gevormd verandert hoe u in uw toepassing van verwijzingen voorziet bouwt (die verwijzing is [code insluiten](../../ui/publishing/environments.md#embed-code)). If you make any changes to destination or file format, you must make a matching update to your application to use the new reference.

De milieu&#39;s komen in drie types (of stadia), met elk type dat een verschillende grens van het totale aantal heeft u kunt hebben:

| Omgevingstype | Toegestaan nummer |
| --- | --- |
| Ontwikkeling | (Geen limiet) |
| Staging | Eén |
| Productie | Eén |

{style=&quot;table-layout:auto&quot;}

Deze omgevingstypen gedragen zich op dezelfde manier, maar worden in verschillende stadia van de [publicatieworkflow voor tags](../../ui/publishing/publishing-flow.md).

Een omgeving behoort tot precies één [eigenschap](./properties.md).

Zie de sectie over [omgevingen](../../ui/publishing/environments.md) in de publicatiedocumenten.

## Aan de slag

The endpoint used in this guide is part of the [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Een lijst met omgevingen ophalen {#list}

U kunt een lijst van milieu&#39;s voor een bezit terugwinnen door identiteitskaart van het bezit in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}/environments
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die eigenaar is van de omgevingen. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde milieu&#39;s op de volgende attributen worden gefiltreerd:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>See the guide on [filtering responses](../guides/filtering.md) for more information.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met omgevingen voor de opgegeven eigenschap.

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

## Een omgeving opzoeken {#lookup}

U kunt een omgeving opzoeken door zijn id op te geven in het pad van een GET-aanvraag.

**API-indeling**

```http
GET /environments/{ENVIRONMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `ENVIRONMENT_ID` | De `id` van de omgeving die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie retourneert de details van de omgeving.

```json
{
  "data": {
    "id": "ENb0c1fbfdc1fd4b8593bfd269f827b3e6",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:30.378Z",
      "library_path": "f9fd106ab399/2f67fccade5e",
      "library_name": "launch-4436c89f6839-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4436c89f6839-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.min.js"
          ],
          "license_path": "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
        },
        {
          "library_name": "launch-4436c89f6839-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:30.378Z",
      "status": "succeeded",
      "token": "4436c89f6839"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/host",
          "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/relationships/host"
        },
        "data": {
          "id": "HTecb76453c8284f84a3c55fe981b5e6c9",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/property"
        },
        "data": {
          "id": "PRadbee4fb64754081a945ed2a5b66627a",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRadbee4fb64754081a945ed2a5b66627a",
      "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Een omgeving maken {#create}

U kunt een nieuwe omgeving maken door een POST aan te vragen.

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/environments
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de [eigenschap](./properties.md) dat u de omgeving definieert onder. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een nieuwe omgeving voor de opgegeven eigenschap gemaakt. De vraag associeert ook het milieu met een bestaande gastheer door `relationships` eigenschap. Zie de handleiding op [relaties](../guides/relationships.md) voor meer informatie .

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Development Environment A",
            "archive": true,
            "archive_passphrase": "pass12345",
            "path": "/development-a",
            "stage": "development"
          },
          "relationships": {
            "host": {
              "data": {
                "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
                "type": "hosts"
              }
            }
          },
          "type": "environments"
        }
      }'
```

| Property | Beschrijving |
| --- | --- |
| `attributes.name` | **(Required)** A human-readable name for the environment. |
| `attributes.archive` | A boolean value indicating whether the build she be in archive format. |
| `attributes.archive_passphrase` | Een tekenreekswachtwoord waarmee het archiefbestand kan worden ontgrendeld. |
| `attributes.path` | Een pad vanaf de host-URL voor de omgeving. |
| `attributes.stage` | Het stadium voor het milieu (ontwikkeling, staging of productie). |
| `id` | De `id` van de omgeving die u wilt bijwerken. Dit moet overeenkomen met de `{ENVIRONMENT_ID}` waarde opgegeven in het aanvraagpad. |
| `type` | The type of resource being updated. Voor dit eindpunt, moet de waarde zijn `environments`. |

{style=&quot;table-layout:auto&quot;}

**Response**

Een geslaagde reactie retourneert de details van de nieuwe omgeving.

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:31:57.857Z",
      "library_path": "f9fd106ab399/bd007122e3e3",
      "library_name": "launch-4d5a31f6ca53-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4d5a31f6ca53-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js"
          ],
          "license_path": "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
        },
        {
          "library_name": "launch-4d5a31f6ca53-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:31:57.857Z",
      "status": "succeeded",
      "token": "4d5a31f6ca53"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/host",
          "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/relationships/host"
        },
        "data": {
          "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa41874e4d1604efd9c3c67d7a123f4c6",
      "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Een omgeving bijwerken {#update}

U kunt een omgeving bijwerken door de bijbehorende id op te nemen in het pad van een PATCH-aanvraag.

**API-indeling**

```http
PATCH /environments/{ENVIRONMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `ENVIRONMENT_ID` | De `id` van de omgeving die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

De volgende aanvraag werkt de `name` voor een bestaande omgeving.

```shell
curl -X PATCH \
  https://reactor.adobe.io/environments/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Environment Name"
          },
          "id": "ENeb00d8f62d244732bd27765301b1410f",
          "type": "environments"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de omgeving moeten worden bijgewerkt. De volgende omgevingskenmerken kunnen worden bijgewerkt: <ul><li>`archive`</li><li>`archive_passphrase`</li><li>`include_debug_library`</li><li>`name`</li><li>`path`</li></ul> Zie de voorbeeldvraag voor [creëren van een omgeving](#create) voor een lijst van kenmerken en het gebruik ervan. |
| `id` | De `id` van de omgeving die u wilt bijwerken. Dit moet overeenkomen met de `{ENVIRONMENT_ID}` waarde opgegeven in het aanvraagpad. |
| `type` | The type of resource being updated. Voor dit eindpunt, moet de waarde zijn `environments`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de bijgewerkte omgeving.

```json
{
  "data": {
    "id": "ENeb00d8f62d244732bd27765301b1410f",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:40.608Z",
      "library_path": "f9fd106ab399/1eb59e88f015",
      "library_name": "launch-caa955ee58ff-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-caa955ee58ff-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.min.js"
          ],
          "license_path": "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
        },
        {
          "library_name": "launch-caa955ee58ff-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
          ]
        }
      ],
      "name": "New environment name",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:41.210Z",
      "status": "succeeded",
      "token": "caa955ee58ff"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host",
          "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/relationships/host"
        },
        "data": {
          "id": "HT7ea0b7c5c556476bafae8240da2d657d",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property"
        },
        "data": {
          "id": "PR558b6514e529409fa740a34e5f974dd8",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR558b6514e529409fa740a34e5f974dd8",
      "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Een omgeving verwijderen

U kunt een omgeving verwijderen door de bijbehorende id op te nemen in het pad van een DELETE-aanvraag.

**API-indeling**

```http
DELETE /environments/{ENVIRONMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `ENVIRONMENT_ID` | De `id` van de omgeving die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responsstructuur, wat aangeeft dat de omgeving is verwijderd.

## Gerelateerde bronnen ophalen voor een omgeving {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een milieu terug te winnen. Wanneer [een omgeving opzoeken](#lookup), worden deze relaties vermeld in het `relationships` eigenschap.

See the [relationships guide](../guides/relationships.md) for more information on relationships in the Reactor API.

### Verwante builds voor een omgeving weergeven {#builds}

U kunt de builds die een omgeving gebruiken, weergeven door ze toe te voegen `/builds` naar het pad van een opzoekverzoek.

**API-indeling**

```http
GET  /environments/{ENVIRONMENT_ID}/builds
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENVIRONMENT_ID}` | De `id` van de omgeving waarvan u de builds wilt vermelden. |

{style=&quot;table-layout:auto&quot;}

**Request**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

A successful response returns a list of builds that use the specified environment.

```json
{
  "data": [
    {
      "id": "BL775f919553aa4c6c8116cbf1da8baec8",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:43.113Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:43.113Z",
        "token": "983989bcdad4"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/environment"
          },
          "data": {
            "id": "ENd8b1aee9d1674e7aa6135752ce839f82",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/library"
          },
          "data": {
            "id": "LB9bca25483e0849a089524c5ca655f2fe",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/property"
          },
          "data": {
            "id": "PRbe32d7f41b2741ecae1c06f6fd2d3906",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/ENd8b1aee9d1674e7aa6135752ce839f82",
        "library": "https://reactor.adobe.io/libraries/LB9bca25483e0849a089524c5ca655f2fe",
        "self": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/launch-d481f2d29bd0-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/983989bcdad4/launch-d481f2d29bd0-development.min.js",
        "archive": false,
        "host_type_of": "akamai"
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

### De verwante host opzoeken voor een omgeving {#host}

U kunt de host opzoeken die een omgeving gebruikt door deze toe te voegen `/host` naar het pad van een GET-aanvraag.

>[!NOTE]
>
>U kunt het hostrelatieobject zelf opzoeken via een [afzonderlijke oproep](#host-relationship).

**API-indeling**

```http
GET  /environments/{ENVIRONMENT_ID}/host
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENVIRONMENT_ID}` | The `id` of the environment whose host you want to look up. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

A successful response returns the details of the host that uses the specified environment.

```json
{
  "data": {
    "id": "HT621241cf4fbb4f7da5b6415ee1b15ac0",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:43:05.382Z",
      "server": null,
      "name": "Example Akamai Host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:43:05.382Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0/property"
        },
        "data": {
          "id": "PR50586546f7764fc59997342b8ff7647c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR50586546f7764fc59997342b8ff7647c",
      "self": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0"
    }
  }
}
```

### De verwante bibliotheek opzoeken voor een omgeving {#library}

U kunt de bibliotheek die een omgeving gebruikt, opzoeken door deze toe te voegen `/library` naar het pad van een GET-aanvraag.

**API format**

```http
GET  /environments/{ENVIRONMENT_ID}/library
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENVIRONMENT_ID}` | De `id` van de omgeving waarvan u de bibliotheek wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord retourneert de details van de bibliotheek die de opgegeven omgeving gebruikt.

```json
{
  "data": {
    "id": "LB6ce27064ebe04ceab3d6942e9de563db",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:50:06.695Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:50:06.695Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/builds"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/environment",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/environment"
        },
        "data": {
          "id": "EN3287da6fafa143c289afd2f578b4d33d",
          "type": "environments"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/extensions",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/rules",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/property"
        },
        "data": {
          "id": "PR95eaa16990c745a78f5bee8439fe4c34",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR95eaa16990c745a78f5bee8439fe4c34",
      "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

### Verwante eigenschap opzoeken voor een omgeving {#property}

U kunt de eigenschap die eigenaar is van een omgeving opzoeken door deze toe te voegen `/property` naar het pad van een GET-aanvraag.

**API-indeling**

```http
GET  /environments/{ENVIRONMENT_ID}/property
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENVIRONMENT_ID}` | De `id` van de omgeving waarvan u de eigenschap wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de eigenschap die eigenaar is van de opgegeven omgeving.

```json
{
  "data": {
    "id": "PR7688dba9f1384507bbd20f10947536f2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:55.254Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:55.254Z",
      "platform": "web",
      "development": false,
      "token": "9611419d84a4",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments",
      "extensions": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions",
      "rules": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules",
      "self": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2"
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
