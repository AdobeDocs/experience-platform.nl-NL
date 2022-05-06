---
title: Extensies, eindpunt
description: Leer hoe te om vraag aan het /extensions eindpunt in Reactor API te maken.
exl-id: cc02b2aa-d107-463a-930c-5a9fcc5b4a5a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# Extensies, eindpunt

In de Reactor-API vertegenwoordigt een extensie de geïnstalleerde instantie van een [extensiepakket](./extension-packages.md). Met een extensie worden de functies die door een extensiepakket worden gedefinieerd, beschikbaar gemaakt voor een [eigenschap](./properties.md). Deze functies worden gebruikt bij het maken van [extensions](./data-elements.md) en [regelcomponenten](./rule-components.md).

Een extensie behoort tot exact één eigenschap. Een eigenschap kan vele extensies hebben, maar niet meer dan één geïnstalleerde instantie van een opgegeven extensiepakket.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Een lijst met extensies ophalen {#list}

U kunt een lijst met extensies voor een eigenschap ophalen door een GET-aanvraag in te dienen.

**API-indeling**

```http
GET properties/{PROPERTY_ID}/extensions
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de extensies wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Met behulp van queryparameters kunnen weergegeven extensies worden gefilterd op basis van de volgende kenmerken:<ul><li>`created_at`</li><li>`dirty`</li><li>`display_name`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li><li>`version`</li></ul>Zie de handleiding op [filterreacties](../guides/filtering.md) voor meer informatie .

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met extensies die zijn gedefinieerd onder de opgegeven eigenschap.

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

## Een extensie opzoeken {#lookup}

U kunt een extensie opzoeken door de id op te geven in het pad van een GET-aanvraag.

>[!NOTE]
>
>Wanneer extensies worden verwijderd, worden ze gemarkeerd als verwijderd in het systeem, maar worden ze niet daadwerkelijk verwijderd. Het is daarom mogelijk een verwijderde extensie op te halen. Verwijderde extensies kunnen worden geïdentificeerd door de aanwezigheid van een `deleted_at` eigenschap in de `meta` van de geretourneerde extensiegegevens.

**API-indeling**

```http
GET /extensions/{EXTENSION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_ID` | De `id` van de extensie die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de extensie.

```json
{
  "data": {
    "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:40:09.823Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:40:09.823Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/property"
        },
        "data": {
          "id": "PR2254ac6a096c4df38508700093d3e153",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/origin"
        },
        "data": {
          "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR2254ac6a096c4df38508700093d3e153",
      "origin": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "self": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Een extensie maken of bijwerken {#create}

Extensies worden gemaakt door te verwijzen naar een [extensiepakket](./extension-packages.md) en het toevoegen van de geïnstalleerde extensie aan een eigenschap. Wanneer de installatietaak is voltooid, wordt een antwoord geretourneerd dat aangeeft of de extensie is geïnstalleerd.

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/extensions
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap waarop u de extensie wilt installeren. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "example-package::extensionConfiguration::config",
            "enabled": true,
            "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
          },
          "relationships": {
            "extension_package": {
              "data": {
                "id": "EP75db2452065b44e2b8a38ca883ce369a",
                "type": "extension_packages"
              }
            }
          },
          "type": "extensions"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `relationships.extension_package` | **(Vereist)** Een object dat verwijst naar de id van het extensiepakket dat wordt geïnstalleerd. |
| `attributes.delegate_descriptor_id` | Als uw extensie aangepaste instellingen nodig heeft, is ook een id voor de gedelegeerde descriptor vereist. Zie de handleiding op [id&#39;s gedelegeerde descriptor](../guides/delegate-descriptor-ids.md) voor meer informatie . |
| `attributes.enabled` | Een Booleaanse waarde die aangeeft of de extensie is ingeschakeld. |
| `attributes.settings` | A settings JSON object represented as a string. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de zojuist gemaakte extensie.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Een extensie reviseren {#revise}

U kunt een extensie herzien door de id ervan op te nemen in het pad van een PATCH-aanvraag.

**API-indeling**

```http
PATCH /extensions/{EXTENSION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_ID` | De `id` van de extensie die u wilt herzien. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Zoals met [een extensie maken](#create), moet een lokale versie van het herziene pakket via formuliergegevens worden geüpload.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "enabled": false,
          },
          "meta": {
            "action": "revise"
          },
          "id": "EX85509bc7baea4f8599bc44024ed3f110",
          "type": "extensions"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | De kenmerken die u wilt herzien. Voor extensies kunt u hun `delegate_descriptor_id`, `enabled`, en `settings` kenmerken. |
| `meta.action` | Moet worden opgenomen met een waarde van `revise` bij een herziening. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord geeft de details van de herziene verlenging terug, met zijn `meta.latest_revision_number` eigenschap verhoogd met 1.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": false,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 2
    }
  }
}
```

## Een extensie verwijderen {#private-release}

U kunt een extensie verwijderen door de id ervan op te nemen in het pad van een DELETE-aanvraag.

**API-indeling**

```http
DELETE /extensions/{EXTENSION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_ID` | De `id` van de extensie die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responstekst om aan te geven dat de extensie is verwijderd.

## Notities voor een extensie beheren {#notes}

Extensies zijn &#39;opmerkelijke&#39; bronnen, wat betekent dat u op tekst gebaseerde notities kunt maken en ophalen voor elke afzonderlijke bron. Zie de [leidraad voor notitiepunten](./notes.md) voor meer informatie over hoe u notities voor extensies en andere compatibele bronnen kunt beheren.

## Gerelateerde bronnen ophalen voor een extensie {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een uitbreiding terug te winnen. Wanneer [zoeken naar een extensie](#lookup), worden deze relaties vermeld in het `relationships` eigenschap.

Zie de [relatiehulplijn](../guides/relationships.md) voor meer informatie over relaties in de Reactor-API.

### Verwante bibliotheken weergeven voor een extensie {#libraries}

U kunt de bibliotheken die een extensie gebruiken, weergeven door ze toe te voegen `/libraries` naar het pad van een opzoekverzoek.

**API-indeling**

```http
GET  /extensions/{EXTENSION_ID}/libraries
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXTENSION_ID}` | De `id` van de extensie waarvan u de bibliotheken wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met bibliotheken die de opgegeven extensie gebruiken.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### Verwante revisies weergeven voor een extensie {#revisions}

U kunt de vorige revisies van een extensie weergeven door deze toe te voegen `/revisions` naar het pad van een opzoekverzoek.

**API-indeling**

```http
GET  /extensions/{EXTENSION_ID}/revisions
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXTENSION_ID}` | De `id` van de extensie waarvan u de revisies wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met revisies voor de opgegeven extensie.

```json
{
  "data": [
    {
      "id": "EXbfcca9f3ce9d40318b9115159a951e09",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.023Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:41:09.023Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "EXd485e07fb3d3429b997768ae40de8f02",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.002Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:41:09.002Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
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
      "total_count": 2
    }
  }
}
```

### Het verwante extensiepakket voor een extensie opzoeken {#extension}

U kunt het extensiepakket opzoeken waarop een extensie is gebaseerd door het toevoegen `/extension_package` naar het pad van een GET-aanvraag.

**API-indeling**

```http
GET  /extensions/{EXTENSION_ID}/extension_package
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXTENSION_ID}` | De `id` van de extensie waarvan u de extensie wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van het extensiepakket waarop de opgegeven extensie is gebaseerd. De voorbeeldreactie hieronder is afgebroken voor de ruimte.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

### De verwante oorsprong opzoeken voor een extensie {#origin}

U kunt de oorsprong van een extensie opzoeken door deze toe te voegen `/origin` naar het pad van een GET-aanvraag. De oorsprong van een extensie is de vorige revisie die is bijgewerkt om de huidige revisie te maken.

**API-indeling**

```http
GET  /extensions/{EXTENSION_ID}/origin
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXTENSION_ID}` | De `id` van de extensie waarvan u de oorsprong wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de oorsprong van de opgegeven extensie.

```json
{
  "data": {
    "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:41:21.397Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:41:21.397Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/property"
        },
        "data": {
          "id": "PR88d6b8ee423b44a49de1dee26391e25b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/origin"
        },
        "data": {
          "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR88d6b8ee423b44a49de1dee26391e25b",
      "origin": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "self": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### De verwante eigenschap voor een extensie opzoeken {#property}

U kunt de eigenschap die eigenaar is van een extensie opzoeken door deze toe te voegen `/property` naar het pad van een GET-aanvraag.

**API-indeling**

```http
GET  /extensions/{EXTENSION_ID}/property
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXTENSION_ID}` | De `id` van de extensie waarvan u de eigenschap wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de eigenschap die eigenaar is van de opgegeven extensie.

```json
{
  "data": {
    "id": "PR96fd3675be144ddc8c4540d79430355a",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:06.993Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:06.993Z",
      "platform": "web",
      "development": false,
      "token": "bf75a40b3c34",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments",
      "extensions": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions",
      "rules": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules",
      "self": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a"
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
