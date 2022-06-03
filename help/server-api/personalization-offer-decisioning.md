---
title: Personalisatie via Offer decisioning
description: Leer hoe u de server-API gebruikt om persoonlijke ervaringen via Offer decisioning te leveren en te renderen
keywords: personalisatie; server-API; Adobe Experience Platform Edge Network personalisatie ophalen;target;offer decisioning;
source-git-commit: 59cb43007c4a7ff125738c21064381cf833063b2
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# Personalisatie via Offer decisioning

## Overzicht {#overview}

De Edge Network Server-API kan persoonlijke ervaringen bieden die worden beheerd in [offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) naar het webkanaal.

[!DNL Offer Decisioning] ondersteunt een niet-visuele interface voor het maken, activeren en leveren van uw activiteiten en personalisatieervaring.

## Uw gegevensstroom configureren {#configure-your-datastream}

Voordat u de server-API in combinatie met Offer decisioning kunt gebruiken, moet u de Adobe Experience Platform-personalisatie in uw datastreamconfiguratie inschakelen en de **[!UICONTROL Offer Decisioning]** optie.

Zie de [gids over het toevoegen van de diensten aan een gegevensstroom](../edge/datastreams/overview.md#adobe-experience-platform-settings), voor gedetailleerde informatie over hoe Offer decisioning kan worden ingeschakeld.

![UI-afbeelding die het configuratiescherm van de datastream-service weergeeft, met Offer decisioning geselecteerd](assets/aep-od-datastream.png)

## Aanmaken van publiek {#audience-creation}

[!DNL Offer Decisioning] vertrouwt op de Adobe Experience Platform Segmentation Service voor publiekscreatie. U kunt de documentatie voor de [!DNL Segmentation Service] [hier](../segmentation/home.md).

## Bepaling van beslissingsbereik {#creating-decision-scopes}

De [!DNL Offer Decision Engine] gebruikt Adobe Experience Platform-gegevens en [Klantprofielen in realtime](../profile/home.md), samen met de [!DNL Offer Library], om aanbiedingen aan de juiste klanten en kanalen op het juiste ogenblik te leveren.

Meer informatie over de [!DNL Offer Decisioning Engine], zie de toegewijde [documentatie](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html).

Na [configureren, gegevensstroom](#configure-your-datastream), moet u het besluitvormingswerkingsgebied bepalen dat in uw verpersoonlijkingscampagne moet worden gebruikt.

[Beslissingsbereik](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) Dit zijn de Base64-gecodeerde JSON-tekenreeksen die de activiteit- en plaatsings-id&#39;s bevatten die u wilt [!DNL Offer Decisioning Service] te gebruiken bij het voorstellen van voorstellen.

**Beslissingsbereik JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**Base64-gecodeerde tekenreeks met beslissingsbereik**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Nadat u uw aanbiedingen en verzamelingen hebt gemaakt, moet u een [beslissingsbereik](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes).

Kopieer het Base64-Gecodeerde besluitvormingswerkingsgebied. U gebruikt deze in het dialoogvenster `query` object van de Server API-aanvraag.

![UI-afbeelding die de gebruikersinterface van de Offer decisioning weergeeft en het beslissingsbereik markeert.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
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

Een volledig verzoek dat een volledig voorwerp XDM, gegevensvoorwerp en een vraag van de Offer decisioning omvat wordt hieronder geschetst.

>[!NOTE]
>
>De `xdm` en `data` objecten zijn optioneel en zijn alleen vereist voor Offer decisioning als u segmenten hebt gemaakt waarin velden in een van deze objecten worden gebruikt.

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

Het Edge-netwerk retourneert een vergelijkbare reactie als hieronder.

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

Als de bezoeker in aanmerking komt voor een verpersoonlijkingsactiviteit op basis van gegevens die worden verzonden naar [!DNL Offer Decisioning], de relevante inhoud van de activiteit in de `handle` object, waarbij het type `personalization:decisions`.

Andere inhoud wordt geretourneerd onder de `handle` ook. Andere inhoudstypen zijn niet relevant voor [!DNL Offer Decisioning] personalisatie. Als de bezoeker in aanmerking komt voor meerdere activiteiten, worden deze opgenomen in een array.

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

