---
title: Het vergelijken bij.js met het Web SDK van het Experience Platform
description: Leer hoe de at.js eigenschappen met Experience Platform Web SDK vergelijken
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;system diagram;diagram
source-git-commit: 6efb40e90cb8c29a0141bb0db6e20cec23f2be9a
workflow-type: tm+mt
source-wordcount: '2277'
ht-degree: 2%

---

# Het vergelijken van de bibliotheek at.js met het Web SDK

## Overzicht

Dit artikel biedt een overzicht van de verschillen tussen de `at.js` bibliotheek en de Experience Platform Web SDK.

## Bibliotheken installeren

### Installeer at.js

Onze klanten kunnen de bibliotheek rechtstreeks downloaden via het tabblad Implementatie van Adobe Experience Cloud. De bibliotheek at.js wordt aangepast met montages die de klant als heeft: clientCode, imsOrgId, enz.

### De SDK van het Web installeren

De vooraf gebouwde versie is beschikbaar op een CDN. U kunt de bibliotheek op CDN rechtstreeks op uw pagina van verwijzingen voorzien, of het downloaden en ontvangen op uw eigen infrastructuur. Het is beschikbaar in geminiatuurde en ongeminificeerde formaten. De ongeminificeerde versie is handig voor foutopsporingsdoeleinden.

URL-structuur: https://cdn1.adoberesources.net/alloy/[VERSIE]/alloy.min.js OR alloy.js voor de niet-geminificeerde versie.

Bijvoorbeeld:

* Gepiliseerd: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Niet-geminificeerd: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)

[Meer informatie](../../fundamentals/installing-the-sdk.md)

## De bibliotheken configureren

### Bij.js configureren

Aan het einde van elk bestand at.js vindt u een sectie waarin we een instellingsobject instantiëren en doorgeven. Het is aanpasbaar, bij het downloaden vullen wij die sectie met huidige klantenmontages.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)


### De SDK van het Web configureren

De configuratie voor de SDK wordt uitgevoerd met de `configure` gebruiken.

>[!IMPORTANT]
>
>`configure` is *altijd* het eerste geroepen bevel.

Voorbeeld:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Er zijn vele opties die tijdens configuratie kunnen worden geplaatst. Alle opties vindt u hieronder, gegroepeerd op categorie.

[Meer informatie](../../fundamentals/configuring-the-sdk.md)


## Aanbiedingen voor het laden van pagina&#39;s aanvragen en automatisch renderen

### At.js gebruiken

Bij .js 2.x gebruiken als u de instelling `pageLoadEnabled`, zal de bibliotheek een vraag aan de Rand van het Doel met teweegbrengen `execute -> pageLoad`. Als alle instellingen op de standaardwaarden zijn ingesteld, is geen aangepaste codering nodig. Nadat at.js aan de pagina is toegevoegd en door de browser is geladen, wordt een doelEdge-aanroep uitgevoerd.

### Web SDK gebruiken

Inhoud die is gemaakt in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kan automatisch worden opgehaald en gerenderd door de SDK.

Om de aanbiedingen van het Doel te verzoeken en automatisch terug te geven, gebruik `sendEvent` en stelt de `renderDecisions` optie voor `true`. Hierdoor wordt de SDK gedwongen om alle gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering, automatisch te renderen.

