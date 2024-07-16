---
title: Personalization-overzicht
description: Leer hoe u de Adobe Experience Platform Edge Network Server-API gebruikt om persoonlijke inhoud op te halen van de oplossingen voor het aanpassen van Adoben.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 4%

---

# Personalization-overzicht

Met [!DNL Server API], kunt u gepersonaliseerde inhoud van de oplossingen van de de verpersoonlijking van de Adobe terugwinnen, met inbegrip van [ Adobe Target ](https://business.adobe.com/products/target/adobe-target.html), [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home), en [ Offer decisioning ](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=nl).

Bovendien, de [!DNL Server API] bevoegdheden zelfde-pagina en volgende-pagina verpersoonlijkingsmogelijkheden door de verpersoonlijkingsbestemmingen van Adobe Experience Platform, zoals [ Adobe Target ](../destinations/catalog/personalization/adobe-target-connection.md) en de [ verbinding van de douaneverpersoonlijking ](../destinations/catalog/personalization/custom-personalization.md). Leren hoe te om Experience Platform voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen, zie de [ specifieke gids ](../destinations/ui/activate-edge-personalization-destinations.md).

Wanneer het gebruiken van de Server API, moet u de reactie integreren die door de verpersoonlijkingsmotor met de logica wordt verstrekt die wordt gebruikt om inhoud op uw plaats terug te geven. In tegenstelling tot [ SDK van het Web ](../web-sdk/home.md), heeft [!DNL Server API] geen mechanisme om inhoud automatisch toe te passen die door de verpersoonlijkingsoplossingen van de Adobe is teruggekeerd.

## Terminologie {#terminology}

Alvorens met de oplossingen van de verpersoonlijking van de Adobe te werken, zorg ervoor om de volgende concepten te begrijpen:

* **Aanbieding**: een aanbieding is een marketingbericht waaraan regels gekoppeld kunnen zijn die bepalen wie in aanmerking komt om de aanbieding te zien.
* **Besluit**: Een besluit (die eerder als aanbiedingsactiviteit wordt bekend) informeert de selectie van een aanbieding.
* **Schema**: Het schema van een besluit informeert het type van teruggekeerde aanbieding.
* **Reikwijdte**: Het werkingsgebied van het besluit.
   * In Adobe Target is dit de [!DNL mbox] . De [!DNL global mbox] is het `__view__` bereik
   * Voor [!DNL Offer Decisioning], zijn dit de Base64-Gecodeerde koorden van JSON die de activiteit en plaatsings IDs bevatten u de dienst van de offer decisioning wilt gebruiken om aanbiedingen voor te stellen.

## Het object `query` {#query-object}

Voor het ophalen van gepersonaliseerde inhoud is een expliciet aanvraagqueryobject voor een aanvraagvoorbeeld vereist. Het queryobject heeft de volgende indeling:

```json
{
  "query": {
    "personalization": {
      "schemas": [
        "https://ns.adobe.com/personalization/html-content-item",
        "https://ns.adobe.com/personalization/json-content-item",
        "https://ns.adobe.com/personalization/redirect-item",
        "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes": [
        "alloyStore",
        "siteWide",
        "__view__",
        "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
      ],
      "surfaces": [
        "web://mywebpage.html/",
        "web://mywebpage.html/#sample-json-content"
      ]
    }
  }
}
```



| Kenmerk | Type | Vereist/optioneel | Beschrijving |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Vereist voor aanpassing van doel. Optioneel voor Offer decisioning. | Lijst van schema&#39;s die in het besluit worden gebruikt, om het type van teruggekeerde aanbiedingen te selecteren. |
| `scopes` | `String[]` | Optioneel | Lijst van beslissingsbereik. Maximaal 30 per aanvraag. |

## Het object handle {#handle}

De gepersonaliseerde inhoud die van verpersoonlijkingsoplossingen wordt teruggewonnen wordt voorgesteld in een `personalization:decisions` handvat, dat het volgende formaat voor zijn lading heeft:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Kenmerk | Type | Beschrijving |
| --- | --- | --- |
| `payload.id` | String | De beslissing-id. |
| `payload.scope` | String | De reikwijdte van de beslissing die tot de voorgestelde aanbiedingen heeft geleid. |
| `payload.scopeDetails.decisionProvider` | String | Instellen op `TGT` bij gebruik van Adobe Target. |
| `payload.scopeDetails.activity.id` | String | De unieke id van de aanbiedingsactiviteit. |
| `payload.scopeDetails.experience.id` | String | De unieke id van de plaatsing van de aanbieding. |
| `items[].id` | String | De unieke id van de plaatsing van de aanbieding. |
| `items[].data.id` | String | De id van de voorgestelde aanbieding. |
| `items[].data.schema` | String | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. |
| `items[].data.format` | String | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. |
| `items[].data.language` | String | Een array met talen die zijn gekoppeld aan de inhoud van het voorgestelde aanbod. |
| `items[].data.content` | String | De inhoud die aan de voorgestelde aanbieding in het formaat van een koord wordt geassocieerd. |
| `items[].data.selector` | String | HTML-kiezer die wordt gebruikt om het DOM-doelelement voor een DOM-actieaanbieding te identificeren. |
| `items[].data.prehidingSelector` | String | HTML-kiezer die wordt gebruikt om het DOM-element te identificeren dat moet worden verborgen tijdens het afhandelen van een DOM-actieaanbieding. |
| `items[].data.deliveryUrl` | String | De afbeeldingsinhoud die aan de voorgestelde aanbieding is gekoppeld, wordt weergegeven in de vorm van een URL. |
| `items[].data.characteristics` | String | Kenmerken van de voorgestelde aanbieding in de vorm van een JSON-object. |

## Voorbeeld-API-aanroep {#sample-call}

**API formaat**

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
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `configId` | String | Ja | De gegevensstroom-id. |
| `requestId` | String | Nee | Geef een externe overtrekID voor aanvragen op. Als niets wordt verstrekt, zal de Edge Network één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |

### Antwoord {#response}

Retourneert een `200 OK` status en een of meer `Handle` -objecten, afhankelijk van de Edge-services die zijn ingeschakeld in de configuratie van de gegevensstroom.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Meldingen {#notifications}

Meldingen moeten worden geactiveerd wanneer een vooraf ingestelde inhoud of weergave is bezocht of weergegeven aan de eindgebruiker. Als meldingen voor het juiste bereik moeten worden afgebroken, moet u de bijbehorende `id` gegevens voor elk bereik bijhouden.

Meldingen met de juiste waarde `id` voor het corresponderende bereik moeten worden geactiveerd om de rapportage correct weer te geven.

**API formaat**

```http
POST /ee/v2/collect
```

### Verzoek {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | ID van de gegevensstroom die door het eindpunt van de gegevensinzameling wordt gebruikt. |
| `requestId` | `String` | Nee | Externe id voor overtrekken van externe aanvraag. Als niets wordt verstrekt, zal de Edge Network één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |
| `silent` | `Boolean` | Nee | Optionele booleaanse parameter die aangeeft of de Edge Network een `204 No Content` -reactie moet retourneren met een lege lading. Kritieke fouten worden gerapporteerd met behulp van de corresponderende HTTP-statuscode en -lading. |

### Antwoord {#notifications-response}

Een geslaagde reactie retourneert een van de volgende statussen en een `requestID` als er niets in de aanvraag is opgegeven.

* `202 Accepted` wanneer de aanvraag correct is verwerkt;
* `204 No Content` wanneer de aanvraag is verwerkt en de parameter `silent` is ingesteld op `true` ;
* `400 Bad Request` wanneer de aanvraag niet correct is samengesteld (de verplichte primaire identiteit is bijvoorbeeld niet gevonden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
