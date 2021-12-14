---
title: Gebeurtenissen bijhouden met de SDK van Adobe Experience Platform Web
description: Leer hoe u Adobe Experience Platform Web SDK-gebeurtenissen kunt bijhouden.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Gebeurtenissen bijhouden

Als u gebeurtenisgegevens naar Adobe Experience Cloud wilt verzenden, gebruikt u de opdracht `sendEvent` gebruiken. De `sendEvent` bevel is de primaire manier om gegevens naar te verzenden [!DNL Experience Cloud]en om gepersonaliseerde inhoud, identiteiten, en publieksbestemmingen terug te winnen.

Gegevens die naar Adobe Experience Cloud worden verzonden, vallen in twee categorieën:

* XDM-gegevens
* Niet-XDM-gegevens

## XDM-gegevens verzenden

XDM-gegevens zijn een object waarvan de inhoud en structuur overeenkomen met een schema dat u in Adobe Experience Platform hebt gemaakt. [Meer informatie over het maken van een schema.](../../xdm/tutorials/create-schema-ui.md)

Om het even welke gegevens XDM die u deel van uw analyses, verpersoonlijking, publiek, of bestemmingen zou willen zijn zouden moeten worden verzonden gebruikend `xdm` optie.


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

Er kan enige tijd verstrijken tussen de `sendEvent` wordt uitgevoerd en wanneer het gegeven wordt verzonden naar de server (bijvoorbeeld, als de bibliotheek van SDK van het Web niet volledig geladen of de toestemming nog niet is ontvangen). Als u van plan bent om het even welk deel van te wijzigen `xdm` object nadat het is uitgevoerd `sendEvent` wordt aangeraden de `xdm` object _voor_ het uitvoeren van `sendEvent` gebruiken. Bijvoorbeeld:

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

