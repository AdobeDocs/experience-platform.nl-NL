---
title: Het eindpunt van gebeurtenissen controleren
description: Leer hoe te om vraag aan het /audit_events eindpunt in Reactor API te maken.
exl-id: 59cd58dc-4085-47b7-846f-d3937740dd9b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Het eindpunt van gebeurtenissen controleren

>[!WARNING]
>
>De implementatie van het `/audit_events` eindpunt is in flits aangezien de eigenschappen worden toegevoegd, verwijderd, en herwerkt.

Een auditgebeurtenis is een record van een specifieke wijziging van een andere bron in de Reactor-API, die wordt gegenereerd op het moment dat de wijziging wordt aangebracht. Dit zijn systeemgebeurtenissen die aan door het gebruik van a [ callback ](./callbacks.md) kunnen worden ingetekend. Met het `/audit_events` -eindpunt in de Reactor-API kunt u auditgebeurtenissen programmatisch beheren binnen uw ervaringstoepassing.

Audit-gebeurtenissen hebben de notatie `{RESOURCE_TYPE}.{EVENT}`, zoals `build.created` of `rule.updated` .

Het middeltype kan om het even welke volgend zijn:

* `property`
* `extension`
* `data_element`
* `rule`
* `rule_component`
* `library`
* `build`
* `environment`
* `host`

De volgende gebeurtenissen worden ondersteund voor elk brontype:

* `created`
* `updated`
* `deleted`

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [ Reactor API ](https://www.adobe.io/experience-platform-apis/references/reactor/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie betreffende hoe te voor authentiek te verklaren aan API.

## Een lijst met auditgebeurtenissen ophalen {#list}

U kunt een lijst van controlegebeurtenissen voor alle eigenschappen terugwinnen die door uw organisatie worden bezeten door een verzoek van de GET tot het `/audit_events` eindpunt te richten.

**API formaat**

```http
GET /audit_events
```

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een geslaagde reactie retourneert een lijst met auditgebeurtenissen. De voorbeeldreactie hieronder is afgebroken voor de ruimte.

```json
{
  "data": [
    {
      "id": "AEa98742de8ef044d8b86767aa6a15a674",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:21.836Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.updated",
        "updated_at": "2020-12-14T17:31:21.836Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app_2\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:21.787Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674"
      }
    },
    {
      "id": "AE7320b6c1c3f84bb69405fcfe9cb58189",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:10.672Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.created",
        "updated_at": "2020-12-14T17:31:10.672Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:10.626Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AE7320b6c1c3f84bb69405fcfe9cb58189"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=129&page%5Bsize%5D=25"
  },
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

## Een auditgebeurtenis opzoeken {#lookup}

U kunt een controlegebeurtenis opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

**API formaat**

```http
GET /audit_events/{AUDIT_EVENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `AUDIT_EVENT_ID` | De `id` van de auditgebeurtenis die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een succesvolle reactie retourneert de details van de auditgebeurtenis.

```json
{
  "data": {
    "id": "AEd6a3b381fb8241818d7520001f8bd459",
    "type": "audit_events",
    "attributes": {
      "attributed_to_display_name": "John Smith",
      "attributed_to_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:31:46.956Z",
      "display_name": "Example Rule",
      "type_of": "rule.created",
      "updated_at": "2020-12-14T17:31:46.956Z",
      "entity": "{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"meta\":{\"latest_revision_number\":0},\"type\":\"rules\",\"links\":{\"self\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"origin\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"property\":\"https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"rule_components\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"},\"attributes\":{\"name\":\"Example Rule\",\"dirty\":true,\"enabled\":true,\"published\":false,\"created_at\":\"2020-12-14T17:31:46.883Z\",\"deleted_at\":null,\"updated_at\":\"2020-12-14T17:31:46.883Z\",\"published_at\":null,\"review_status\":\"unsubmitted\",\"revision_number\":0},\"relationships\":{\"notes\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes\"}},\"origin\":{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"type\":\"rules\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin\"}},\"property\":{\"data\":{\"id\":\"PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"type\":\"properties\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property\"}},\"libraries\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries\"}},\"revisions\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions\"}},\"rule_components\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"}}}}}"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "entity": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/rule"
        },
        "data": {
          "type": "rules",
          "id": "RL52d156a9074844b89ca20c987dbafd3b"
        }
      }
    },
    "links": {
      "entity": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "self": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459"
    },
    "meta": {
      "property_name": "Kessel Example Property"
    }
  }
}
```
