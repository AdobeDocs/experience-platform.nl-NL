---
title: Gegevensverzameling
description: Leer hoe de Adobe Experience Platform Edge Network Server API de verzamelde gegevens structureert.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 2%

---


# Gegevensverzameling

[!DNL Server API] biedt twee typen eindpunten voor gegevensverzameling:

* [ Interactieve eindpunten van de gegevensinzameling ](interactive-data-collection.md), gebruikt wanneer de cliënt een reactie verwacht dat door de server wordt teruggekeerd. Deze eindpunten kunnen inhoud van andere diensten van de Edge Network ook terugkeren, terwijl het uitvoeren van gegevensinzameling.
* [ de niet-interactieve inzameling van gebeurtenisgegevens ](non-interactive-data-collection.md), wordt gebruikt wanneer geen reactie van de server wordt verwacht. Deze eindpunten worden alleen gebruikt voor gegevensverzameling.

## `Event` -object {#event-object}

De gegevens die door [!DNL Server API] worden verzameld, zijn gestructureerd in het `Event` -object. De structuur van dit object wordt hieronder beschreven.

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
| `xdm` | Object | *Vereiste*. JSON-object met gegevens in XDM-indeling die overeenkomen met het schema van de gegevensset. |
| `data` | Object | *Facultatief*. JSON-object met vrije-formuliergegevens, dat door de Edge Network aan XDM kan worden toegewezen. |

