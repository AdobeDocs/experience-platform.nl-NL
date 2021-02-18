---
title: Koppelingen bijhouden met de Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Koppelingen bijhouden

Koppelingen kunnen handmatig worden ingesteld of automatisch worden bijgehouden [a1/>. ](#automaticLinkTracking) Handmatig bijhouden wordt uitgevoerd door de details onder het gedeelte `web.webInteraction` van het schema toe te voegen. Er zijn drie vereiste variabelen:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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
* **`exit`:** Een afsluitkoppeling

## Automatisch koppelingen bijhouden {#automaticLinkTracking}

Standaard wordt in de SDK van het web geklikt op kwalificeerde koppelingstags, worden de labels en records vastgelegd. Klikken worden vastgelegd met een [capture](https://www.w3.org/TR/uievents/#capture-phase)-klikgebeurtenislistener die aan het document is gekoppeld.

De automatische verbinding het volgen kan door [het vormen ](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) SDK van het Web worden onbruikbaar gemaakt.

```javascript
clickCollectionEnabled: false
```

### Welke markeringen kwalificeren voor verbinding-volgen?{#qualifyingLinks}

De automatische verbinding het volgen wordt gedaan voor ankermarkeringen `A` en `AREA`. Nochtans, worden deze markeringen niet overwogen voor verbinding het volgen als zij `onclick` manager in bijlage hebben.

### Hoe worden koppelingen gelabeld?{#labelingLinks}

Koppelingen worden gelabeld als een downloadkoppeling als de ankertag een downloadkenmerk bevat of als de koppeling eindigt met een populaire bestandsextensie. De downloadkoppelingskwalificatie kan [gevormd ](../fundamentals/configuring-the-sdk.md) met een regelmatige uitdrukking zijn:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

De verbindingen worden geëtiketteerd als uitgangsverbinding als het domein van het verbindingsdoel van huidige `window.location.hostname` verschilt.

Koppelingen die niet als download- of afsluitkoppeling worden gekwalificeerd, worden aangeduid als &quot;other&quot;.
