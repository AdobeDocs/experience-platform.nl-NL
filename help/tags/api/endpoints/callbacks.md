---
title: Callbacks eindpunt
description: Leer hoe te om vraag aan het /callbacks eindpunt in Reactor API te maken.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# Callbacks eindpunt

Een callback is een bericht dat de Reactor API naar een specifieke URL verzendt (gewoonlijk één die door uw organisatie wordt ontvangen).

Callbacks zijn bedoeld om samen met [auditgebeurtenissen](./audit-events.md) de activiteiten in de Reactor-API volgen. Telkens wanneer een controlegebeurtenis van een bepaald type wordt geproduceerd, kan een callback een passend bericht naar gespecificeerde URL verzenden.

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

Een callback behoort tot precies één [eigenschap](./properties.md). Een eigenschap kan vele callbacks hebben.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Callbacks weergeven {#list}

U kunt van alle callbacks onder een bezit een lijst maken door een verzoek van de GET te doen.

**API-indeling**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `id` van het bezit waarvan callbacks u wilt een lijst maken. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde callbacks op de volgende attributen worden gefiltreerd:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Zie de handleiding op [filterreacties](../guides/filtering.md) voor meer informatie .

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

**Antwoord**

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

**API-indeling**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

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

**Antwoord**

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

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de [eigenschap](./properties.md) dat u de callback onder bepaalt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
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
| `subscriptions` | Een array van tekenreeksen die de gebeurtenistypen van de audit aangeven die de callback zullen activeren. Zie de [eindhandleiding voor auditgebeurtenissen](./audit-events.md) voor een lijst met mogelijke gebeurtenistypen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

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

U kunt een callback bijwerken door zijn identiteitskaart in de weg van een verzoek van de PUT te omvatten.

**API-indeling**

```http
PUT /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

De volgende aanvraag werkt de `subscriptions` array voor een bestaande callback.

```shell
curl -X PUT \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
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
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de callback moeten worden bijgewerkt. Elke sleutel vertegenwoordigt het bepaalde callback attribuut dat moet worden bijgewerkt, samen met de overeenkomstige waarde het zou moeten worden bijgewerkt aan.<br><br>De volgende attributen kunnen voor callbacks worden bijgewerkt:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | De `id` van de callback die u wilt bijwerken. Dit moet overeenkomen met de `{CALLBACK_ID}` waarde opgegeven in het aanvraagpad. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde zijn `callbacks`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

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

**API-indeling**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `CALLBACK_ID` | De `id` van de callback die u wilt schrappen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder antwoord, wat aangeeft dat de callback is verwijderd.