Voorbeeld:

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
});
```

SDK van het Web van het Experience Platform verzendt automatisch een bericht met de aanbiedingen die door WEB SDK werden uitgevoerd, is dit een voorbeeld van hoe een lading van het berichtverzoek als kijkt:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Meer informatie](../rendering-personalization-content.md)

## Aanbiedingen voor het laden van pagina&#39;s aanvragen en NIET automatisch renderen

### At.js gebruiken

Er zijn twee manieren wij een vraag aan de Rand van het Doel konden in brand steken die aanbiedingen voor pagina-lading zal halen.

Voorbeeld 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Voorbeeld 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)

### Web SDK gebruiken

Een `sendEvent` bevel met een bijzonder toepassingsgebied onder `decisionScopes`: `__view__`. Wij gebruiken dit werkingsgebied als signaal om alle pagina-lading activiteiten van Doel te halen en alle meningen vooraf in te stellen. SDK van het Web zal ook proberen om alle VEC mening gebaseerde activiteiten te evalueren. Het uitschakelen van weergave-prefetching wordt momenteel niet ondersteund in de Web SDK.

Om tot om het even welke verpersoonlijkingsinhoud toegang te hebben, kunt u een callback functie verstrekken, die zal worden geroepen nadat SDK een succesvolle reactie van de server ontvangt. Uw callback wordt verstrekt een resultaatvoorwerp, dat voorzetbezit kan bevatten die om het even welke teruggekeerde verpersoonlijkingsinhoud bevatten.

Voorbeeld:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Meer informatie](../rendering-personalization-content.md#manually-rendering-content)


## Specifieke doelvakken voor formulieren aanvragen


### At.js gebruiken

U kunt op formulier gebaseerde Composer-activiteiten ophalen met de opdracht `getOffer` functie:

Voorbeeld 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Voorbeeld 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)


### Web SDK gebruiken

U kunt op formulier gebaseerde Composer-activiteiten ophalen met de opdracht `sendEvent` en geeft u de mbox-namen door onder het dialoogvenster `decisionScopes` optie. De `sendEvent` command retourneert een promise die wordt opgelost met een object dat de gevraagde activiteiten / voorstellen bevat: Zo ziet het `propositions` array ziet er als volgt uit:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Voorbeeld:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Meer informatie](../rendering-personalization-content.md#manually-rendering-content)

## Hoe de doelactiviteiten worden toegepast

### At.js gebruiken

U kunt de doelactiviteiten toepassen met behulp van de `applyOffers` functie: `adobe.target.applyOffer(options)`

Voorbeeld:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=en)

### Web SDK gebruiken

Deze functie wordt momenteel niet ondersteund in Web SDK.

## Hoe kan ik gebeurtenissen volgen?

### At.js gebruiken

U kunt gebeurtenissen volgen door `trackEvent` functie of gebruik `sendNotifications`.

Deze functie voert een verzoek in om gebruikersacties, zoals kliks en omzettingen te melden. Het levert geen activiteiten in de reactie.


**Voorbeeld 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Voorbeeld 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=en)

### Web SDK gebruiken

U kunt gebeurtenissen en gebruikersacties volgen door `sendEvent` opdracht, vullen `_experience.decisioning.propositions` XDM-veldgroep en het instellen van de `eventType` tot een van de twee waarden:

* `decisioning.propositionDisplay`: Geeft aan dat de doelactiviteit wordt gerenderd.
* `decisioning.propositionInteract`: Geeft een gebruikersinteractie met de activiteit aan, zoals een muisklik.

De `_experience.decisioning.propositions` XDM fieldGroup is een array met objecten. De eigenschappen van elk object worden afgeleid van de `result.propositions` die wordt geretourneerd in het dialoogvenster `sendEvent` opdracht: `{ id, scope, scopeDetails }`

**Voorbeeld 1 - Een track `decisioning.propositionDisplay` gebeurtenis na het renderen van een activiteit**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```

