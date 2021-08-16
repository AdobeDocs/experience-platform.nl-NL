---
title: Punt voor App-configuraties
description: Leer hoe te om vraag aan het /app_configuration eindpunt in Reactor API te maken.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# Punt voor App-configuraties

>[!WARNING]
>
>De implementatie van het `/app_configurations` eindpunt is in flits aangezien de eigenschappen worden toegevoegd, verwijderd, en herwerkt.

Met toepassingsconfiguraties kunnen referenties worden opgeslagen en opgehaald voor later gebruik. Met het `/app_configurations`-eindpunt in de Reactor-API kunt u toepassingsconfiguraties programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Een lijst met toepassingsconfiguraties ophalen {#list}

**API-indeling**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschrijving |
| --- | --- |
| `COMPANY_ID` | De `id` van het [bedrijf](./companies.md) dat eigenaar is van de toepassingsconfiguraties. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Met behulp van queryparameters kunnen de weergegeven toepassingsconfiguraties worden gefilterd op basis van de volgende kenmerken:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Zie de gids op [het filtreren reacties](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met toepassingsconfiguraties.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
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

## Een toepassingsconfiguratie opzoeken {#lookup}

U kunt een toepassingsconfiguratie opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

**API-indeling**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `APP_CONFIGURATION_ID` | De `id` van de toepassingsconfiguratie die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord retourneert de details van de toepassingsconfiguratie.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Een toepassingsconfiguratie maken {#create}

U kunt een nieuwe toepassingsconfiguratie tot stand brengen door een verzoek van de POST te doen.

**API-indeling**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschrijving |
| --- | --- |
| `COMPANY_ID` | De `id` van het [bedrijf](./companies.md) dat u de toepassingsconfiguratie onder bepaalt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `platform` | Het platform waarop de toepassing wordt uitgevoerd (web of mobiel). Dit bepaalt welke overseinendiensten beschikbaar zijn. |
| `messaging_service` | De berichtenservice die aan de app is gekoppeld, zoals [Apple Push Notification service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) en [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Hiermee bepaalt u welke sleuteltypen kunnen worden gebruikt. |
| `key_type` | Vertegenwoordigt het protocol dat een leverancier van de dupservice steunt en bepaalt het formaat van het `push_credential` voorwerp. Aangezien de protocollen voor overseinendiensten evolueren, worden de nieuwe `key_type` waarden gecreeerd om de bijgewerkte protocollen te steunen. |
| `push_credential` | De eigenlijke credentiewaarde, die in rust wordt gecodeerd. Dit veld wordt gewoonlijk niet gedecodeerd of opgenomen in API-reacties. Alleen bepaalde Adobe-services kunnen een reactie krijgen die een ontsleutelde pushreferentie bevat. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de nieuwe toepassingsconfiguratie.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Toepassingsconfiguratie bijwerken

U kunt een toepassingsconfiguratie bijwerken door zijn identiteitskaart in de weg van een verzoek van de PUT op te nemen.

**API-indeling**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `APP_CONFIGURATION_ID` | De `id` van de toepassingsconfiguratie die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt `app_id` bijgewerkt voor een bestaande toepassingsconfiguratie.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de toepassingsconfiguratie moeten worden bijgewerkt. Elke sleutel vertegenwoordigt het specifieke attribuut van de toepassingsconfiguratie dat moet worden bijgewerkt, samen met de overeenkomstige waarde het zou moeten worden bijgewerkt aan.<br><br>De volgende kenmerken kunnen worden bijgewerkt voor toepassingsconfiguraties:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | De `id` van de toepassingsconfiguratie die u wilt bijwerken. Dit zou de `{APP_CONFIGURATION_ID}` waarde moeten aanpassen die in de verzoekweg wordt verstrekt. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `app_configurations` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord retourneert de details van de bijgewerkte toepassingsconfiguratie.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Een toepassingsconfiguratie verwijderen

U kunt een toepassingsconfiguratie schrappen door zijn identiteitskaart in de weg van een verzoek van de DELETE op te nemen.

**API-indeling**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `APP_CONFIGURATION_ID` | De `id` van de toepassingsconfiguratie die u wilt schrappen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responsiehoofdtekst om aan te geven dat de toepassingsconfiguratie is verwijderd.
