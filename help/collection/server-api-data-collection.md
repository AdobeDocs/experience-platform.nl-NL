---
title: Gegevensverzameling
description: Leer hoe de Adobe Experience Platform Edge Network Server API de verzamelde gegevens structureert
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: gegevensverzameling;verzameling;Adobe Experience Platform Edge Network;api;structuur
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---


# Gegevensverzameling

De [!DNL Server API] biedt twee typen eindpunten voor gegevensverzameling:

* [Interactieve eindpunten voor gegevensverzameling](interactive-data-collection.md), gebruikt wanneer de client verwacht dat een reactie wordt geretourneerd door de server. Deze eindpunten kunnen inhoud van andere diensten van het Netwerk van de Rand ook terugkeren, terwijl het uitvoeren van gegevensinzameling.
* [Niet-interactieve verzameling van gebeurtenisgegevens](non-interactive-data-collection.md), wordt gebruikt wanneer geen reactie van de server wordt verwacht. Deze eindpunten worden alleen gebruikt voor gegevensverzameling.

## `Event` object {#event-object}

Gegevens verzameld door de [!DNL Server API] is gestructureerd in de `Event` object. De structuur van dit object wordt hieronder beschreven.

```json
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
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Kenmerk | Type | Beschrijving |
| --- | --- | --- |
| `xdm` | Object | *Vereist*. JSON-object met gegevens in XDM-indeling die overeenkomen met het schema van de gegevensset. |
| `data` | Object | *Optioneel*. JSON-object met vrije-formuliergegevens, dat door het Edge Network aan XDM kan worden toegewezen. |

