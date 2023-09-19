---
title: Interactieve gegevensverzameling
description: Leer hoe de Adobe Experience Platform Edge Network Server API interactieve gegevensverzameling uitvoert.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 3%

---

# Interactieve gegevensverzameling

## Overzicht {#overview}

De interactieve eindpunten van de gegevensinzameling ontvangen één enkele gebeurtenis en worden gebruikt wanneer de cliënt een antwoord verwacht dat door de server van het Netwerk van de Rand van Adobe Experience Platform zal zijn teruggekeerd. Deze eindpunten kunnen inhoud van andere diensten van het Netwerk van de Rand ook terugkeren, terwijl het uitvoeren van gegevensinzameling.

De serverreactie omvat een of meer `Handle` objecten, zoals hieronder weergegeven.

## API-aanroepvoorbeeld

### API-indeling {#format}

```http
POST /ee/v2/interact
```

### Verzoek {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | DataStream-id. |
| `requestId` | `String` | Nee | Geef een willekeurige client-id op voor correlerende interne serveraanvragen. Als niets wordt verstrekt, zal het Netwerk van de Rand één produceren en zal het in de reactie terugkeren. |

### Antwoord {#response}

Een geslaagde reactie retourneert de HTTP-status `200 OK`, met een of meer `Handle` objecten, afhankelijk van de Edge-services in real time die in de configuratie van de gegevensstroom zijn ingeschakeld.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
