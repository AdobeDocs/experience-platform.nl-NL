---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL-conversies
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# PQL-conversies

intro

- Opmaak vanuit pql/tekst en pql/json omzetten

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de segmentatie-API. Lees de ontwikkelaarsgids voor [segmentatie voordat u verdergaat](./getting-started.md).

In het bijzonder, omvat de [begonnen sectie](./getting-started.md#getting-started) van de de ontwikkelaarsgids van de Segmentatie verbindingen aan verwante onderwerpen, een gids aan het lezen van de steekproefAPI vraag in het document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke API van het Platform van de Ervaring met succes te maken.

## Opmaak vanuit pql/tekst en pql/json omzetten

**API-indeling**

```http
POST /segment/conversion
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een unieke naam voor de segmentdefinitie. |
| `expression.type` | Het expressietype. Het kan zijn `PQL` of `ARL`. |
| `expression.format` | De expressie-indeling. Het kan zijn `pql/text` of `pql/json`. |
| `expression.value` | De queryreeks van de expressie die u wilt omzetten. |
| `schema.name` | De klasse-id van het schema waarnaar u verwijst. |
| `ttlInDays` | Een geheel getal dat de tijd vertegenwoordigt om te leven (TTL). |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw omgezette segment terug.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Volgende stappen
