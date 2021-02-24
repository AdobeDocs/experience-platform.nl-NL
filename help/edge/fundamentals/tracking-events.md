---
title: Gebeurtenissen bijhouden met de SDK van Adobe Experience Platform Web
seo-description: Leer hoe u Adobe Experience Platform Web SDK-gebeurtenissen kunt bijhouden.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---


# Gebeurtenissen bijhouden

Als u gebeurtenisgegevens naar Adobe Experience Cloud wilt verzenden, gebruikt u de opdracht `sendEvent`. Het `sendEvent` bevel is de primaire manier om gegevens naar [!DNL Experience Cloud] te verzenden, en gepersonaliseerde inhoud, identiteiten, en publieksbestemmingen terug te winnen.

Gegevens die naar Adobe Experience Cloud worden verzonden, vallen in twee categorieën:

* XDM-gegevens
* Niet-XDM-gegevens (momenteel niet ondersteund)

## XDM-gegevens verzenden

XDM-gegevens zijn een object waarvan de inhoud en structuur overeenkomen met een schema dat u in Adobe Experience Platform hebt gemaakt. [Meer informatie over het maken van een schema.](../../xdm/tutorials/create-schema-ui.md)

Om het even welke gegevens XDM die u deel van uw analyses, verpersoonlijking, publiek, of bestemmingen zou willen uitmaken zouden moeten worden verzonden gebruikend de `xdm` optie.


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

Er kan enige tijd verstrijken tussen het moment waarop de opdracht `sendEvent` wordt uitgevoerd en het moment waarop de gegevens naar de server worden verzonden (bijvoorbeeld als de SDK-bibliotheek van het Web nog niet volledig is geladen of de toestemming nog niet is ontvangen). Als u een deel van het `xdm`-object wilt wijzigen nadat u de opdracht `sendEvent` hebt uitgevoerd, wordt u ten zeerste aangeraden het `xdm`-object _te klonen voordat_ de opdracht `sendEvent` uitvoert. Bijvoorbeeld:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

In dit voorbeeld wordt de gegevenslaag gekloond door het in series te vervaardigen aan JSON, dan het deserializing van het. Vervolgens wordt het gekloonde resultaat doorgegeven aan de opdracht `sendEvent`. Dit zorgt ervoor dat de opdracht `sendEvent` een momentopname van de gegevenslaag heeft zoals deze bestond toen de opdracht `sendEvent` werd uitgevoerd, zodat latere wijzigingen in het oorspronkelijke object van de gegevenslaag niet worden weerspiegeld in de gegevens die naar de server worden verzonden. Als u een gebeurtenisgestuurde gegevenslaag gebruikt, wordt het klonen van uw gegevens waarschijnlijk al automatisch verwerkt. Als u bijvoorbeeld de [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer/wiki) gebruikt, biedt de methode `getState()` een berekende, gekloonde momentopname van alle eerdere wijzigingen. Dit wordt ook automatisch voor u afgehandeld als u de uitbreiding van SDK van het Web van Adobe Experience Platform in Adobe Experience Platform Launch gebruikt.

>[!NOTE]
>
>Er geldt een limiet van 32 kB voor de gegevens die in elke gebeurtenis in het XDM-veld kunnen worden verzonden.

### Niet-XDM-gegevens verzenden

Het verzenden van gegevens die niet overeenkomen met een XDM-schema wordt momenteel niet ondersteund. De steun is gepland voor een toekomstige datum.

### Instelling `eventType`

