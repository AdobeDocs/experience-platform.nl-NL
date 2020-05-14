---
title: Gebeurtenissen bijhouden
seo-title: Gebeurtenissen van Adobe Experience Platform Web SDK bijhouden
description: Leer hoe te om de gebeurtenissen van het Web SDK van het Platform van de Ervaring te volgen
seo-description: Leer hoe te om de gebeurtenissen van het Web SDK van het Platform van de Ervaring te volgen
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Gebeurtenissen bijhouden

Gebruik de `sendEvent` opdracht om gebeurtenisgegevens naar de Adobe Experience Cloud te verzenden. Het `sendEvent` bevel is de primaire manier om gegevens naar de Wolk van de Ervaring te verzenden, en gepersonaliseerde inhoud, identiteiten, en publieksbestemmingen terug te winnen.

Gegevens die naar Adobe Experience Cloud worden verzonden, vallen in twee categorieën:

* XDM-gegevens
* Niet-XDM-gegevens (momenteel niet ondersteund)

## XDM-gegevens verzenden

XDM-gegevens zijn een object waarvan de inhoud en structuur overeenkomen met een schema dat u hebt gemaakt in het Adobe Experience Platform. [Meer informatie over het maken van een schema.](../../xdm/tutorials/create-schema-ui.md)

Om het even welke gegevens XDM u deel van uw analyses, verpersoonlijking, publiek, of bestemmingen zou moeten worden verzonden gebruikend de `xdm` optie.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

>[!NOTE]
>Er geldt een limiet van 32 kB voor de gegevens die in elke gebeurtenis in het XDM-veld kunnen worden verzonden.

### Niet-XDM-gegevens verzenden

Het verzenden van gegevens die niet overeenkomen met een XDM-schema wordt momenteel niet ondersteund. De steun is gepland voor een toekomstige datum.

### Instelling `eventType`

In een XDM ervaringsgebeurtenis, is er een `eventType` gebied. Dit houdt het primaire gebeurtenistype voor het verslag. Dit kan als deel van de `xdm` optie worden overgegaan.

```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

U kunt de opdracht ook aan de gebeurtenisopdracht `eventType` doorgeven met de `type` optie. Achter de scènes wordt dit toegevoegd aan de XDM-gegevens. Als u de optie `type` als een optie hebt, kunt u de XDM-lading eenvoudiger instellen `eventType` zonder dat u de XDM-lading hoeft te wijzigen.

```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## De sendBeacon-API gebruiken

Het kan lastig zijn om gebeurtenisgegevens te verzenden vlak voordat de gebruiker van de webpagina weg is genavigeerd. Als de aanvraag te lang duurt, kan de browser de aanvraag annuleren. Sommige browsers hebben een webstandaard-API geïmplementeerd, die wordt aangeroepen `sendBeacon` om gegevens tijdens deze periode gemakkelijker te kunnen verzamelen. Wanneer `sendBeacon`de browser wordt gebruikt, wordt de webaanvraag uitgevoerd in de algemene browsercontext. Dit betekent browser maakt het bakenverzoek op de achtergrond en houdt niet de paginanavigatie op. Als u de Adobe Experience Platform Web SDK wilt laten gebruiken, voegt u de optie toe `sendBeacon``"documentUnloading": true` aan de gebeurtenisopdracht.  Hier volgt een voorbeeld:

```javascript
alloy("sendEvent", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Browsers hebben limieten ingesteld voor de hoeveelheid gegevens die `sendBeacon` tegelijk kan worden verzonden. In veel browsers is de limiet 64 kB. Als de browser de gebeurtenis afwijst omdat de lading te groot is, wordt de SDK van het Web van het Platform van de Ervaring van Adobe teruggezet naar het gebruiken van zijn normale vervoermethode (bijvoorbeeld, haal).

## Reacties van gebeurtenissen afhandelen

Als u een reactie van een gebeurtenis wilt afhandelen, kunt u als volgt op de hoogte worden gesteld van een succes of mislukking:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Gebeurtenissen globaal wijzigen {#modifying-events-globally}

Als u velden wilt toevoegen aan, verwijderen uit of wijzigen uit de gebeurtenis, kunt u een `onBeforeEventSend` callback configureren.  Deze callback wordt geroepen telkens als een gebeurtenis wordt verzonden.  Deze callback wordt doorgegeven in een gebeurtenisobject met een `xdm` veld.  Wijzigen `event.xdm` om de gegevens te wijzigen die in de gebeurtenis worden verzonden.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` velden worden in deze volgorde ingesteld:

1. Waarden die als opties worden doorgegeven aan de gebeurtenisopdracht `alloy("sendEvent", { xdm: ... });`
2. Automatisch verzamelde waarden.  (Zie [Automatische informatie](../reference/automatic-information.md).)
3. De wijzigingen die zijn aangebracht in de `onBeforeEventSend` callback.

Als callback een uitzondering werpt, wordt de gebeurtenis nog verzonden; `onBeforeEventSend` echter, worden geen van de veranderingen die binnen callback werden aangebracht toegepast op de definitieve gebeurtenis.

## Mogelijke uitvoerbare fouten

Bij het verzenden van een gebeurtenis kan een fout optreden als de gegevens die worden verzonden te groot zijn (meer dan 32 kB voor de volledige aanvraag). In dit geval moet u de hoeveelheid gegevens die wordt verzonden verminderen.

Wanneer het zuiveren wordt toegelaten, bevestigt de server synchroon gebeurtenisgegevens die tegen het gevormde schema XDM worden verzonden. Als de gegevens niet overeenkomen met het schema, worden gegevens over de niet-overeenkomende gegevens geretourneerd van de server en wordt een fout gegenereerd. In dit geval past u de gegevens aan het schema aan. Wanneer het zuiveren niet wordt toegelaten, controleert de server asynchroon gegevens en, daarom, wordt geen overeenkomstige fout geworpen.
