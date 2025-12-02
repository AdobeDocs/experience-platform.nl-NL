---
title: Opdrachtreacties afhandelen
description: Reacties van opdrachten verwerken met JavaScript-beloften.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Opdrachtreacties afhandelen

Sommige Web SDK-opdrachten kunnen een object retourneren dat gegevens bevat die mogelijk nuttig zijn voor uw organisatie. U kunt desgewenst kiezen wat u met die gegevens wilt doen. De reacties van het bevel zijn waardevol voor voorstellen en bestemmingen, aangezien zij de gegevens van Edge Network vereisen effectief te werken.

De reacties van het bevel gebruiken JavaScript [&#x200B; beloften &#x200B;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), handelend als volmacht voor een waarde die niet gekend is wanneer de belofte wordt gecreeerd. Zodra de waarde gekend is, wordt de belofte &quot;opgelost&quot;met de waarde.

Gebruik de methoden `then` en `catch` om te bepalen wanneer een opdracht slaagt of mislukt. U kunt `then` of `catch` weglaten als hun doeleinden niet belangrijk voor uw implementatie zijn.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Alle beloftes die door opdrachten worden geretourneerd, gebruiken een `result` -object. U kunt bijvoorbeeld bibliotheekinformatie ophalen van het `result` -object met de opdracht [`getLibraryInfo`](getlibraryinfo.md) :

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

De inhoud van dit `result` -object is afhankelijk van een combinatie van de opdracht die u gebruikt en de toestemming van de gebruiker. Als een gebruiker geen toestemming heeft gegeven voor een bepaald doel, bevat het reactieobject alleen informatie die kan worden verstrekt in de context van wat de gebruiker heeft toegestaan.

## Opdrachtreacties met de webtagextensie SDK

De Web SDK-tagextensie die gelijk is aan opdrachtreacties, is een regel die zich abonneert op de [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete) -gebeurtenis. Vervolgens kunt u handelingen zoals [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) of [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) aan deze regel toevoegen.
