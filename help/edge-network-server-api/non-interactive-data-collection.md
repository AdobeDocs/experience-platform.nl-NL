---
title: Niet-interactieve gegevensverzameling
description: Leer hoe de Adobe Experience Platform Edge Network Server-API niet-interactieve gegevensverzamelingen uitvoert
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: gegevensverzameling;verzameling;adobe experience platform edge network;api;niet-interactieve gegevensverzameling
source-git-commit: 3bb73e5798d8fcdb6bb8bdcb796e8df6a1bd8805
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# Niet-interactieve gegevensverzameling

## Overzicht {#overview}

De niet-interactieve eindpunten van de gebeurtenisgegevensinzameling worden gebruikt om veelvoudige gebeurtenissen naar Experience Platform datasets of andere afzet te verzenden.

Het verzenden van gebeurtenissen in batch wordt aanbevolen wanneer gebeurtenissen voor eindgebruikers gedurende een korte periode lokaal in de wachtrij worden geplaatst (bijvoorbeeld wanneer er geen netwerkverbinding is).

Gebeurtenissen in batch moeten niet noodzakelijkerwijs tot dezelfde eindgebruiker behoren, wat betekent dat gebeurtenissen verschillende identiteiten binnen hun eigen identiteit kunnen bevatten `identityMap` object.


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## Niet-interactief voorbeeld van API-aanroep {#example}

### API-indeling {#api-format}

```http
POST /ee/v2/collect
```

### Verzoek {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
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
| `requestId` | `String` | Nee | Geef een externe id voor het overtrekken van aanvragen op. Als niets wordt verstrekt, zal het Netwerk van de Rand één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |
| `silent` | `Boolean` | Nee | Optionele booleaanse parameter die aangeeft of het Edge-netwerk een `204 No Content` reageren met een lege lading of niet. Kritieke fouten worden gerapporteerd met behulp van de corresponderende HTTP-statuscode en -lading. |


### Antwoord {#response}

Een geslaagde reactie retourneert een van de volgende statussen en een `requestID` indien in het verzoek geen informatie is verstrekt.

* `202 Accepted` wanneer het verzoek met succes is verwerkt;
* `204 No Content` wanneer de aanvraag met succes is verwerkt en de `silent` parameter is ingesteld op `true`;
* `400 Bad Request` wanneer het verzoek niet correct is geformuleerd (bv. de verplichte primaire identiteit is niet gevonden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
