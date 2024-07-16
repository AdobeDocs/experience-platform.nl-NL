---
title: Personalization via Adobe Target
description: Leer hoe u de server-API gebruikt om persoonlijke ervaringen die in Adobe Target zijn gemaakt, te leveren en te renderen.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Personalization via Adobe Target

## Overzicht {#overview}

De server API van de Edge Network kan gepersonaliseerde ervaringen leveren en teruggeven die in Adobe Target, met de hulp van [ worden gecreeerd vorm-Gebaseerde Composer van de Ervaring ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

>[!IMPORTANT]
>
>De ervaringen van Personalization die door [ worden gecreeerd Visual Experience Composer (VEC) ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) worden niet volledig gesteund door de Server API. De server API kan **** activiteiten terugwinnen die door VEC worden gecreeerd, maar de Server API kan **** activiteiten niet teruggeven die door VEC worden gecreeerd. Als u activiteiten wilt teruggeven die door VEC worden gecreeerd, gelieve [ hybride verpersoonlijking ](../web-sdk/personalization/hybrid-personalization.md) uit te voeren gebruikend het Web SDK en de Server API van de Edge Network.

## Uw gegevensstroom configureren {#configure-your-datastream}

Voordat u de server-API in combinatie met Adobe Target kunt gebruiken, moet u Adobe Target-personalisatie in uw configuratie van de gegevensstroom inschakelen.

Zie de [ gids bij het toevoegen van de diensten aan een datastream ](../datastreams/overview.md#adobe-target-settings), voor gedetailleerde informatie over hoe te om Adobe Target toe te laten.

Wanneer u de gegevensstroom configureert, kunt u (optioneel) waarden opgeven voor [!DNL Property Token] , [!DNL Target Environment ID] en [!DNL Target Third Party ID Namespace] .

![ beeld UI die het scherm van de de dienstconfiguratie van de gegevensstroom toont, met Adobe Target selecteerde ](assets/target-datastream.png)

## Aangepaste parameters {#custom-parameters}

De meeste velden in het [!DNL XDM] -gedeelte van elke aanvraag worden geserialiseerd in puntnotatie en vervolgens verzonden naar Target als aangepaste of [!DNL mbox] -parameters.


### Voorbeeld {#custom-parameters-example}

Op basis van het volgende XDM-voorbeeld:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Bij het maken van doelgroepen zijn de volgende waarden beschikbaar als aangepaste parameters:

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Updates van doelprofiel {#profile-update}

Met [!DNL Server API] kunt u updates uitvoeren naar het doelprofiel. Als u een doelprofiel wilt bijwerken, moet u ervoor zorgen dat de profielgegevens worden doorgegeven in het `data` -gedeelte van de aanvraag in de volgende indeling:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Beoogde activiteiten opvragen {#querying-target-activities}

### Schema&#39;s {#schemas}

Het vraaggedeelte van het verzoek bepaalt welke inhoud door Doel is teruggekeerd. Onder het `personalization` -object bepaalt `schemas` het type inhoud dat door Target moet worden geretourneerd.

In situaties waar u van welke soort aanbiedingen onzeker bent u zult terugwinnen, zou u alle vier schema&#39;s in uw verpersoonlijkingsvraag aan de Edge Network moeten omvatten:

* **op HTML-Gebaseerde aanbiedingen:**
https://ns.adobe.com/personalization/html-content-item
* **op JSON-Gebaseerde aanbiedingen:**
https://ns.adobe.com/personalization/json-content-item
* **Redirect aanbiedingen van het Doel**
https://ns.adobe.com/personalization/redirect-item
* **DOM van het Doel Manipulation aanbiedingen**
https://ns.adobe.com/personalization/dom-action

### Beslissingsbereik {#decision-scopes}

Adobe Target [!DNL mbox] -namen moeten in de `decisionScopes` -array worden opgenomen om de juiste inhoud te retourneren.

#### Voorbeeld {#decision-scopes-example}

In het onderstaande voorbeeld worden alle vier de aanbiedingstypen opgevraagd, samen met een doelactiviteit met de naam `serverapimbox` .

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
      ]
   }
}
```

## API-aanroepvoorbeeld {#api-example}

**API formaat**

```http
POST /ee/v2/interact
```

### Verzoek {#request}

Een volledig verzoek dat een volledig voorwerp XDM, profielparameters, samen met de aangewezen vraag van het Doel omvat wordt hieronder geschetst.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
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
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Antwoord {#response}

De Edge Network zal een reactie teruggeven gelijkend op hieronder.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Als de bezoeker in aanmerking komt voor een verpersoonlijkingsactiviteit op basis van de gegevens die naar Adobe Target zijn verzonden, wordt de relevante activiteitsinhoud gevonden onder het `handle` -object, waarbij het type `personalization:decisions` is.

Andere inhoud wordt soms ook onder `handle` geretourneerd. Andere inhoudstypen zijn niet relevant voor de doelpersonalisatie. Als de bezoeker voor meerdere activiteiten in aanmerking komt, wordt elke activiteit een afzonderlijk `personalization` -object in de array.

In de onderstaande tabel worden de belangrijkste elementen van dat gedeelte van het antwoord uitgelegd.

| Eigenschap | Beschrijving | Voorbeeld |
|---|---|---|
| `scope` | De naam van de doelbox die tot de voorgestelde aanbiedingen heeft geleid. | `"scope": "serverapimbox"` |
| `items[].schema` | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. Dit is gerelateerd aan het type activiteit dat u hebt geselecteerd bij het maken van de verpersoonlijkingsactiviteit. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | De unieke id van de aanbiedingsactiviteit. Gewoonlijk een getal van 6 cijfers. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | De naam van de door de gebruiker opgegeven aanbiedingsactiviteit. Dit wordt verstrekt tijdens de stap van de activiteitenverwezenlijking. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | De unieke id van de personalisatie-ervaring. | `"experience.id": "0"` |
| `items[].meta.experience.name` | De unieke naam van de verpersoonlijkingservaring. | `"experience.name": "Experience A"` |
| `items[].data.id` | De id van de voorgestelde aanbieding. | `"id": "282484"` |
| `items[].data.format` | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. | `"format: "application/json` |
| `items[].data.content` | Inhoud van het voorgestelde aanbod. Dit zal voor verpersoonlijking van inhoud van de roepende toepassing worden gebruikt. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Voorbeeld van personalisatie aan de serverzijde {#sample}

De steekproeftoepassing die bij [ wordt gevonden dit URL ](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) toont het gebruiken van Adobe Experience Platform aan om verpersoonlijkingsinhoud van Adobe Target te krijgen. De webpagina verandert op basis van de geretourneerde personalisatie-inhoud.

Deze steekproef baseert zich _niet_ op cliënt-zijbibliotheken zoals [!DNL Web SDK] om verpersoonlijkingsinhoud te krijgen. In plaats daarvan worden de Adobe Experience Platform API&#39;s gebruikt om personalisatie-inhoud op te halen. Dan produceert de implementatie de HTML server-kant die op de teruggekeerde verpersoonlijkingsinhoud wordt gebaseerd.
