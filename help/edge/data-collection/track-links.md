---
title: Koppelingen bijhouden met de Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: b22eccb34e98ca2da47fe849492ee464d679d2a0
workflow-type: tm+mt
source-wordcount: '340'
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
      "name":"My Custom Link", // Name that shows up in the custom links report
      "URL":"https://myurl.com", // The URL of the link
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

Deze waarden worden [automatisch toegewezen](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics als [configured](adobe-analytics/analytics-overview.md) dit doet.

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

### Hoe kunnen link-volgende waarden worden gefiltreerd?

De gegevens die met automatische verbinding het volgen worden verzameld kunnen worden geïnspecteerd en worden gefiltreerd door een [onBeforeEventSend callback functie](../fundamentals/tracking-events.md#modifying-events-globally) te verstrekken.

Het filteren van gegevens voor het bijhouden van koppelingen kan handig zijn bij het voorbereiden van gegevens voor rapportage via Analytics. Bij het automatisch bijhouden van koppelingen worden zowel de naam als de URL van de koppeling vastgelegd. In analyserapporten heeft de naam van de koppeling voorrang op de URL van de koppeling. Als u de URL van de koppeling wilt rapporteren, moet de naam van de koppeling worden verwijderd. In het volgende voorbeeld wordt een functie `onBeforeEventSend` getoond die de naam van de koppeling voor downloadkoppelingen verwijdert:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

