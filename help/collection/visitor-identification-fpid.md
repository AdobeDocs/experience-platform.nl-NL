---
title: Visitor-identificatie via FPID
description: Leer hoe u bezoekers consistent kunt identificeren via de server-API, met behulp van de FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: edge network;gateway;api;bezoeker;identificatie;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Visitor-identificatie via FPID

## Overzicht

[!DNL First-party IDs] (`FPIDs`) zijn apparaat-id&#39;s die door klanten worden gegenereerd, beheerd en opgeslagen. Dit geeft klanten controle over het identificeren van gebruikersapparaten. Door verzenden `FPIDs`, genereert het Edge-netwerk geen gloednieuwe `ECID` voor een aanvraag die er geen bevat.

De `FPID` kan als onderdeel van de `identityMap` of kan worden verzonden als een cookie.

An `FPID` kan definitief worden omgezet in een `ECID` door Edge Network, dus `FPID` identiteiten zijn volledig compatibel met Experience Cloud oplossingen. Een `ECID` van een specifieke `FPID` geeft altijd hetzelfde resultaat, zodat gebruikers een consistente ervaring hebben.

De `ECID` op deze manier verkregen `identity.fetch` query:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Voor aanvragen die zowel een `FPID` en `ECID`de `ECID` reeds in het verzoek aanwezig is, heeft voorrang op het verzoek dat uit het `FPID`. Daarom zal het Netwerk van de Rand gebruiken `ECID` reeds verstrekt en zal niet één van gegeven berekenen `FPID`.

In termen van apparaat-id&#39;s worden de `server` gegevensstromen moeten `FPID` als apparaat-id. Andere identiteiten (d.w.z. `EMAIL`) kan ook worden verstrekt binnen het verzoeklichaam, maar het Netwerk van de Rand vereist dat een primaire identiteit uitdrukkelijk wordt verstrekt. Primaire identiteit is de basisidentiteit waarin de profielgegevens worden opgeslagen.

>[!NOTE]
>
>Verzoeken die geen identiteit hebben, respectievelijk geen primaire identiteit die uitdrukkelijk binnen de aanvraaginstantie wordt geplaatst, zullen ontbreken.

Het volgende `identityMap` veldgroep is correct ingesteld voor een `server` gegevensstroomverzoek:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Het volgende `identityMap` veldgroep resulteert in een foutreactie als deze wordt ingesteld op een `server` gegevensstroomverzoek:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

De foutenreactie die door het Netwerk van Edge in dit geval wordt teruggekeerd is gelijkaardig aan het volgende:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Visitor-identificatie met `FPID`

Gebruikers identificeren via `FPID`ervoor te zorgen dat de `FPID` cookie is verzonden voordat aanvragen zijn ingediend bij het Edge-netwerk. De `FPID` kan worden doorgegeven in een cookie of als onderdeel van de `identityMap` in de inhoud van het verzoek.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
                    },
                    "webReferrer": {
                        "URL": ""
                    }
                },
                "device": {
                    "screenHeight": 1440,
                    "screenWidth": 3440,
                    "screenOrientation": "landscape"
                },
                "environment": {
                    "type": "browser",
                    "browserDetails": {
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Aanvragen met `FPID` doorgegeven als `identityMap` field

In het onderstaande voorbeeld wordt het [!DNL FPID] als `identityMap` parameter.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
