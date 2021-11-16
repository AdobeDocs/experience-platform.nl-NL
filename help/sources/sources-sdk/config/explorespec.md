---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Vorm onderzoek specificaties voor Bronnen SDK
topic-legacy: overview
description: Dit document verstrekt een overzicht van de configuraties u moet voorbereiden om Bronnen SDK te gebruiken.
hide: true
hidefromtoc: true
source-git-commit: 4ce9eac605fb7c801852cd0e109448d314092603
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Vorm onderzoek specificaties voor Bronnen SDK

De specificaties van het onderzoek bepalen de parameters die voor het onderzoeken van en het inspecteren van voorwerpen in uw bron worden vereist. Met de specificaties verkennen definieert u ook de indeling voor reacties die wordt geretourneerd wanneer objecten worden doorzocht en geïnspecteerd.

>[!TIP]
>
>Verken de specificaties zijn hard-gecodeerd en u kunt eenvoudig de lading kopiëren en kleven hieronder aan uw verbindingsspecificatie.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Specificaties verkennen | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `name` | Definieert de naam of id van de exploratiespecificatie. | `Resource` |
| `type` | Definieert het type van de verkenningsspecificatie. | `Resource` |
| `requestSpec` | Bevat de parameters die vereist zijn om objecten in de verbinding te verkennen. |
| `requestSpec.type` | Definieert het gegevenstype van de aanvraagspecificatie. | `object` |
| `responseSpec` | Bevat de parameters die het formaat van het antwoordbericht bepalen tegen een verkennen vraag is teruggekeerd. |
| `responseSpec.type` | Definieert het gegevenstype van de reactiespecificatie. | `object` |
| `responseSpec.properties` | Bevat informatie met betrekking tot hoe het reactiebericht wordt geformatteerd. |
| `responseSpec.properties.format` | Bepaalt het formatteren van het reactieschema. | `object` |
| `responseSpec.properties.format.type` | Definieert het gegevenstype van eigenschappen. | `string` |
| `responseSpec.schema` | Bevat informatie met betrekking tot hoe het reactieschema geformatteerd is. |
| `responseSpec.schema.type` | Definieert het gegevenstype van het schema. | `object` |
| `responseSpec.schema.properties` | Bevat informatie over de kolommen, het type, en de punten die binnen een schema worden gehouden. |
| `responseSpec.schema.properties.columns.items.properties.name` | Hiermee geeft u de naam van het bestand weer. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Hiermee definieert u het gegevenstype van de bestandsnaam. | `string` |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Als uw verkenningsspecificaties zijn gevuld, kunt u doorgaan en een volledige verbindingsspecificatie maken met de opdracht [!DNL Flow Service] API. Zie de [[!DNL Sources SDK] API-handleiding](../api/overview.md) voor meer informatie .