**Voorbeeld 2 - Een track `decisioning.propositionInteract` gebeurtenis na klikken vindt metrisch plaats**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Meer informatie](../rendering-personalization-content.md#manually-rendering-content)

## Een weergavewijziging activeren in een toepassing voor één pagina

### At.js gebruiken

Gebruik de `adobe.target.triggerView` functie. Deze functie kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven. adobe.target.triggerView () zou voor enige paginatoepassingen (SPA) moeten worden uitgevoerd om Visual Experience Composer (VEC) te gebruiken om A/B Tests en Ervaring te creëren richtend (XT) activiteiten. Als adobe.target.triggerView() niet is geïmplementeerd op de site, kan de VEC niet worden gebruikt voor SPA.

**Voorbeeld**

```javascript
adobe.target.triggerView("homeView")
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=en)


### Web SDK gebruiken

Als u een weergavewijziging van één pagina wilt activeren of signaleren, stelt u de optie `web.webPageDetails.viewName` eigendom onder de `xdm` de `sendEvent` gebruiken. De SDK van het Web zal het meningsgeheime voorgeheugen controleren, als er aanbiedingen voor zijn `viewName` gespecificeerd in `sendEvent` deze wordt uitgevoerd en er wordt een weergavemeldingsgebeurtenis verzonden.

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Meer informatie](./spa-implementation.md#implementing-xdm-views)

## Respontokens gebruiken

Tot de personalisatie-inhoud die door Adobe Target wordt geretourneerd, behoren [reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het gebruikersinterface van Adobe Target worden gevormd.

### At.js gebruiken

Gebruik at.js aangepaste gebeurtenissen om te luisteren naar de reactie van het Doel en de reactietokens te lezen.

**Voorbeeld**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)


### Web SDK gebruiken

>[!IMPORTANT]
>
>Zorg ervoor dat u versie 2.6.0 van SDK van het Web van Platforms of later gebruikt.

De reactietokens worden geretourneerd als onderdeel van de `propositions` die worden blootgesteld in het resultaat van de `sendEvent` gebruiken. Elk voorstel bevat een array van `items`en elk item bevat een `meta` -object gevuld met antwoordtokens als deze zijn ingeschakeld in de interface van Target-beheerder. [Meer informatie](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)

**Voorbeeld**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Meer informatie](./accessing-response-tokens.md)

## Flikkering beheren

### At.js gebruiken

Met at.js kunt u flikkering beheren door de instelling `bodyHidingEnabled: true` zodat at.js de container die de gepersonaliseerde containers voorverbergt alvorens het ophaalt en de DOM-wijzigingen toepast, is.
De paginagedeelten die gepersonaliseerde inhoud bevatten, kunnen vooraf worden verborgen door at.js te overschrijven `bodyHiddenStyle`.
Standaard `bodyHiddenStyle` verbergt de gehele HTML `body`.
U kunt beide instellingen overschrijven met `window.targetGlobalSettings`. `window.targetGlobalSettings` moet worden geplaatst voordat het bestand te.js wordt geladen.

### Web SDK gebruiken

Gebruikend Web SDK kan de klant opstelling hun pre-verbergende stijl in vormen bevel, zoals in het voorbeeld hieronder:

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Wanneer het laden van de asynchrone SDK van het Web adviseren wij dat het volgende fragment in de pagina wordt ingespoten alvorens het Web SDK wordt ingespoten:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Hoe wordt A4T verwerkt?

### At.js gebruiken

Er zijn 2 types van registreren A4T die het gebruiken at.js worden gesteund:

* Logboekregistratie aan clientzijde
* Logboekregistratie op de server voor Analytics

#### Logboekregistratie aan clientzijde

**Voorbeeld 1: Globale instelling van doel gebruiken**

Logboekregistratie aan de clientzijde van Analytics kan worden ingeschakeld door de instelling `analyticsLogging: client_side` in de instellingen at.js of door de `window.targetglobalSettings` object.
Als deze optie is ingesteld, ziet de indeling van de geretourneerde lading er als volgt uit:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

De payload kan vervolgens naar Analytics worden doorgestuurd via de API voor het invoegen van gegevens.

Voorbeeld 2: Het vormen in elke `getOffers` functie:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Zo ziet de antwoordlading eruit:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

De lading Analytics (`tnta` token) moet worden opgenomen in de hit Analytics [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Logboekregistratie op de server voor Analytics

Logboekregistratie aan de serverkant van Analytics kan worden ingeschakeld door het instellen van `analyticsLogging: server_side` in de instellingen at.js of door de `window.targetglobalSettings` object.
Vervolgens worden de gegevens als volgt gestroomd:

![](assets/a4t-server-side-atjs.png)

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=en)

### Web SDK gebruiken

Web SDK ondersteunt ook:

* Logboekregistratie aan clientzijde
* Logboekregistratie aan de zijde van Analytics Server

#### Logboekregistratie aan clientzijde

Logboekregistratie aan de clientzijde van Analytics wordt ingeschakeld wanneer Adobe Analytics is uitgeschakeld voor die DataStream-configuratie.

![](assets/analytics-disabled-datastream-config.png)

De klant heeft toegang tot het token Analytics (`tnta`) die met Analytics moet worden gedeeld met behulp van [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
door de `sendEvent` en doorloopt de resulterende array met voorstellingen.

**Voorbeeld**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Hier is een diagram om te tonen hoe de gegevensstromen wanneer de Kant van de Cliënt van Analytics wordt toegelaten:

![](assets/analytics-client-side-logging.png)

#### Logboekregistratie op de server voor Analytics

Logboekregistratie aan de serverkant van Analytics wordt ingeschakeld wanneer Analytics is ingeschakeld voor die DataStream-configuratie.

![](assets/analytics-enabled-datastream-config.png)

Wanneer de Logboekregistratie van de Analyse van de Server Zijdelings wordt toegelaten A4T nuttige lading die met Analytics moet worden gedeeld zodat de Analytics rapporteert correcte beelden tonen en de omzettingen op het niveau van de Rand van de Ervaring worden gedeeld, zodat de klant geen extra verwerking hoeft te doen.

Hieronder wordt beschreven hoe gegevens in onze systemen stromen wanneer de Logboekregistratie van de Analytics van de Server wordt toegelaten:

![](assets/analytics-server-side-logging.png)

## Globale instellingen doel instellen

### At.js gebruiken

U kunt instellingen in de bibliotheek at.js overschrijven met `window.targetGlobalSettings`, in plaats van de instellingen te configureren in de standaardinterface/Premium van het doel of met REST API&#39;s.

De overschrijving moet worden gedefinieerd voordat om.js wordt geladen of in Beheer > Implementatie > Bewerken op.js-instellingen > Codeinstellingen > Bibliotheekheader.

Voorbeeld:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)

### Web SDK gebruiken

Deze functie wordt niet ondersteund in Web SDK.

## De kenmerken van het doelprofiel bijwerken

### At.js gebruiken

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Web SDK gebruiken

Als u een doelprofiel wilt bijwerken, gebruikt u de opdracht `sendEvent` en stelt de `data.__adobe.target` eigenschap, sleutelnamen voorschrijven met `profile`.

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Hoe gebruik ik Target Recommendations

### At.js gebruiken

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.productName": "T-shirt",
     "entity.productId": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.productName": "T-shirt",
            "entity.productId": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=en)


### Web SDK gebruiken

Om de gegevens van de Aanbeveling te verzenden, gebruik `sendEvent` en stelt de `data.__adobe.target` eigenschap, sleutelnamen voorschrijven met `entity`.

**Voorbeeld**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.productName": "T-shirt",
        "entity.productId": "1234"
      }
    }
  }
});
```

## Hoe gebruik ik id&#39;s van derden

### At.js gebruiken

Het gebruiken van at.js is er veelvoudige manieren om te verzenden `mbox3rdPartyId`, gebruiken `getOffer` of `getOffers`:

**Voorbeeld 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Voorbeeld 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Of er is een manier om de `mbox3rdPartyId` ofwel in `targetPageParams` of `targetPageParamsAll`.
Wanneer u deze instelt `targetPageParams`, wordt het in de verzoeken om `target-global-mbox` ook bekend als `pag-lLoad`.
De aanbeveling moet worden vastgesteld met behulp van `targetPageParamsAll` aangezien het in elk doelverzoek zal worden verzonden.
Het voordeel van het gebruik `targetPageParamsAll` is dat u de `mbox3rdPartyId` eenmaal op de pagina staan, zodat alle doelaanvragen het juiste kunnen worden ingediend `mbox3rdPartyId`.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Meer informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=en)

