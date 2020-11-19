---
title: Koppeling bijhouden met Adobe Analytics
seo-title: Koppeling bijhouden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Koppelingen bijhouden

Koppelingen kunnen handmatig worden ingesteld of [automatisch](#automaticLinkTracking)worden bijgehouden. Handmatig bijhouden wordt uitgevoerd door de details onder het `web.webInteraction` gedeelte van het schema toe te voegen. Er zijn drie vereiste variabelen:

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
* **`exit`:** Een exit-koppeling

## Automatisch koppelingen bijhouden {#automaticLinkTracking}

Standaard wordt in de SDK van het web geklikt op kwalificeerde koppelingstags, worden de labels en records vastgelegd. Klikken worden vastgelegd met een [vastleggen](https://www.w3.org/TR/uievents/#capture-phase) , klik op de gebeurtenislistener die aan het document is gekoppeld.

De automatische verbinding het volgen kan worden onbruikbaar gemaakt door SDK van het Web te [vormen](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) .

```javascript
clickCollectionEnabled: false
```

### Welke markeringen kwalificeren voor verbinding-volgen?{#qualifyingLinks}

Het automatisch bijhouden van koppelingen wordt uitgevoerd voor ankerlabels `A` en `AREA` codes. Nochtans, worden deze markeringen niet overwogen voor verbinding het volgen als zij een verbonden `onclick` manager hebben.

### Hoe worden koppelingen gelabeld?{#labelingLinks}

Koppelingen worden gelabeld als een downloadkoppeling als de ankertag een downloadkenmerk bevat of als de koppeling eindigt met een populaire bestandsextensie. De downloadkoppelingskwalificatie kan met een regelmatige uitdrukking worden [gevormd](../fundamentals/configuring-the-sdk.md) :

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

De verbindingen worden geëtiketteerd als uitgangsverbinding als het domein van het verbindingsdoel van het huidige `window.location.hostname`.

Koppelingen die niet als download- of afsluitkoppeling worden gekwalificeerd, worden aangeduid als &quot;other&quot;.