In een XDM ervaringsgebeurtenis, is er een facultatief `eventType` gebied. Dit houdt het primaire gebeurtenistype voor het verslag. Door een gebeurtenistype in te stellen kunt u onderscheid maken tussen de verschillende gebeurtenissen die u wilt verzenden. XDM biedt verschillende vooraf gedefinieerde gebeurtenistypen die u kunt gebruiken of u maakt altijd uw eigen aangepaste gebeurtenistypen voor uw gebruiksgevallen. Hieronder vindt u een lijst met alle vooraf gedefinieerde gebeurtenistypen die door XDM worden geleverd. [Lees meer in het openbare XDM-rapport](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **Type gebeurtenis:** | **Definitie:** |
| ---------------------------------- | ------------ |
| advertising.completes | Geeft aan of een getimed media-element is gecontroleerd op voltooiing, wat niet noodzakelijkerwijs betekent dat de kijker de hele video heeft bekeken. viewer had voorsprong kunnen overslaan |
| advertising.timePlayed | Beschrijft de hoeveelheid tijd die door een gebruiker aan een specifiek getimed media activa wordt doorgebracht |
| advertising.federated | Geeft aan of een ervaringsgebeurtenis is gemaakt via gegevensfederatie (gegevensdeling tussen klanten) |
| advertising.clicks | Klikken op acties op een advertentie |
| advertising.conversions | Een vooraf gedefinieerde actie(s) van de klant die een gebeurtenis voor prestatiebeoordeling activeert |
| advertising.firstQuartiles | Een digitale video heeft 25% van de duur bij normale snelheid afgespeeld |
| advertising.impressions | Indrukking(en) van een advertentie voor een eindgebruiker met de mogelijkheid te worden bekeken |
| advertising.midpoints | Een digitale video heeft 50% van de duur bij normale snelheid afgespeeld |
| advertising.starts | Er is een digitale video afgespeeld |
| advertising.thirdQuartiles | Een digitale video heeft 75% van de duur bij normale snelheid afgespeeld |
| web.webpagedetails.pageViews | Weergave(s) van een webpagina is opgetreden |
| web.webinteraction.linkClicks | Klik van een Web-verbinding is voorgekomen |
| commerce.checkouts | Een actie tijdens een uitcheckproces van een productlijst, kan er meer dan één controlegebeurtenis zijn als er veelvoudige stappen in een controleproces zijn. Als er meerdere stappen zijn, worden de informatie over de tijd van de gebeurtenis en de pagina waarnaar wordt verwezen of de ervaring gebruikt om de stap te identificeren die individuele gebeurtenissen in volgorde vertegenwoordigen |
| commerce.productListAdds | Toevoeging van een product aan de productlijst. Voorbeeld van een product dat aan een winkelwagentje wordt toegevoegd |
| commerce.productListOpens | Initialisaties van een nieuwe productlijst. Voorbeeld van een winkelwagentje |
| commerce.productListRemovals | Een product uit een productlijst verwijderen. Voorbeeld: een product wordt uit een winkelwagentje verwijderd |
| commerce.productListReopens | Een productlijst die niet meer toegankelijk (verlaten) was is opnieuw geactiveerd door de gebruiker. Voorbeeld via een hermarketingactiviteit |
| commerce.productListViews | Weergave(s) van een productlijst is opgetreden |
| commerce.productViews | Weergave(s) van een product is/zijn opgetreden |
| commerce.purchases | Er is een bestelling geaccepteerd. De aankoop is de enige vereiste actie in een handelsomzetting. De aanschaf moet een productlijst bevatten waarnaar wordt verwezen |
| commerce.saveForLaters | De productlijst wordt opgeslagen voor toekomstig gebruik. Voorbeeld van een verlanglijst voor een product |
| delivery.feedback | Feedbackgebeurtenissen voor een levering. Voorbeeld van feedbackgebeurtenissen voor een e-maillevering |


Deze gebeurtenistypen worden weergegeven in een vervolgkeuzelijst als u de Adobe Experience Platform Launch-extensie gebruikt of u kunt ze altijd zonder Experience Platform Launch doorgeven. Ze kunnen worden doorgegeven als onderdeel van de optie `xdm`.


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

U kunt ook `eventType` in de gebeurtenisopdracht doorgeven met de optie `type`. Achter de scènes wordt dit toegevoegd aan de XDM-gegevens. Als u `type` als optie hebt, kunt u `eventType` eenvoudiger instellen zonder dat u de XDM-lading hoeft te wijzigen.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### De gegevensset-id overschrijven

In sommige gebruiksgevallen, zou u een gebeurtenis naar een dataset buiten kunnen willen verzenden die in de Configuratie UI wordt gevormd. Hiervoor moet u de optie `datasetId` op het `sendEvent` bevel plaatsen:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Identiteitsgegevens toevoegen

U kunt ook aangepaste identiteitsgegevens toevoegen aan de gebeurtenis. Zie [Experience Cloud-id ophalen](../identity/overview.md).

## De sendBeacon-API gebruiken

Het kan lastig zijn om gebeurtenisgegevens te verzenden vlak voordat de gebruiker van de webpagina weg is genavigeerd. Als de aanvraag te lang duurt, kan de browser de aanvraag annuleren. Sommige browsers hebben een webstandaard-API met de naam `sendBeacon` geïmplementeerd, zodat gegevens tijdens deze periode eenvoudiger kunnen worden verzameld. Wanneer u `sendBeacon` gebruikt, doet de browser het webverzoek in de algemene browsercontext. Dit betekent browser maakt het bakenverzoek op de achtergrond en houdt niet de paginanavigatie op. Als u wilt dat Adobe Experience Platform [!DNL Web SDK] `sendBeacon` gebruikt, voegt u de optie `"documentUnloading": true` toe aan de gebeurtenisopdracht.  Hier volgt een voorbeeld:


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

Browsers hebben limieten ingesteld voor de hoeveelheid gegevens die tegelijk met `sendBeacon` kan worden verzonden. In veel browsers is de limiet 64 kB. Als de browser de gebeurtenis afwijst omdat de lading te groot is, valt Adobe Experience Platform [!DNL Web SDK] terug naar het gebruiken van zijn normale vervoermethode (bijvoorbeeld, halen).

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

## Globaal wijzigen van gebeurtenissen {#modifying-events-globally}

Als u, velden van de gebeurtenis globaal wilt toevoegen verwijderen of wijzigen, kunt u een `onBeforeEventSend` callback vormen.  Deze callback wordt geroepen telkens als een gebeurtenis wordt verzonden.  Deze callback wordt doorgegeven in een gebeurtenisobject met een veld `xdm`.  Wijzig `event.xdm` om de gegevens te wijzigen die in de gebeurtenis worden verzonden.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. Als opties doorgegeven waarden aan de gebeurtenisopdracht `alloy("sendEvent", { xdm: ... });`
2. Automatisch verzamelde waarden.  (Zie [Automatische informatie](../data-collection/automatic-information.md).)
3. De veranderingen die in `onBeforeEventSend` callback worden aangebracht.

Als de `onBeforeEventSend` callback een uitzondering werpt, wordt de gebeurtenis nog verzonden; echter, worden geen van de veranderingen die binnen callback werden aangebracht toegepast op de definitieve gebeurtenis.

## Mogelijke uitvoerbare fouten

Bij het verzenden van een gebeurtenis kan een fout optreden als de gegevens die worden verzonden te groot zijn (meer dan 32 kB voor de volledige aanvraag). In dit geval moet u de hoeveelheid gegevens die wordt verzonden, verminderen.

Wanneer het zuiveren wordt toegelaten, bevestigt de server synchroon gebeurtenisgegevens die tegen het gevormde schema XDM worden verzonden. Als de gegevens niet overeenkomen met het schema, worden gegevens over de niet-overeenkomende gegevens geretourneerd van de server en wordt een fout gegenereerd. In dit geval past u de gegevens aan het schema aan. Wanneer het zuiveren niet wordt toegelaten, controleert de server asynchroon gegevens en, daarom, wordt geen overeenkomstige fout geworpen.
