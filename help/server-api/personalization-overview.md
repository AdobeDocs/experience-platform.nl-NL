---
title: Inhoud voor personalisatie ophalen uit andere Adobe-oplossingen
description: Leer hoe u de Adobe Experience Platform Edge Network Server-API gebruikt om persoonlijke inhoud op te halen uit de oplossingen voor het aanpassen van Adobe
seo-description: Learn how to use the Adobe Experience Platform Edge Network Server API to retrieve personalized content from Adobe personalization solutions
keywords: personalisatie; server-API; Adobe Experience Platform Edge Network personalisatie ophalen
source-git-commit: 4fd5b5eebdeca065582365343b605a5b9ee695bb
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 7%

---


# Inhoud voor personalisatie ophalen uit Adobe-oplossingen

## Overzicht {#overview}

Met de [!DNL Server API]kunt u persoonlijke inhoud ophalen van Adobe-oplossingen voor personalisatie, waaronder [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) en [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

Daarnaast worden de [!DNL Server API] bevoegdheden personaliseringsmogelijkheden van zelfde pagina en van volgende pagina door de verpersoonlijkingsbestemmingen van Adobe Experience Platform, zoals [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) en de [aangepaste verpersoonlijkingsverbinding](../destinations/catalog/personalization/custom-personalization.md). Om te leren hoe te om Experience Platform voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen, zie [speciale gids](../destinations/ui/configure-personalization-destinations.md).

Wanneer het gebruiken van de Server API, moet u de reactie integreren die door de verpersoonlijkingsmotor met de logica wordt verstrekt die wordt gebruikt om inhoud op uw plaats terug te geven. In tegenstelling tot [Web SDK](../edge/home.md)de [!DNL Server API] heeft geen mechanisme om automatisch inhoud toe te passen die is geretourneerd door [!DNL Adobe Target] en [!DNL Offer Decisioning].

## Terminologie {#terminology}

Alvorens met de oplossingen van de verpersoonlijking van Adobe te werken, zorg ervoor om de volgende concepten te begrijpen:

* **Aanbieding**: een aanbieding is een marketingbericht waaraan regels gekoppeld kunnen zijn die bepalen wie in aanmerking komt om de aanbieding te zien.
* **Besluit**: Een besluit (voorheen bekend als de aanbiedingsactiviteit) brengt de selectie van een aanbieding ter kennis.
* **Schema**: In het schema van een besluit wordt aangegeven welk soort aanbieding is geretourneerd.
* **Toepassingsgebied**: De reikwijdte van het besluit.
   * In Adobe Target is dit de [!DNL mbox]. De [!DNL global mbox] is de `__view__` bereik
   * Voor [!DNL Offer Decisioning], dit zijn de Base64-Gecodeerde koorden van JSON die de activiteit en plaatsings IDs bevatten u de dienst van de offer decisioning wilt gebruiken om aanbiedingen voor te stellen.

## De `query` object {#query-object}

Voor het ophalen van gepersonaliseerde inhoud is een expliciet aanvraagqueryobject voor een aanvraagvoorbeeld vereist. Het queryobject heeft de volgende indeling:

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| Kenmerk | Type | Vereist/optioneel | Beschrijving |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Vereist voor aanpassing van doel. Optioneel voor Offer decisioning. | Lijst van schema&#39;s die in het besluit worden gebruikt, om het type teruggekeerde aanbiedingen te selecteren. |
| `scopes` | `String[]` | Optioneel | Lijst van beslissingsbereik. Maximaal 30 per aanvraag. |

## Het object handle {#handle}

De gepersonaliseerde inhoud die van verpersoonlijkingsoplossingen wordt teruggewonnen wordt voorgesteld in a `personalization:decisions` handle met de volgende notatie voor de lading:

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
| `payload.id` | Tekenreeks | De beslissing-id. |
| `payload.scope` | Tekenreeks | De reikwijdte van de beslissing die tot de voorgestelde aanbiedingen heeft geleid. |
| `payload.scopeDetails.decisionProvider` | Tekenreeks | Instellen op `TGT` bij gebruik van Adobe Target. |
| `payload.scopeDetails.activity.id` | Tekenreeks | De unieke id van de aanbiedingsactiviteit. |
| `payload.scopeDetails.experience.id` | Tekenreeks | De unieke id van de plaatsing van de aanbieding. |
| `items[].id` | Tekenreeks | De unieke id van de plaatsing van de aanbieding. |
| `items[].data.id` | Tekenreeks | De id van de voorgestelde aanbieding. |
| `items[].data.schema` | Tekenreeks | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. |
| `items[].data.format` | Tekenreeks | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. |
| `items[].data.language` | Tekenreeks | Een array met talen die zijn gekoppeld aan de inhoud van het voorgestelde aanbod. |
| `items[].data.content` | Tekenreeks | De inhoud die aan de voorgestelde aanbieding in het formaat van een koord wordt geassocieerd. |
| `items[].data.selector` | Tekenreeks | HTML-kiezer die wordt gebruikt om het DOM-doelelement voor een DOM-actieaanbieding te identificeren. |
| `items[].data.prehidingSelector` | Tekenreeks | HTML-kiezer die wordt gebruikt om het DOM-element te identificeren dat moet worden verborgen tijdens het afhandelen van een DOM-actieaanbieding. |
| `items[].data.deliveryUrl` | Tekenreeks | De afbeeldingsinhoud die aan de voorgestelde aanbieding is gekoppeld, wordt weergegeven in de vorm van een URL. |
| `items[].data.characteristics` | Tekenreeks | Kenmerken van de voorgestelde aanbieding in de vorm van een JSON-object. |

## Voorbeeld-API-aanroep {#sample-call}

**API-indeling**

```http
POST /v2/interact
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
| `configId` | Tekenreeks | Ja | De gegevensstroom-id. |
| `requestId` | Tekenreeks | Nee | Geef een externe id voor het overtrekken van aanvragen op. Als niets wordt verstrekt, zal het Netwerk van de Rand één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |

### Antwoord {#response}

Retourneert een `200 OK` status en een of meer `Handle` objecten, afhankelijk van de Edge-services die zijn ingeschakeld in de configuratie van de gegevensstroom.

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

Meldingen moeten worden geactiveerd wanneer een vooraf ingestelde inhoud of weergave is bezocht of gerenderd aan de eindgebruiker. Om meldingen voor het juiste bereik uit te schakelen, moet u de bijbehorende `id` voor elk toepassingsgebied.

Meldingen aan de rechterkant `id` voor de overeenkomstige werkingsgebieden moeten worden geactiveerd om de rapportage correct weer te geven.

**API-indeling**

```http
POST /ee/v2/collect
```

### Verzoek {#notifications-request}

```shell
url -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
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
| `requestId` | `String` | Nee | Externe id voor overtrekken van externe aanvraag. Als niets wordt verstrekt, zal het Netwerk van de Rand één voor u produceren en zal het terug in de reactielichaam/kopballen terugkeren. |
| `silent` | `Boolean` | Nee | Optionele booleaanse parameter die aangeeft of het Edge-netwerk een `204 No Content` reageren met een lege lading. Kritieke fouten worden gerapporteerd met behulp van de corresponderende HTTP-statuscode en -lading. |

### Antwoord {#notifications-response}

Een geslaagde reactie retourneert een van de volgende statussen en een `requestID` indien in het verzoek geen informatie is verstrekt.

* `202 Accepted` wanneer het verzoek met succes is verwerkt;
* `204 No Content` wanneer de aanvraag met succes is verwerkt en de `silent` parameter is ingesteld op `true`;
* `400 Bad Request` wanneer het verzoek niet correct is geformuleerd (bv. de verplichte primaire identiteit is niet gevonden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
