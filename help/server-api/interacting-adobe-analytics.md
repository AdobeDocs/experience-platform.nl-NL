---
title: Interactie met Adobe Analytics
description: Leer hoe u de Edge Network Server-API gebruikt om te communiceren met Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Interactie met Adobe Analytics

## Overzicht {#overview}

Adobe Analytics-gegevensverzameling werkt door XDM-gegevens te vertalen naar een indeling die Adobe Analytics kan begrijpen. Verscheidene gebieden XDM worden [ automatisch in kaart gebracht ](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) aan de variabelen van Analytics. U kunt ook handmatig XDM-waarden toewijzen aan verouderde analytische variabelen.

Om Adobe Analytics toe te laten om gegevens van Server API te ontvangen, moet u uw datastream ](../datastreams/overview.md#adobe-analytics-settings) vormen om gebeurtenissen aan Adobe Analytics door:sturen, door de identiteitskaart van de rapportreeks in te gaan in de de configuratiepagina van de gegevensstroom.[

![ Configuratie van Adobe Analytics DataStream ](assets/analytics-datastream.png)

## Interactie met Adobe Analytics {#interacting-analytics}

### API-indeling {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Verzoek {#request}

Het onderstaande voorbeeld bevat verschillende automatisch toegewezen waarden uit de veldgroep `_experience.analytics` . De klasse bevat ook op JSON gebaseerde gegevenslagen. Terwijl deze gegevenslagen niet automatisch kunnen worden in kaart gebracht, is het mogelijk om [ Prep van Gegevens voor de Inzameling van Gegevens ](../datastreams/data-prep.md) te gebruiken om deze waarden aan een schema in kaart te brengen dat hierboven van verwijzingen voorzien gebiedsgroepen bevat.

Alle waarden die gebruikers toewijzen aan die velden, worden automatisch toegewezen aan de juiste analysewaarden, alsof deze zijn opgenomen in de API-aanvraag.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
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
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
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
      }
   }
}'
```

### Reactie {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