### Web SDK gebruiken

Web SDK ondersteunt doel-id van derden. Er zijn echter nog een paar stappen voor nodig. Voordat we in de oplossing duiken, moeten we eerst wat praten over `identityMap`.
Met Identiteitskaart kunnen klanten meerdere identiteiten verzenden. Alle identiteiten worden naamruimte gegeven. Elke naamruimte kan een of meer identiteiten hebben. Een bepaalde identiteit kan als primair worden gemarkeerd.
Met deze kennis in mening kunnen wij zien wat de noodzakelijke stappen aan opstellings Web sdk zijn om identiteitskaart van de Derde van het Doel te gebruiken.

1. Opstelling namespace die identiteitskaart van de Derde van het Doel in de mening van de Configuratie van de Stroom van Gegevens zal bevatten:

![](assets/mbox-3-party-id-setup.png)

1. Verzend die identiteitsnaamruimte in elke sendEvent-opdracht als volgt:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Hoe kan ik eigenschapstokens instellen?

### At.js gebruiken

Gebruikend at.js zijn er twee manieren om opstelling de bezitstokens, of het gebruiken `targetPageParams` of `targetPageParamsAll`. Gebruiken `targetPageParams` voegt de eigenschap token toe aan de `target-global-mbox` vraag, maar het gebruiken `targetPageParamsAll` voegt het teken aan alle doelvraag toe:

