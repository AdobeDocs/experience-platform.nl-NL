---
title: Personalisatie via Adobe Target
description: Leer hoe u de server-API gebruikt om persoonlijke ervaringen die in Adobe Target zijn gemaakt, te leveren en te renderen.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: d6573f8f4d779fb7ed11b44561a0ad9667748b27
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# Personalisatie via Adobe Target

## Overzicht {#overview}

De Edge Network Server-API kan gepersonaliseerde ervaringen die in Adobe Target zijn gemaakt, met behulp van de [Formuliergebaseerde Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>Persoonlijke ervaringen die zijn gemaakt via de [Target Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) niet volledig worden ondersteund door de server-API. De server-API kan **ophalen** activiteiten gemaakt door VEC, maar server API kan niet **renderen** door VEC gecreëerde activiteiten. Als u activiteiten wilt renderen die door VEC zijn gemaakt, moet u de opdracht [Web SDK](../edge/home.md).

## Uw gegevensstroom configureren {#configure-your-datastream}

Voordat u de server-API in combinatie met Adobe Target kunt gebruiken, moet u Adobe Target-personalisatie in uw configuratie van de gegevensstroom inschakelen.

Zie de [gids over het toevoegen van de diensten aan een gegevensstroom](../edge/datastreams/overview.md#adobe-target-settings), voor gedetailleerde informatie over hoe Adobe Target kan worden ingeschakeld.

Bij het configureren van de gegevensstroom kunt u (optioneel) waarden opgeven voor [!DNL Property Token], [!DNL Target Environment ID], en [!DNL Target Third Party ID Namespace].

![UI-afbeelding die het configuratiescherm van de datastream-service weergeeft, met Adobe Target geselecteerd](assets/target-datastream.png)

U kunt kiezen uit de volgende opties: [!DNL Analytics Logging] opties:

* **[!DNL Server Side]**: Dit is de standaardoptie voor [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). Als deze optie is geselecteerd, wordt telkens wanneer de personalisatie-inhoud door Target wordt geretourneerd, de relevante [!DNL A4T] gegevens worden automatisch naar Analytics verzonden, op basis van de reactie van de Target personalization engine.
* **[!DNL Client Side]**: Als deze optie is geselecteerd, wordt telkens wanneer de personalisatie-inhoud door Target wordt geretourneerd, de relevante [!DNL A4T] gegevens worden geretourneerd aan de aanroepende toepassing. Als u deze gegevens wilt opnemen in Analytics, moet u ervoor zorgen dat deze worden gerapporteerd bij een volgende oproep tot [!DNL Analytics].

   >[!IMPORTANT]
   >
   >Naast het selecteren **[!UICONTROL Client Side]** in de Configuratie van het Doel, moet u Analytics ook onbruikbaar maken, voor het Netwerk van de Rand om terug te keren [!DNL A4T] informatie terug naar het antwoord.


## Aangepaste parameters {#custom-parameters}

De meeste velden in de [!DNL XDM] deel van elk verzoek wordt geserialiseerd in puntnotatie en dan verzonden naar Doel als douane of [!DNL mbox] parameters.


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

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Updates van doelprofiel {#profile-update}

De [!DNL Server API] Hiermee kunt u updates uitvoeren naar het doelprofiel. Als u een doelprofiel wilt bijwerken, moet u ervoor zorgen dat de profielgegevens worden doorgegeven in het dialoogvenster `data` deel van het verzoek in het volgende formaat:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Quarting Target activities {#querying-target-activities}

### Schema&#39;s {#schemas}

Het vraaggedeelte van het verzoek bepaalt welke inhoud door Doel is teruggekeerd. Onder de `personalization` object, `schemas` bepaalt het type inhoud dat door Doel moet worden geretourneerd.

In situaties waar u van welke soort aanbiedingen onzeker bent u zult terugwinnen, zou u alle vier schema&#39;s in uw verpersoonlijkingsvraag aan het Netwerk van de Rand moeten omvatten:

* **Op HTML gebaseerde aanbiedingen:**
https://ns.adobe.com/personalization/html-content-item
* **Op JSON gebaseerde aanbiedingen:**
https://ns.adobe.com/personalization/json-content-item
* **Doelgerichte omleiding**
https://ns.adobe.com/personalization/redirect-item
* **Aanbiedingen voor DOM-manipulatie**
https://ns.adobe.com/personalization/dom-action

### Beslissingsbereik {#decision-scopes}

Adobe Target [!DNL mbox] de namen moeten in de `decisionScopes` -array om de juiste inhoud te retourneren.

#### Voorbeeld {#decision-scopes-example}

In het onderstaande voorbeeld worden alle vier de aanbiedingstypen opgevraagd samen met een doelactiviteit die wordt aangeroepen `serverapimbox`.

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

## Voorbeeld van API-aanroep {#api-example}

**API-indeling**

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

Het Edge-netwerk retourneert een vergelijkbare reactie als hieronder.

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

Als de bezoeker in aanmerking komt voor een verpersoonlijkingsactiviteit op basis van de gegevens die naar Adobe Target zijn verzonden, wordt de relevante activiteiteninhoud gevonden onder de `handle` object, waarbij het type `personalization:decisions`.

Andere inhoud wordt soms geretourneerd onder `handle` ook. Andere inhoudstypen zijn niet relevant voor de doelpersonalisatie. Als de bezoeker in aanmerking komt voor meerdere activiteiten, wordt elke activiteit afzonderlijk uitgevoerd `personalization` -object in de array.

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
