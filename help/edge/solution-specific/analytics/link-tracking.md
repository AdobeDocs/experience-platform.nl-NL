---
title: Pagina- en koppelingenbeheer met Adobe Analytics
seo-title: Koppeling bijhouden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8840e00ec3aa28d43c371b793da4a4b9bfc8d259
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Gegevens verzenden naar Adobe Analytics

Terwijl er in het verleden verschillende functies waren om tussen een paginamening en een verbinding (bijvoorbeeld, `s.t(), s.tl()`) te onderscheiden, in het Web SDK is er enkel het `sendEvent` bevel. De gegevens die u met een gebeurtenis verzendt, bepalen of het een paginaweergave of een koppeling moet zijn.

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

Hoewel analyses technisch gezien een paginaweergave registreren, zelfs als deze variabele niet is ingesteld, is het aan te raden deze variabele in te stellen wanneer u een paginaweergave wilt opnemen om expliciet in uw gegevens te worden opgenomen en om in de toekomst uw implementatie te controleren.

## Koppelingen bijhouden

Koppelingen kunnen handmatig worden ingesteld of [automatisch](#automaticLinkTracking)worden bijgehouden. Handmatig bijhouden wordt uitgevoerd door de details onder het `web.webInteraction` gedeelte van het schema toe te voegen. Er zijn drie vereiste variabelen: `web.webInteraction.name`, `web.webInteraction.type` en `web.webInteraction.linkClicks.value`.

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
  }
});
```

Het verbindingstype kan één van drie waarden zijn:

* **`other`:** Een aangepaste koppeling
* **`download`:** Een downloadkoppeling
* **`exit`:** Een exit-koppeling

### Automatisch koppelen bijhouden {#automaticLinkTracking}

Standaard legt de SDK van het Web vast, [etiketteert](#labelingLinks), en [registreert](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) klikt op [kwalificerende](#qualifyingLinks) verbindingsmarkeringen. Klikken worden vastgelegd met een [vastleggen](https://www.w3.org/TR/uievents/#capture-phase) , klik op de gebeurtenislistener die aan het document is gekoppeld.

Het onbruikbaar maken van automatische verbinding het volgen kan worden gedaan door SDK van het Web te [vormen](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) .

```javascript
clickCollectionEnabled: false
```

#### Welke markeringen kwalificeren voor verbinding-volgen?{#qualifyingLinks}

Het automatisch bijhouden van koppelingen wordt uitgevoerd voor ankerlabels `A` en `AREA` codes. Nochtans, worden deze markeringen niet overwogen voor verbinding het volgen als zij een verbonden `onclick` manager hebben.

#### Hoe worden koppelingen gelabeld?{#labelingLinks}

Koppelingen worden gelabeld als een downloadkoppeling als de ankertag een downloadkenmerk bevat of als de koppeling eindigt met een populaire bestandsextensie. De downloadkoppelingskwalificatie kan met een regelmatige uitdrukking worden [gevormd](../../fundamentals/configuring-the-sdk.md) :

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

De verbindingen worden geëtiketteerd als uitgangsverbinding als het domein van het verbindingsdoel van het huidige `window.location.hostname`.

Koppelingen die niet als download- of afsluitkoppeling worden gekwalificeerd, worden aangeduid als &quot;other&quot;.
