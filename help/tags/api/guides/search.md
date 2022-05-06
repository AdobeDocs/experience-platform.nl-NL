---
title: Bronnen zoeken in de Reactor-API
description: Leer hoe u naar bronnen in de Reactor-API kunt zoeken.
exl-id: cb594e60-3e24-457e-bfb3-78ec84d3e39a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Bronnen zoeken in de Reactor-API

De `/search` eindpunt in Reactor API staat u toe om gestructureerde vragen over opgeslagen middelen te maken. Dit document bevat voorbeelden van verschillende zoekopdrachten voor verschillende veelvoorkomende gebruiksgevallen.

>[!NOTE]
>
>Voor het lezen van deze handleiding raadpleegt u de [zoekeindpuntgids](../endpoints/search.md) voor informatie over toegelaten vraagsyntaxis en andere gebruiksrichtlijnen.

## Basisquerystrategieën

In de volgende voorbeelden worden enkele basisbeginselen getoond voor het gebruik van de zoekfunctionaliteit van de API.

### Zoeken in meerdere velden

U kunt zoeken in meerdere velden door jokertekens in de veldnaam te gebruiken. Als u bijvoorbeeld wilt zoeken in meerdere kenmerkvelden, gebruikt u `attributes.*` als de veldnaam.

```json
{
  "data": {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>Doorgaans moeten de zoekwaarden overeenkomen met het type gegevens dat wordt doorzocht. Bijvoorbeeld, een vraagwaarde van `evar7` in een veld met gehele getallen mislukt. Wanneer het zoeken over veelvoudige gebieden, wordt het vraagtype vereist om fouten te vermijden, maar kan ongewenste resultaten veroorzaken.

### De vragen van het werkingsgebied aan specifieke middeltypes

U kunt een onderzoek tot een specifiek middeltype door te voorzien `resource_types` in het verzoek. Als u bijvoorbeeld wilt zoeken naar `data_elements`, en `rule_components`:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### Reacties sorteren

De `sort` kan worden gebruikt om reacties te sorteren. Als u bijvoorbeeld wilt sorteren op `created_at` met nieuwste eerst:

```json
{
  "data": {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## Algemene zoekvoorbeelden

In het volgende voorbeeld worden extra gebruikelijke zoekpatronen getoond.

### Elke bron met een specifieke naam

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### Elke bron die verwijst naar &quot;evar7&quot;

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### De elementen van gegevens van een &quot;douane-code&quot;afgevaardigde type

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### Regelcomponenten die verwijzen naar een specifiek gegevenselement

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### Regels in een specifieke eigenschap

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### Een bron zoeken op ID

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### Een zoekopdracht uitvoeren met de term &quot;OR&quot;-logica

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
