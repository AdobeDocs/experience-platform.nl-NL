---
title: Koppelingen bijhouden met de Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: dac14cd358922b577c71f8d9b7f7c9b7e1b4f87d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Koppelingen bijhouden

Koppelingen kunnen handmatig worden ingesteld of bijgehouden [automatisch](#automaticLinkTracking). Handmatig bijhouden wordt uitgevoerd door de gegevens onder de `web.webInteraction` deel van het schema. Er zijn drie vereiste variabelen:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

Het verbindingstype kan één van drie waarden zijn:

* **`other`:** Een aangepaste koppeling
* **`download`:** Een downloadkoppeling
* **`exit`:** Een exit-koppeling

Deze waarden zijn [automatisch toegewezen](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics als [geconfigureerd](adobe-analytics/analytics-overview.md) om dit te doen.

## Automatisch koppelingen bijhouden {#automaticLinkTracking}

Standaard wordt in de SDK van het web geklikt op kwalificeerde koppelingstags, worden de labels en records vastgelegd. Klikken worden vastgelegd met een [vastleggen](https://www.w3.org/TR/uievents/#capture-phase) Klik op de gebeurtenislistener die aan het document is gekoppeld.

Het automatisch bijhouden van koppelingen kan worden uitgeschakeld door [configureren](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) de Web SDK.

```javascript
clickCollectionEnabled: false
```

### Welke markeringen kwalificeren voor verbinding-volgen?{#qualifyingLinks}

Automatisch koppelingen bijhouden is uitgevoerd voor anker `A` en `AREA` -tags. Nochtans, worden deze markeringen niet overwogen voor verbinding het volgen als zij een bijlage hebben `onclick` handler.

### Hoe worden koppelingen gelabeld?{#labelingLinks}

Koppelingen worden gelabeld als een downloadkoppeling als de ankertag een downloadkenmerk bevat of als de koppeling eindigt met een populaire bestandsextensie. De downloadkoppelingskwalificatie kan [geconfigureerd](../fundamentals/configuring-the-sdk.md) met een reguliere expressie:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

De verbindingen worden geëtiketteerd als uitgangsverbinding als het domein van het verbindingsdoel van huidige verschilt `window.location.hostname`.

Koppelingen die niet als download- of afsluitkoppeling worden gekwalificeerd, worden aangeduid als &quot;other&quot;.

### Hoe kunnen link-volgende waarden worden gefiltreerd?

De gegevens die met automatische verbinding volgen kunnen worden geïnspecteerd en gefiltreerd door te verstrekken [onBeforeEventSend, callback, functie](../fundamentals/tracking-events.md#modifying-events-globally).

Het filteren van gegevens voor het bijhouden van koppelingen kan handig zijn bij het voorbereiden van gegevens voor rapportage via Analytics. Bij het automatisch bijhouden van koppelingen worden zowel de naam als de URL van de koppeling vastgelegd. In analyserapporten heeft de naam van de koppeling voorrang op de URL van de koppeling. Als u de URL van de koppeling wilt rapporteren, moet de naam van de koppeling worden verwijderd. In het volgende voorbeeld wordt een `onBeforeEventSend` functie die de naam van de koppeling voor downloadkoppelingen verwijdert:

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

