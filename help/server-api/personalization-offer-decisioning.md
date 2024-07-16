---
title: Personalization via Offer decisioning
description: Leer hoe u de server-API gebruikt om persoonlijke ervaringen via Offer decisioning te leveren en weer te geven.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Personalization via Offer decisioning

## Overzicht {#overview}

De Server API van de Edge Network kan gepersonaliseerde ervaringen leveren die in [ Offer decisioning ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html) aan het Webkanaal worden beheerd.

[!DNL Offer Decisioning] ondersteunt een niet-visuele interface voor het maken, activeren en leveren van uw activiteiten en een persoonlijk tintje.

## Vereisten {#prerequisites}

Personalization via [!DNL Offer Decisioning] vereist dat u toegang tot [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) hebt alvorens u uw integratie vormt.

## Uw gegevensstroom configureren {#configure-your-datastream}

Voordat u de server-API in combinatie met Offer decisioning kunt gebruiken, moet u de personalisatie van Adobe Experience Platform in uw configuratie van de gegevensstroom inschakelen en de optie **[!UICONTROL Offer Decisioning]** inschakelen.

Zie de [ gids bij het toevoegen van de diensten aan een datastream ](../datastreams/overview.md#adobe-experience-platform-settings), voor gedetailleerde informatie over hoe te om Offer decisioning toe te laten.

![ beeld UI die het scherm van de de dienstconfiguratie van de gegevensstroom toont, met geselecteerde Offer decisioning ](assets/aep-od-datastream.png)

## Aanmaken van publiek {#audience-creation}

[!DNL Offer Decisioning] is voor het maken van publiek afhankelijk van de Adobe Experience Platform Segmentation Service. U kunt de documentatie voor [!DNL Segmentation Service] [ hier ](../segmentation/home.md) vinden.

## Bepaling van beslissingsbereik {#creating-decision-scopes}

[!DNL Offer Decision Engine] gebruikt de gegevens van Adobe Experience Platform en [ Real-Time de profielen van de Klant ](../profile/home.md), samen met [!DNL Offer Library], om aanbiedingen aan de juiste klanten en kanalen in de juiste tijd te leveren.

Meer over [!DNL Offer Decisioning Engine] leren, zie de specifieke [ documentatie ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html).

Na [ vormend uw datastream ](#configure-your-datastream), moet u het besluitvormingswerkingsgebied bepalen dat in uw verpersoonlijkingscampagne moet worden gebruikt.

[ het werkingsgebied van het Besluit ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes) is de Base64-Gecodeerde koorden JSON die de activiteit en plaatsing IDs bevatten die u [!DNL Offer Decisioning Service] wilt gebruiken wanneer het voorstellen van aanbiedingen.

**werkingsgebied JSON van het Besluit**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**gebied Base64-Gecodeerde koord van het Besluit**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Nadat u uw aanbiedingen en inzamelingen hebt gecreeerd, moet u a [ besluitvormingswerkingsgebied ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes) bepalen.

Kopieer het Base64-Gecodeerde besluitvormingswerkingsgebied. U gebruikt dit in het `query` -object van de API-aanvraag van de server.

![ beeld UI die de Offer decisioning UI toont, die het besluitvormingswerkingsgebied benadrukt.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
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

Een volledig verzoek dat een volledig voorwerp XDM, gegevensvoorwerp en een vraag van de Offer decisioning omvat wordt hieronder geschetst.

>[!NOTE]
>
>De objecten `xdm` en `data` zijn optioneel en zijn alleen vereist voor Offer decisioning als u segmenten met voorwaarden hebt gemaakt waarin velden in een van deze objecten worden gebruikt.

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
            }
        },
        "data": {
            "page": {
                "pageInfo": {
                    "pageName": "Promotions",
                    "siteSection": "Home"
                },
                "promos": {
                    "heroPromos": "purse,shoes,sunglasses"
                },
                "customVariables": {
                    "testGroup": "orange/black theme"
                },
                "events": {
                    "homePage": true
                },
                "products": [
                    {
                        "productSKU": "abc123",
                        "productName": "shirt"
                    }
                ]
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Antwoord {#response}

De Edge Network zal een reactie teruggeven gelijkend op hieronder.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Als de bezoeker in aanmerking komt voor een verpersoonlijkingsactiviteit op basis van gegevens die naar [!DNL Offer Decisioning] worden verzonden, wordt de relevante activiteitsinhoud gevonden onder het `handle` -object, waarbij het type `personalization:decisions` is.

Andere inhoud wordt ook geretourneerd onder het object `handle` . Andere inhoudstypen zijn niet relevant voor [!DNL Offer Decisioning] personalisatie. Als de bezoeker in aanmerking komt voor meerdere activiteiten, worden deze opgenomen in een array.

In de onderstaande tabel worden de belangrijkste elementen van dat gedeelte van het antwoord uitgelegd.

| Eigenschap | Beschrijving | Voorbeeld |
|---|---|---|
| `scope` | De reikwijdte van de beslissing die verband hield met de voorgestelde aanbiedingen die werden teruggegeven. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | De unieke id van de aanbiedingsactiviteit. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | De unieke id van de plaatsing van de aanbieding. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | De unieke id van het voorgestelde voorstel. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | De unieke id van het voorgestelde voorstel. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. | `"format": "text/html"` |
| `language` | Een array met talen die zijn gekoppeld aan de inhoud van het voorgestelde aanbod. | `"language": [ "en-US" ]` |
| `content` | De inhoud die aan de voorgestelde aanbieding in het formaat van een koord wordt geassocieerd. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | De afbeeldingsinhoud die aan de voorgestelde aanbieding is gekoppeld, wordt weergegeven in de vorm van een URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON-object dat de kenmerken bevat die aan de voorgestelde aanbieding zijn gekoppeld. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
