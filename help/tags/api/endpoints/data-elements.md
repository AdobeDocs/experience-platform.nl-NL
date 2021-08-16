---
title: Gegevenselementen, eindpunt
description: Leer hoe te om vraag aan het /data_elements eindpunt in Reactor API te maken.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 1%

---

# Gegevenselementen, eindpunt

Een gegevenselement werkt als een variabele die naar een belangrijk stuk gegevens binnen uw toepassing verwijst. Gegevenselementen worden gebruikt binnen [regels](./rules.md) en [extension](./extensions.md) configuraties. Wanneer een regel wordt geactiveerd bij uitvoering in een browser of toepassing, wordt de waarde van het gegevenselement opgelost en gebruikt binnen de regel. De elementen van gegevens functioneren het zelfde voor uitbreidingsconfiguraties.

Als u meerdere gegevenselementen tegelijk gebruikt, resulteert dit in een gegevenswoordenboek of een gegevenskaart. Dit woordenboek vertegenwoordigt de gegevens die Adobe Experience Platform kent en kan gebruiken.

Een gegevenselement behoort tot exact één [eigenschap](./properties.md). Een eigenschap kan veel gegevenselementen bevatten.

Voor meer algemene informatie over gegevenselementen en hun gebruik in markeringen, zie [gegevenselementengids](../../ui/managing-resources/data-elements.md) in de documentatie UI.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Een lijst met gegevenselementen ophalen {#list}

U kunt een lijst van gegevenselementen voor een bezit terugwinnen door identiteitskaart van het bezit in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}/data_elements
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die eigenaar is van de gegevenselementen. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde gegevenselementen worden gefiltreerd gebaseerd op de volgende attributen:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Zie de gids op [het filtreren reacties](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met gegevenselementen voor de opgegeven eigenschap.

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

## Een gegevenselement opzoeken {#lookup}

U kunt een gegevenselement opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

>[!NOTE]
>
>Wanneer gegevenselementen worden verwijderd, worden ze gemarkeerd als verwijderd, maar worden ze niet daadwerkelijk uit het systeem verwijderd. Daarom is het mogelijk om een geschrapt gegevenselement op te zoeken. Verwijderde gegevenselementen kunnen worden geïdentificeerd door de aanwezigheid van een `data.meta.deleted_at`-kenmerk.

**API-indeling**

```http
GET /data_elements/{DATA_ELEMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `DATA_ELEMENT_ID` | De `id` van het gegevenselement dat u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van het gegevenselement.

```json
{
  "data": {
    "id": "DE8097636264104451ac3a18c95d5ff833",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:35:54.956Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:35:54 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:35:54.956Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/property"
        },
        "data": {
          "id": "PRa5621686159f44c880557e12af412a95",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/origin"
        },
        "data": {
          "id": "DE8097636264104451ac3a18c95d5ff833",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/extension"
        },
        "data": {
          "id": "EX085a465793b54be39b5408d13b50b46e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension"
        },
        "data": {
          "id": "EXf9a32699efde42e9b9410b43bd660848",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa5621686159f44c880557e12af412a95",
      "origin": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "self": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "extension": "https://reactor.adobe.io/extensions/EX085a465793b54be39b5408d13b50b46e"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Een data-element maken {#create}

U kunt een nieuw gegevenselement tot stand brengen door een verzoek van de POST te doen.

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/data_elements
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de [eigenschap](./properties.md) die u het gegevenselement onder definieert. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met de volgende aanvraag wordt een nieuw gegevenselement voor de opgegeven eigenschap gemaakt. De vraag associeert ook het gegevenselement met een bestaande uitbreiding door het `relationships` bezit. Zie de gids op [relaties](../guides/relationships.md) voor meer informatie.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Data Element 2020-12-14 17:33:21 +0000",
            "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
            "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}",
            "default_value": "general_label",
            "enabled": true,
            "force_lower_case": true,
            "clean_text": true,
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
                "type": "extensions"
              }
            }
          },
          "type": "data_elements"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.name` | **(Vereist)** Een leesbare naam voor het gegevenselement. |
| `attributes.delegate_descriptor_id` | **(Vereist)** Een opgemaakte tekenreeks die het gegevenselement koppelt aan een extensiepakket. Alle gegevenselementen moeten met een uitbreidingspakket worden geassocieerd wanneer zij eerst worden gecreeerd, aangezien elk uitbreidingspakket de compatibele types voor zijn elementen van gedelegeerde gegevens, evenals hun voorgenomen gedrag bepaalt. Zie de gids op [afgevaardigde beschrijver IDs](../guides/delegate-descriptor-ids.md) voor meer informatie. |
| `attributes.settings` | A settings JSON object represented as a string. |
| `attributes.default_value` | Een standaardwaarde die moet worden geretourneerd als het gegevenselement `undefined` oplevert. |
| `attributes.enabled` | Een booleaanse waarde die aangeeft of het gegevenselement is ingeschakeld. |
| `attributes.force_lower_case` | Een booleaanse waarde die aangeeft of de waarde van het gegevenselement moet worden omgezet in kleine letters voordat deze wordt opgeslagen. |
| `attributes.clean_text` | Een booleaanse waarde die aangeeft of voorafgaande en navolgende witruimte uit de waarde van het gegevenselement moet worden verwijderd voordat deze wordt opgeslagen. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `data_elements` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe gegevenselement.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Een gegevenselement bijwerken {#update}

U kunt een gegevenselement bijwerken door zijn identiteitskaart in de weg van een PATCH verzoek te omvatten.

**API-indeling**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `DATA_ELEMENT_ID` | De `id` van het gegevenselement dat u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt `name` bijgewerkt voor een bestaand gegevenselement.

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor het gegevenselement moeten worden bijgewerkt. Alle kenmerken van gegevenselementen kunnen worden bijgewerkt. Zie de voorbeeldvraag voor [het creëren van een gegevenselement](#create) voor een lijst van attributen en hun gebruiksgeval. |
| `id` | De `id` van het gegevenselement dat u wilt bijwerken. Dit zou de `{DATA_ELEMENT_ID}` waarde moeten aanpassen die in de verzoekweg wordt verstrekt. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `data_elements` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van het bijgewerkte gegevenselement.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Een gegevenselement herzien {#revise}

Wanneer u een gegevenselement bijwerkt, wordt een nieuwe revisie van het gegevenselement gecreeerd met de huidige (hoofd) revisie. Elke revisie van een gegevenselement zal zijn eigen identiteitskaart hebben. Het oorspronkelijke gegevenselement kan worden ontdekt door een oorsprongskoppeling.

U kunt een gegevenselement herzien door een `meta.action` bezit van een waarde van `revise` in het lichaam van een verzoek van PATCH te voorzien.

**API-indeling**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `DATA_ELEMENT_ID` | De `id` van het gegevenselement dat u wilt herzien. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "meta": {
            "action": "revise"
          },
          "id": "DE7d7284657ee540ee8f402277860e9f8a",
          "type": "data_elements"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor het gegevenselement moeten worden bijgewerkt. Alle kenmerken van gegevenselementen kunnen worden bijgewerkt. Zie de voorbeeldvraag voor [het creëren van een gegevenselement](#create) voor een lijst van attributen en hun gebruiksgeval. |
| `meta.action` | Wanneer deze eigenschap is opgenomen met de waarde `revise`, geeft deze aan dat een nieuwe revisie voor het gegevenselement moet worden gemaakt. |
| `id` | De `id` van het gegevenselement dat u wilt herzien. Dit zou de `{DATA_ELEMENT_ID}` waarde moeten aanpassen die in de verzoekweg wordt verstrekt. |
| `type` | Het type bron dat wordt herzien. Voor dit eindpunt, moet de waarde `data_elements` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert de details van de nieuwe herziening voor het gegevenselement terug, zoals die door de verhoogde `meta.latest_revision_number` attributen wordt vermeld.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Een gegevenselement verwijderen

U kunt een gegevenselement schrappen door zijn identiteitskaart in de weg van een verzoek van de DELETE te omvatten.

**API-indeling**

```http
DELETE /data_elements/{DATA_ELEMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `DATA_ELEMENT_ID` | De `id` van het gegevenselement dat u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responsiehoofdtekst om aan te geven dat het gegevenselement is verwijderd.

## Notities beheren voor een gegevenselement {#notes}

Gegevenselementen zijn &#39;opmerkelijke&#39; bronnen, wat betekent dat u op tekst gebaseerde notities kunt maken en ophalen voor elke afzonderlijke bron. Zie [Notitie eindpuntgids](./notes.md) voor meer informatie over hoe te om nota&#39;s voor gegevenselementen en andere compatibele middelen te beheren.

## Gerelateerde bronnen voor een gegevenselement ophalen {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een gegevenselement terug te winnen. Wanneer [een gegevenselement](#lookup) omhoog kijkt, zijn deze verhoudingen vermeld onder het `relationships` bezit.

Zie de [relatiehandleiding](../guides/relationships.md) voor meer informatie over relaties in de Reactor-API.

### Verwante bibliotheken weergeven voor een gegevenselement {#libraries}

U kunt een lijst maken van de bibliotheken die een gegevenselement gebruiken door `/libraries` aan de weg van een raadplegingsverzoek toe te voegen.

**API-indeling**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/libraries
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_ELEMENT_ID}` | De `id` van het gegevenselement waarvan bibliotheken u wilt een lijst maken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met bibliotheken die het opgegeven gegevenselement gebruiken.

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

### Verwante revisies weergeven voor een gegevenselement {#revisions}

U kunt een lijst maken van de vorige revisies van een gegevenselement door `/revisions` aan de weg van een raadplegingsverzoek toe te voegen.

**API-indeling**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/revisions
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_ELEMENT_ID}` | De `id` van het gegevenselement waarvan revisies u wilt vermelden. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met revisies voor het opgegeven gegevenselement.

```json
{
  "data": [
    {
      "id": "DEaeceb5164d494c768c18e37ec6f3b091",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:06.488Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:37:06.488Z",
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
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "DE5172417ff56e43d2a99ca149021bf65a",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:05.920Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:37:05.920Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
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

### De verwante extensie voor een gegevenselement opzoeken {#extension}

U kunt de uitbreiding opzoeken die een gegevenselement door `/extension` aan de weg van een verzoek van de GET gebruikt toe te voegen.

**API-indeling**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/extension
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_ELEMENT_ID}` | De `id` van het gegevenselement waarvan uitbreiding u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de extensie die het opgegeven gegevenselement gebruikt.

```json
{
  "data": {
    "id": "EX9c7f9f1e826149978f2dadaf4c639679",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:37:31.952Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:31.952Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/property"
        },
        "data": {
          "id": "PR5c15543ef7bb403abc79d65fee0bf1f9",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/origin"
        },
        "data": {
          "id": "EX9c7f9f1e826149978f2dadaf4c639679",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5c15543ef7bb403abc79d65fee0bf1f9",
      "origin": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "self": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### De gerelateerde oorsprong van een gegevenselement opzoeken {#origin}

U kunt de oorsprong van een gegevenselement opzoeken door `/origin` aan de weg van een verzoek van de GET toe te voegen. De oorsprong van een gegevenselement is de vorige revisie die is bijgewerkt om de huidige revisie te maken.

**API-indeling**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/origin
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_ELEMENT_ID}` | De `id` van het gegevenselement waarvan oorsprong u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de oorsprong van het opgegeven gegevenselement.

```json
{
  "data": {
    "id": "DE790cb76f91594c2082a727b9f97024f6",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:37:19.891Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:37:19 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:19.891Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/property"
        },
        "data": {
          "id": "PRf1ac400fb1e04c689e28d5efcd675c94",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/origin"
        },
        "data": {
          "id": "DE790cb76f91594c2082a727b9f97024f6",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/extension"
        },
        "data": {
          "id": "EX2345dba2c8b34d1cbe2795e29c62bf27",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension"
        },
        "data": {
          "id": "EXad7ebb72d721478483b741eebfffda6a",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRf1ac400fb1e04c689e28d5efcd675c94",
      "origin": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "self": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "extension": "https://reactor.adobe.io/extensions/EX2345dba2c8b34d1cbe2795e29c62bf27"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### De verwante eigenschap voor een gegevenselement opzoeken {#property}

U kunt het bezit opzoeken dat een gegevenselement bezit door `/property` aan de weg van een verzoek van de GET toe te voegen.

**API-indeling**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/property
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATA_ELEMENT_ID}` | De `id` van het gegevenselement waarvan bezit u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de eigenschap die eigenaar is van het opgegeven gegevenselement.

```json
{
  "data": {
    "id": "PRae9440b0f3234c4286569485f2b7a6a2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:40.829Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:40.829Z",
      "platform": "web",
      "development": false,
      "token": "42daac072e1e",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments",
      "extensions": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions",
      "rules": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules",
      "self": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2"
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
