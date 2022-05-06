---
title: Punt voor App-configuraties
description: Leer hoe te om vraag aan het /app_configuration eindpunt in Reactor API te maken.
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---

# Punt voor App-configuraties

>[!WARNING]
>
>De uitvoering van de `/app_configurations` Het eindpunt is in flits aangezien de eigenschappen worden toegevoegd, verwijderd, en herwerkt.

Met toepassingsconfiguraties kunnen referenties worden opgeslagen en opgehaald voor later gebruik. De `/app_configurations` kunt u toepassingsconfiguraties programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Een lijst met toepassingsconfiguraties ophalen {#list}

**API-indeling**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beschrijving |
| --- | --- |
| `COMPANY_ID` | De `id` van de [bedrijf](./companies.md) die eigenaar is van de toepassingsconfiguraties. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Met behulp van queryparameters kunnen de weergegeven toepassingsconfiguraties worden gefilterd op basis van de volgende kenmerken:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Zie de handleiding op [filterreacties](../guides/filtering.md) voor meer informatie .

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `COMPANY_ID` | De `id` van de [bedrijf](./companies.md) dat u de toepassingsconfiguratie onder definieert. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `messaging_service` | De berichtenservice die aan de app is gekoppeld, zoals [APN&#39;s (Apple Push Notification service)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) en [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Hiermee bepaalt u welke sleuteltypen kunnen worden gebruikt. |
| `key_type` | Vertegenwoordigt het protocol dat een duw-dienst verkoper steunt en bepaalt het formaat van `push_credential` object. Aangezien de protocollen voor overseinendiensten evolueren, nieuw `key_type` waarden worden gecreeerd om de bijgewerkte protocollen te steunen. |
| `push_credential` | De eigenlijke credentiewaarde, die in rust wordt gecodeerd. Dit veld wordt gewoonlijk niet gedecodeerd of opgenomen in API-reacties. Alleen bepaalde Adobe-services kunnen een antwoord krijgen met een gedecodeerde pushreferentie. |

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

De volgende aanvraag werkt de `app_id` voor een bestaande toepassingsconfiguratie.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `id` | De `id` van de toepassingsconfiguratie die u wilt bijwerken. Dit moet overeenkomen met de `{APP_CONFIGURATION_ID}` waarde opgegeven in het aanvraagpad. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde zijn `app_configurations`. |

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
| `APP_CONFIGURATION_ID` | De `id` van de toepassingsconfiguratie die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder responsiehoofdtekst om aan te geven dat de toepassingsconfiguratie is verwijderd.
