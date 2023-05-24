---
title: Gegevens verzenden naar Adobe Analytics via de Adobe Experience Platform Web SDK
description: Leer hoe u gegevens naar Adobe Analytics verzendt met de Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Gegevens verzenden naar Adobe Analytics

In het verleden waren er verschillende functies om onderscheid te maken tussen een paginaweergave en een koppeling (bijvoorbeeld `s.t(), s.tl()`), in de SDK van het Web is er alleen de `sendEvent` gebruiken. De gegevens die u met een gebeurtenis verzendt, bepalen of het een paginaweergave of een koppeling moet zijn. [Meer informatie over het bijhouden van koppelingen](../track-links.md).

## Een paginaweergave verzenden

U kunt een paginaweergave opgeven door het dialoogvenster `web.webPageDetails.pageViews.value=1` variabele.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Hoewel Analytics technisch een paginamening registreert zelfs als deze variabele niet wordt geplaatst, is het beste praktijken om deze variabele te plaatsen wanneer u een paginamening wilt registreren om uitdrukkelijk in uw gegevens te zijn en aan toekomstige proefdruk uw implementatie.
