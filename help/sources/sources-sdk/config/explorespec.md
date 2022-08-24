---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Configureren van de specificaties voor Self-Serve Sources (Batch SDK)
topic-legacy: overview
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden om Self-Serve Sources (Batch SDK) te kunnen gebruiken.
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Configureren van de specificaties voor Self-Serve Sources (Batch SDK)

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

Als uw verkenningsspecificaties zijn gevuld, kunt u doorgaan en een volledige verbindingsspecificatie maken met de opdracht [!DNL Flow Service] API. Zie de [Zelfbedieningsbronnen (Batch SDK) API-handleiding](../api/api-overview.md) voor meer informatie .
