---
title: Niet-interactieve gegevensverzameling
description: Leer hoe de Adobe Experience Platform Edge Network Server API niet-interactieve gegevensverzameling uitvoert.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---


# Niet-interactieve gegevensverzameling

## Overzicht {#overview}

De niet-interactieve eindpunten van de gebeurtenisgegevensinzameling worden gebruikt om veelvoudige gebeurtenissen naar Experience Platform datasets of andere afzet te verzenden.

Het verzenden van gebeurtenissen in batch wordt aanbevolen wanneer gebeurtenissen voor eindgebruikers gedurende een korte periode lokaal in de wachtrij worden geplaatst (bijvoorbeeld wanneer er geen netwerkverbinding is).

Batch-gebeurtenissen hoeven niet noodzakelijkerwijs tot dezelfde eindgebruiker te behoren, wat betekent dat gebeurtenissen verschillende identiteiten kunnen bevatten binnen hun `identityMap` -object.

## Niet-interactief voorbeeld van API-aanroep {#example}

### API-indeling {#api-format}

```http
POST /ee/v2/collect
```

### Verzoek {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | ID van de gegevensstroom die door het eindpunt van de gegevensinzameling wordt gebruikt. |
| `requestId` | `String` | Nee | Geef een externe overtrekID voor aanvragen op. Als niets wordt verstrekt, zal de Edge Network één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |
| `silent` | `Boolean` | Nee | Optionele booleaanse parameter die aangeeft of de Edge Network een `204 No Content` -reactie moet retourneren met een lege lading. Kritieke fouten worden gerapporteerd met behulp van de corresponderende HTTP-statuscode en -lading. |

### Antwoord {#response}

Een geslaagde reactie retourneert een van de volgende statussen en een `requestID` als er niets in de aanvraag is opgegeven.

* `202 Accepted` wanneer de aanvraag correct is verwerkt;
* `204 No Content` wanneer de aanvraag is verwerkt en de parameter `silent` is ingesteld op `true` ;
* `400 Bad Request` wanneer de aanvraag niet correct is samengesteld (de verplichte primaire identiteit is bijvoorbeeld niet gevonden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
