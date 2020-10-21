---
title: Pagina- en koppelingenbeheer met Adobe Analytics
seo-title: Koppeling bijhouden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: c9d777f4350f0b039608c4f9b01d5206994e2572
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

Terwijl er in het verleden verschillende functies waren om tussen een paginamening en een verbinding (bijvoorbeeld, `s.t(), s.tl()`) te onderscheiden, in het Web SDK is er enkel het `sendEvent` bevel. De gegevens die u met een gebeurtenis verzendt, bepalen of het een paginaweergave of een koppeling moet zijn. [Meer weten over het bijhouden van koppelingen](../track-links.md)?

## Een paginaweergave verzenden

U kunt een paginaweergave opgeven door de `web.webPageDetails.pageViews.value=1` variabele in te stellen.

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
