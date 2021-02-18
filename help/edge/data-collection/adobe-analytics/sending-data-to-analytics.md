---
title: Gegevens verzenden naar Adobe Analytics via de Adobe Experience Platform Web SDK
description: Leer hoe u gegevens naar Adobe Analytics verzendt met de Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

Terwijl er in het verleden verschillende functies waren om tussen een paginamening en een verbinding (bijvoorbeeld, `s.t(), s.tl()`) te onderscheiden, in het Web SDK is er enkel het `sendEvent` bevel. De gegevens die u met een gebeurtenis verzendt, bepalen of het een paginaweergave of een koppeling moet zijn. [Meer weten over het bijhouden van koppelingen](../track-links.md)?

## Een paginaweergave verzenden

U kunt een paginaweergave opgeven door de variabele `web.webPageDetails.pageViews.value=1` in te stellen.

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
