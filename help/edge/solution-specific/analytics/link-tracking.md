---
title: Pagina- en koppelingenbeheer met Adobe Analytics
seo-title: Koppeling bijhouden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
translation-type: tm+mt
source-git-commit: ab73e4d793cf39c29ddca385487bf027002db883
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

Terwijl er in het verleden verschillende functies waren om tussen een paginamening en een verbinding (bijvoorbeeld, `s.t(), s.tl()`) te onderscheiden, in SDK van het Web is er enkel het `sendEvent` bevel. De gegevens die u met een gebeurtenis verzendt, bepalen of het een paginaweergave of een koppeling moet zijn.

## Een paginaweergave verzenden

U kunt een paginaweergave opgeven door de `web.webPageDetails.pageViews.value=1` variabele in te stellen.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Hoewel analyses technisch gezien een paginaweergave registreren, zelfs als deze variabele niet is ingesteld, is het aan te raden deze variabele in te stellen wanneer u een paginaweergave wilt opnemen om expliciet in uw gegevens te zijn en de implementatie in de toekomst te controleren.

## Koppelingen bijhouden

De verbindingen kunnen worden geplaatst door de details onder het `web.webInteraction` deel van het schema toe te voegen. Er zijn drie vereiste variabelen: `web.webInteraction.name`, `web.webInteraction.type` en `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

Het verbindingstype kan één van drie waarden zijn:

* **`other`:** Een aangepaste koppeling
* **`download`:** Een downloadkoppeling (deze kan automatisch door de bibliotheek worden bijgehouden)
* **`exit`:** Een exit-koppeling

### Automatisch koppelen bijhouden

SDK van het Web kan alle verbindingskliks automatisch volgen door [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)toe te laten.

Downloadkoppelingen worden automatisch gedetecteerd op basis van populaire bestandstypen. De logica voor hoe de downloads worden geclassificeerd is configureerbaar.
