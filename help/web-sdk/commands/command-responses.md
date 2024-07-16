---
title: Opdrachtreacties afhandelen
description: Reacties van opdrachten verwerken met JavaScript-beloften.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Opdrachtreacties afhandelen

Sommige opdrachten van Web SDK kunnen een object retourneren dat gegevens bevat die mogelijk nuttig zijn voor uw organisatie. U kunt desgewenst kiezen wat u met die gegevens wilt doen. De reacties van het bevel zijn waardevol voor voorstellen en bestemmingen, aangezien zij Edge Network gegevens vereisen effectief te werken.

De reacties van het bevel gebruiken JavaScript [ beloften ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), handelend als volmacht voor een waarde die niet gekend is wanneer de belofte wordt gecreeerd. Zodra de waarde gekend is, wordt de belofte &quot;opgelost&quot;met de waarde.

## Opdrachtreacties afhandelen met de web SDK-tagextensie

Maak een regel die als onderdeel van een regel op de gebeurtenis **[!UICONTROL Send event complete]** wordt geabonneerd.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Events] een bestaande gebeurtenis of maak een gebeurtenis.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Event Type] in op **[!UICONTROL Send event complete]** .
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

Vervolgens kunt u de handelingen **[!UICONTROL Apply propositions]** of **[!UICONTROL Apply response]** aan deze regel toevoegen.

1. Selecteer een bestaande handeling of maak een handeling wanneer u de hierboven gemaakte of bewerkte regel bekijkt.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel [!UICONTROL Action Type] in op **[!UICONTROL Apply propositions]** of **[!UICONTROL Apply response]** , afhankelijk van het gewenste gedrag.
1. Stel de gewenste velden voor de handeling in en klik op **[!UICONTROL Keep Changes]** .

## Opdrachtreacties afhandelen met de Web SDK JavaScript-bibliotheek

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
