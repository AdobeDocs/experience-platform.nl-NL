---
title: Callbacks eindpunt
description: Leer hoe te om vraag aan het /callbacks eindpunt in Reactor API te maken.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 3%

---

# Callbacks eindpunt

Een callback is een bericht dat de Reactor API naar een specifieke URL verzendt (gewoonlijk één die door uw organisatie wordt ontvangen).

Callbacks zijn bedoeld om samen met [&#x200B; controlegebeurtenissen &#x200B;](./audit-events.md) aan spooractiviteiten in Reactor API worden gebruikt. Telkens wanneer een controlegebeurtenis van een bepaald type wordt geproduceerd, kan een callback een passend bericht naar gespecificeerde URL verzenden.

De service achter de URL die in de callback is opgegeven, moet reageren met HTTP-statuscode 200 (OK) of 201 (Gemaakt). Als de dienst niet met één van beiden van deze statuscodes antwoordt, wordt de berichtlevering opnieuw geprobeerd met de volgende intervallen:

* 1 minuut
* 5 minuten
* 30 minuten
* 1 uur
* 12 uur
* 1 dag
* 3 dagen

>[!NOTE]
>
>Intervallen voor opnieuw proberen zijn relatief ten opzichte van het vorige interval. Als het opnieuw proberen op één minuut bijvoorbeeld mislukt, wordt de volgende poging vijf minuten gepland nadat de poging van één minuut is mislukt (zes minuten nadat het bericht is gegenereerd).

Als alle leveringspogingen zijn mislukt, wordt het bericht genegeerd.

Een callback behoort tot precies één [&#x200B; bezit &#x200B;](./properties.md). Een eigenschap kan vele callbacks hebben.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [&#x200B; Reactor API &#x200B;](https://www.adobe.io/experience-platform-apis/references/reactor/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../getting-started.md) voor belangrijke informatie betreffende hoe te voor authentiek te verklaren aan API.

## Callbacks weergeven {#list}

U kunt van alle callbacks onder een bezit een lijst maken door een verzoek van de GET te doen.

**API formaat**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van de eigenschap waarvan u de callbacks wilt weergeven. |

{style="table-layout:auto"}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde callbacks op de volgende attributen worden gefiltreerd:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Zie de gids bij [&#x200B; het filtreren reacties &#x200B;](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een succesvolle reactie keert een lijst van callbacks voor het gespecificeerde bezit terug.

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

## Een callback opzoeken {#lookup}

U kunt omhoog callback kijken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

**API formaat**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een succesvolle reactie keert de details van callback terug.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Een callback maken {#create}

U kunt een nieuwe callback tot stand brengen door een verzoek van de POST te doen.

**API formaat**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | `id` van het [&#x200B; bezit &#x200B;](./properties.md) dat u callback bepaalt onder. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `url` | De bestemming URL voor het callback bericht. De URL moet de HTTPS-protocolextensie gebruiken. |
| `subscriptions` | Een array van tekenreeksen die de gebeurtenistypen van de audit aangeven die de callback activeren. Zie de [&#x200B; gids van het de controlegebeurtenissen eindpunt &#x200B;](./audit-events.md) voor een lijst van mogelijke gebeurtenistypen. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert de details van pas gecreëerde callback terug.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Een callback bijwerken

U kunt een callback bijwerken door zijn identiteitskaart in de weg van een verzoek van de PATCH te omvatten.

**API formaat**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt de array `subscriptions` voor een bestaande callback bijgewerkt.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de callback moeten worden bijgewerkt. Elke sleutel vertegenwoordigt het bepaalde callback attribuut dat moet worden bijgewerkt, samen met de overeenkomstige waarde het zou moeten worden bijgewerkt aan.<br><br> de volgende attributen kunnen voor callbacks worden bijgewerkt:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | De `id` van de callback die u wilt bijwerken. Dit moet overeenkomen met de `{CALLBACK_ID}` -waarde in het aanvraagpad. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt moet de waarde `callbacks` zijn. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert de details van bijgewerkte callback terug.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Een callback verwijderen

U kunt een callback schrappen door zijn identiteitskaart in de weg van een verzoek van de DELETE te omvatten.

**API formaat**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder antwoord, wat aangeeft dat de callback is verwijderd.