In dit voorbeeld wordt de gegevenslaag gekloond door het in series te vervaardigen aan JSON, dan het deserializing van het. Vervolgens wordt het gekloonde resultaat doorgegeven aan het `sendEvent` gebruiken. Zo zorgt u ervoor dat de `sendEvent` bevel heeft een momentopname van de gegevenslaag zoals het bestond toen `sendEvent` werd bevel uitgevoerd zodat de recentere wijzigingen in het originele voorwerp van de gegevenslaag niet in de gegevens zullen worden weerspiegeld die naar de server worden verzonden. Als u een gebeurtenisgestuurde gegevenslaag gebruikt, wordt het klonen van uw gegevens waarschijnlijk al automatisch verwerkt. Als u bijvoorbeeld de opdracht [Gegevenslaag Adobe-client](https://github.com/adobe/adobe-client-data-layer/wiki)de `getState()` Deze methode biedt een berekende, gekloonde momentopname van alle eerdere wijzigingen. Dit wordt ook automatisch voor u afgehandeld als u de de marktextensie van SDK van het Web van Adobe Experience Platform gebruikt.

>[!NOTE]
>
>Er geldt een limiet van 32 kB voor de gegevens die in elke gebeurtenis in het XDM-veld kunnen worden verzonden.


## Niet-XDM-gegevens verzenden

Gegevens die niet overeenkomen met een XDM-schema moeten worden verzonden met de opdracht `data` de `sendEvent` gebruiken. Deze eigenschap wordt gesteund in versies 2.5.0 en hoger van het Web SDK.

Dit is handig als u een Adobe Target-profiel moet bijwerken of kenmerken van Target Recommendations moet verzenden. [Meer informatie over deze doelfuncties.](../personalization/adobe-target/target-overview.md#single-profile-update)

In de toekomst kunt u de volledige gegevenslaag onder de `data` en deze toewijzen aan de XDM-server.

**Profiel en Recommendations-kenmerken verzenden naar Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Instelling `eventType` {#event-types}

In XDM ExperienceEvent-schema&#39;s is er een optionele `eventType` veld. Dit houdt het primaire gebeurtenistype voor het verslag. Door een gebeurtenistype in te stellen kunt u onderscheid maken tussen de verschillende gebeurtenissen die u wilt verzenden. XDM biedt verschillende vooraf gedefinieerde gebeurtenistypen die u kunt gebruiken of u maakt altijd uw eigen aangepaste gebeurtenistypen voor uw gebruiksgevallen. Raadpleeg de XDM-documentatie voor een [lijst met alle vooraf gedefinieerde gebeurtenistypen](../../xdm/classes/experienceevent.md#eventType).

Deze gebeurtenistypen worden weergegeven in een vervolgkeuzelijst als u de tagextensie gebruikt of u kunt ze altijd zonder tags doorgeven. Ze kunnen worden doorgegeven als onderdeel van het `xdm` optie.


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

Als alternatief kan de `eventType` kan worden doorgegeven aan de gebeurtenisopdracht met de opdracht `type` optie. Achter de scènes wordt dit toegevoegd aan de XDM-gegevens. De `type` als een optie u gemakkelijker kunt plaatsen `eventType` zonder dat u de XDM-lading hoeft te wijzigen.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### De gegevensset-id overschrijven

In sommige gebruiksgevallen, zou u een gebeurtenis naar een dataset buiten kunnen willen verzenden die in de Configuratie UI wordt gevormd. Hiervoor moet u de `datasetId` de optie `sendEvent` opdracht:


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

Het kan lastig zijn om gebeurtenisgegevens te verzenden vlak voordat de gebruiker van de webpagina weg is genavigeerd. Als de aanvraag te lang duurt, kan de browser de aanvraag annuleren. Sommige browsers hebben een webstandaard-API geïmplementeerd, genaamd `sendBeacon` om gegevens tijdens deze periode gemakkelijker te kunnen verzamelen. Wanneer u `sendBeacon`De browser doet de webaanvraag in de algemene browsercontext. Dit betekent browser maakt het bakenverzoek op de achtergrond en houdt niet de paginanavigatie op. Adobe Experience Platform vertellen [!DNL Web SDK] te gebruiken `sendBeacon`, voegt u de optie toe `"documentUnloading": true` naar de gebeurtenisopdracht.  Hier volgt een voorbeeld:


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

Browsers hebben limieten ingesteld voor de hoeveelheid gegevens die kan worden verzonden `sendBeacon` in één keer. In veel browsers is de limiet 64 kB. Als de browser de gebeurtenis afwijst omdat de lading te groot is, Adobe Experience Platform [!DNL Web SDK] valt terug naar het gebruiken van zijn normale vervoermethode (bijvoorbeeld, halen).

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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### De `result` object

De `sendEvent` bevel keert een belofte terug die met een wordt opgelost `result` object. De `result` object bevat de volgende eigenschappen:

**voorstellen**: De personalisatie biedt aan dat de bezoeker voor heeft gekwalificeerd. [Meer weten over voorstellen?](../personalization/rendering-personalization-content.md#manually-rendering-content)

**besluiten**: Deze eigenschap is vervangen. Gebruik `propositions` in plaats daarvan.

**bestemmingen**: Segmenten uit Adobe Experience Platform die kunnen worden gedeeld met externe personalisatieplatforms, contentbeheersystemen, servers en andere toepassingen die op websites van klanten worden uitgevoerd. [Meer informatie over doelen.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

**conclusies**: Inzichten in real-time machine leren. [Meer informatie over real-time leren van machines.](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/real-time-machine-learning/home.html?lang=en)

>[!WARNING]
>
>`inferences` is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.



## Gebeurtenissen globaal wijzigen {#modifying-events-globally}

Als u velden wilt toevoegen aan, verwijderen uit of wijzigen uit de gebeurtenis, kunt u een `onBeforeEventSend` callback.  Deze callback wordt geroepen telkens als een gebeurtenis wordt verzonden.  Deze callback wordt doorgegeven in een gebeurtenisobject met een `xdm` veld.  Wijzigen `content.xdm` om de gegevens te wijzigen die met de gebeurtenis worden verzonden.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` velden worden in deze volgorde ingesteld:

1. Waarden die als opties worden doorgegeven aan de gebeurtenisopdracht `alloy("sendEvent", { xdm: ... });`
2. Automatisch verzamelde waarden.  (Zie [Automatische informatie](../data-collection/automatic-information.md).)
3. De in de `onBeforeEventSend` callback.

Enkele opmerkingen over de `onBeforeEventSend` callback:

* Gebeurtenis XDM kan tijdens callback worden gewijzigd. Nadat de callback is geretourneerd, worden eventuele gewijzigde velden en waarden van de content.xdm- en content.data-objecten verzonden met de gebeurtenis.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Als callback een uitzondering genereert, wordt de verwerking voor de gebeurtenis stopgezet en wordt de gebeurtenis niet verzonden.
* Als de callback de booleaanse waarde van `false`, wordt de verwerking van gebeurtenissen beëindigd zonder een fout en wordt de gebeurtenis niet verzonden. Met dit mechanisme kunnen bepaalde gebeurtenissen eenvoudig worden genegeerd door de gebeurtenisgegevens te bekijken en te retourneren `false` als de gebeurtenis niet moet worden verzonden.

   >[!NOTE]
   >Let erop dat u niet de fout retourneert bij de eerste gebeurtenis op een pagina. Als u false retourneert op de eerste gebeurtenis, kan dit een negatieve invloed hebben op de personalisatie.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Elke andere geretourneerde waarde dan de booleaanse waarde `false` De gebeurtenis kan na de callback worden verwerkt en verzonden.

* Gebeurtenissen kunnen worden gefilterd door het gebeurtenistype te bekijken (zie [Gebeurtenistypen](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Mogelijke uitvoerbare fouten

Bij het verzenden van een gebeurtenis kan een fout optreden als de gegevens die worden verzonden te groot zijn (meer dan 32 kB voor de volledige aanvraag). In dit geval moet u de hoeveelheid gegevens die wordt verzonden, verminderen.
