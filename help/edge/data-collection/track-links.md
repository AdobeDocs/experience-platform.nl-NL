---
title: Koppelingen bijhouden met de Adobe Experience Platform Web SDK
description: Leer hoe te om Gegevens van de Verbinding naar Adobe Analytics met het Web SDK van het Experience Platform te verzenden
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: edf33d0d5991aed5c0535d0e7010aef082bcf48a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Koppelingen bijhouden

Koppelingen kunnen handmatig worden ingesteld of bijgehouden [automatisch](#automaticLinkTracking). Handmatig bijhouden wordt uitgevoerd door de gegevens onder de `web.webInteraction` deel van het schema. Er zijn twee vereiste variabelen:

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

Vanaf versie 2.15.0 legt de SDK van het Web de `region` van het aangeklikte HTML-element. Hierdoor wordt de [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) rapportagefuncties in Adobe Analytics.

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

Vanaf Web SDK versie 2.15.0 kunnen de gegevens die met automatische link tracking worden verzameld, worden geïnspecteerd, aangevuld of gefilterd door een [onBeforeLinkClickSend, callback-functie](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Deze callback functie wordt uitgevoerd slechts wanneer een automatische gebeurtenis van de verbindingsklik voorkomt.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Wanneer het filtreren van de verbinding het volgen gebeurtenissen gebruikend `onBeforeLinkClickSend` opdracht, Adobe raadt aan terug te keren `false` voor de koppeling klikt u die u niet wilt bijhouden. Om het even welke andere reactie zal SDK van het Web de gegevens naar het Netwerk van de Rand verzenden.


>[!NOTE]
>
>** Wanneer beide `onBeforeEventSend` en `onBeforeLinkClickSend` callback-functies worden ingesteld, de Web SDK voert de `onBeforeLinkClickSend` callback-functie om de gebeurtenis link click te filteren en aan te vullen, gevolgd door de `onBeforeEventSend` callback-functie.