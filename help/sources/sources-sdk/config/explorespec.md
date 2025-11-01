---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Configureren van verkennende specificaties voor Self-Serve Bronnen (Batch SDK)
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden voor het gebruik van Self-Serve Sources (Batch SDK).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Configureren van verkennende specificaties voor Self-Serve Bronnen (Batch SDK)

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
| `requestSpec` | Bevat de parameters die vereist zijn om objecten in de verbinding te verkennen. |  |
| `requestSpec.type` | Definieert het gegevenstype van de aanvraagspecificatie. | `object` |
| `responseSpec` | Bevat de parameters die het formaat van het antwoordbericht bepalen tegen een verkennen vraag is teruggekeerd. |  |
| `responseSpec.type` | Definieert het gegevenstype van de reactiespecificatie. | `object` |
| `responseSpec.properties` | Bevat informatie met betrekking tot hoe het reactiebericht wordt geformatteerd. |  |
| `responseSpec.properties.format` | Bepaalt het formatteren van het reactieschema. | `object` |
| `responseSpec.properties.format.type` | Definieert het gegevenstype van eigenschappen. | `string` |
| `responseSpec.schema` | Bevat informatie met betrekking tot hoe het reactieschema geformatteerd is. |  |
| `responseSpec.schema.type` | Definieert het gegevenstype van het schema. | `object` |
| `responseSpec.schema.properties` | Bevat informatie over de kolommen, het type, en de punten die binnen een schema worden gehouden. |  |
| `responseSpec.schema.properties.columns.items.properties.name` | Hiermee geeft u de naam van het bestand weer. |  |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Hiermee definieert u het gegevenstype van de bestandsnaam. | `string` |

{style="table-layout:auto"}

## Volgende stappen

Als uw verkenningsspecificaties zijn gevuld, kunt u doorgaan met het maken van een volledige verbindingsspecificatie met de API [!DNL Flow Service] . Zie de [&#x200B; Zelfbediening Bron (Partij SDK) API gids &#x200B;](../api/api-overview.md) voor meer informatie.
