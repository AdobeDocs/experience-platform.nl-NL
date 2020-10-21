---
title: Koppeling bijhouden met Adobe Analytics
seo-title: Koppeling bijhouden naar Adobe Analytics met Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '250'
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

Standaard legt de SDK van het Web vast, [etiketteert](#labelingLinks), en [registreert](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/webinteraction.schema.md) klikt op [kwalificerende](#qualifyingLinks) verbindingsmarkeringen. Klikken worden vastgelegd met een [vastleggen](https://www.w3.org/TR/uievents/#capture-phase) , klik op de gebeurtenislistener die aan het document is gekoppeld.

Het onbruikbaar maken van automatische verbinding het volgen kan worden gedaan door SDK van het Web te [vormen](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) .

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
