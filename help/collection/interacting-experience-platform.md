---
title: Interactie met Adobe Experience Platform
description: Leer hoe u de Edge Network Server-API gebruikt om te communiceren met Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: gegevensverzameling; uitlaat; analytische gegevens; Adobe Experience Platform Edge Network api;aep
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interactie met Adobe Experience Platform

## Overzicht {#overview}

Om de gegevensinzameling van het Experience Platform toe te laten, moet u eerst [configureren, gegevensstroom](../edge/fundamentals/datastreams.md) gebeurtenissen door:sturen in Experience Platform datasets.

Zodra gevormd, zou de gegevensstroomconfiguratie montages voor moeten omvatten `com_adobe_experience_platform`, zoals in het onderstaande voorbeeld wordt getoond:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