**Voorbeeld 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Voorbeeld 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Web SDK gebruiken

Gebruikend Web SDK kunnen de klanten opstelling het bezit op een hoger niveau, wanneer vestiging de configuratie van de Stroom van Gegevens, onder Adobe Target namespace:
![](assets/at-property-setup.png)
Dit betekent elke vraag van het Doel voor die specifieke configuratie van de Stream van Gegevens die bezitstoken zal bevatten.

## Hoe kan ik een voorvoegsel toevoegen aan een box

### At.js gebruiken

Deze functionaliteit is alleen beschikbaar in at.js 2.x. at.js 2.x heeft een nieuwe functie genoemd `getOffers`. `getOffers` klanten toestaan inhoud vooraf in te stellen voor een of meer vakken. Hier volgt een voorbeeld:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

OPMERKING: Het wordt ten zeerste aanbevolen ervoor te zorgen dat `mbox` in de `mboxes` array heeft een eigen index. Meestal heeft de eerste box `index=0`, de volgende `index=1`, enz.

### Web SDK gebruiken

Deze functionaliteit wordt momenteel niet ondersteund in Web SDK.

## Hoe kan ik fouten opsporen in mijn doelimplementatie

### At.js gebruiken

At.js stelt deze het zuiveren eigenschappen bloot:

* Mbox Uitschakelen - schakel Doel uit van ophalen en renderen om te controleren of de pagina wordt verbroken zonder interactie van Doel
* Mbox Debug - at.js registreert elke actie
* Doelovertrek - met een mbox trace-token dat in Bullseye is gegenereerd, is een trace-object met details die aan het besluitvormingsproces hebben deelgenomen, beschikbaar onder `window.___target_trace` object

Opmerking: Al deze foutopsporingsfuncties zijn beschikbaar met verbeterde functies in [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Web SDK gebruiken

U hebt veelvoudige het zuiveren mogelijkheden wanneer het gebruiken van Web SDK:

* Gebruiken [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
* [Web SDK debugenabled](../../../edge/fundamentals/debugging.md)
* Gebruiken [Controle van webSDK-haken](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Gebruiken [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=en)
* Doelovertrek
