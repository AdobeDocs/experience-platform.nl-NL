---
title: Opdrachtreacties afhandelen
description: Reacties van opdrachten verwerken met behulp van JavaScript-beloften.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Opdrachtreacties afhandelen

Sommige opdrachten van Web SDK kunnen een object retourneren dat gegevens bevat die mogelijk nuttig zijn voor uw organisatie. U kunt desgewenst kiezen wat u met die gegevens wilt doen. De reacties van het bevel zijn waardevol voor voorstellen en bestemmingen, aangezien zij de gegevens van het Netwerk van de Rand vereisen om effectief te werken.

Opdrachtreacties gebruiken JavaScript [beloften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), die fungeert als een proxy voor een waarde die niet bekend is wanneer de belofte wordt gemaakt. Zodra de waarde gekend is, wordt de belofte &quot;opgelost&quot;met de waarde.

## Opdrachtreacties afhandelen met de web SDK-tagextensie

Maak een regel die zich abonneert op de **[!UICONTROL Send event complete]** gebeurtenis als onderdeel van een regel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Events]selecteert u een bestaande gebeurtenis of maakt u een gebeurtenis.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Event Type] tot **[!UICONTROL Send event complete]**.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

U kunt vervolgens de handelingen opnemen **[!UICONTROL Apply propositions]** of **[!UICONTROL Apply response]** op deze regel.

1. Selecteer een bestaande handeling of maak een handeling wanneer u de hierboven gemaakte of bewerkte regel bekijkt.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Apply propositions]** of **[!UICONTROL Apply response]**, afhankelijk van het gewenste gedrag.
1. Stel de gewenste velden voor de handeling in en klik op **[!UICONTROL Keep Changes]**.

## Opdrachtreacties afhandelen met de Web SDK JavaScript-bibliotheek

Gebruik de `then` en `catch` methoden om te bepalen wanneer een opdracht slaagt of mislukt. U kunt beide weglaten `then` of `catch` als hun doeleinden niet belangrijk zijn voor uw implementatie.

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

Alle beloftes die door opdrachten worden geretourneerd, gebruiken een `result` object. U kunt bijvoorbeeld bibliotheekgegevens opvragen in het dialoogvenster `result` object gebruiken [`getLibraryInfo`](getlibraryinfo.md) opdracht:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

De inhoud van dit `result` is afhankelijk van een combinatie van de opdracht die u gebruikt en de toestemming van de gebruiker. Als een gebruiker geen toestemming heeft gegeven voor een bepaald doel, bevat het reactieobject alleen informatie die kan worden verstrekt in de context van wat de gebruiker heeft toegestaan.
