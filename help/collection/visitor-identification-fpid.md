---
title: Visitor-identificatie via FPID
description: Leer hoe u bezoekers consistent kunt identificeren via de Edge Network API, met de FPID
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: edge network;gateway;api;bezoeker;identificatie;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Visitor-identificatie via FPID

[!DNL First-party IDs] (`FPIDs`) is apparaat IDs die door klanten wordt geproduceerd, wordt geleid en wordt opgeslagen. Dit geeft klanten controle over het identificeren van gebruikersapparaten. Door `FPIDs` te verzenden, genereert de Edge Network geen gloednieuw `ECID` voor een aanvraag die er geen bevat.

`FPID` kan als onderdeel van `identityMap` in de aanvraagtekst van de API worden opgenomen of als cookie worden verzonden.

Een `FPID` kan deterministisch worden omgezet in een `ECID` door de Edge Network, zodat `FPID` -identiteiten volledig compatibel zijn met Experience Cloud-oplossingen. Het verkrijgen van een `ECID` van een specifieke `FPID` geeft altijd hetzelfde resultaat, zodat gebruikers een consistente ervaring hebben.

De op deze manier verkregen `ECID` kan worden opgehaald via een `identity.fetch` -query:

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

Voor aanvragen die zowel een `FPID` als een `ECID` bevatten, heeft de eigenschap `ECID` die al in de aanvraag aanwezig is, voorrang op de aanvraag die kan worden gegenereerd vanuit de `FPID` . Met andere woorden, de Edge Network gebruikt de `ECID` die al is opgegeven en de `FPID` wordt genegeerd. Een nieuwe `ECID` wordt alleen gegenereerd wanneer een `FPID` op zichzelf wordt geleverd.

Wat apparaat-id&#39;s betreft, moeten de `server` gegevensstromen `FPID` gebruiken als apparaat-id. Andere identiteiten (d.w.z. `EMAIL`) kunnen ook binnen de aanvraaginstantie worden opgegeven, maar de Edge Network vereist dat expliciet een primaire identiteit wordt opgegeven. Primaire identiteit is de basisidentiteit waarin de profielgegevens worden opgeslagen.

>[!NOTE]
>
>Verzoeken die geen identiteit hebben, respectievelijk geen primaire identiteit die uitdrukkelijk binnen de aanvraaginstantie wordt geplaatst, zullen ontbreken.

De volgende `identityMap` -veldgroep wordt correct gevormd voor een `server` -gegevensstroomaanvraag:

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

De volgende `identityMap` -veldgroep resulteert in een foutreactie wanneer deze wordt ingesteld op een `server` -gegevensstroomaanvraag:

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

De door de Edge Network in dit geval geretourneerde foutreactie is vergelijkbaar met de volgende:

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

Als u gebruikers wilt identificeren via `FPID` , moet u ervoor zorgen dat het `FPID` -cookie is verzonden voordat u aanvragen bij de Edge Network indient. `FPID` kan in een koekje of als deel van `identityMap` in het lichaam van het verzoek worden overgegaan.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
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

## Verzoek met `FPID` doorgegeven als `identityMap` -veld

In het onderstaande voorbeeld wordt de parameter [!DNL FPID] als een parameter `identityMap` doorgegeven.

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
