---
title: Clientregistratie voor A4T-gegevens in de Web SDK van het Platform
description: Leer hoe te om cliënt-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van het Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: doel;a4t;registreren;web sdk;ervaring;platform;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Clientregistratie voor A4T-gegevens in de Web SDK van het Platform

## Overzicht {#overview}

Met de Adobe Experience Platform Web SDK kunt u gegevens verzamelen [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) gegevens op de clientzijde van uw webtoepassing.

Logboekregistratie aan de clientzijde betekent dat [!DNL Target] gegevens worden geretourneerd aan de clientzijde, zodat u deze kunt verzamelen en delen met Analytics. Deze optie moet zijn ingeschakeld als u gegevens handmatig naar Analytics wilt verzenden met de opdracht [API voor gegevensinvoer](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Een methode om dit uit te voeren met [AppMeturement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) is momenteel in ontwikkeling en zal in de nabije toekomst beschikbaar zijn.

Dit document behandelt de stappen voor vestiging cliënt-kant het registreren A4T voor het Web SDK en verstrekt sommige implementatievoorbeelden voor gemeenschappelijke gebruiksgevallen.

## Vereisten {#prerequisites}

Dit leerprogramma veronderstelt dat u met de fundamentele concepten en processen vertrouwd bent met het gebruiken van SDK van het Web voor verpersoonlijkingsdoeleinden. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [De SDK van het Web configureren](../../../fundamentals/configuring-the-sdk.md)
* [Gebeurtenissen verzenden](../../../fundamentals/tracking-events.md)
* [Renderen van personalisatie-inhoud](../../rendering-personalization-content.md)

## Logboekregistratie op de client van Analytics instellen {#set-up-client-side-logging}

De volgende subsecties schetsen hoe te om cliënt-zijregistreren van Analytics voor uw implementatie van SDK van het Web toe te laten.

### Logboekregistratie op de client voor Analytics inschakelen {#enable-analytics-client-side-logging}

Als u wilt overwegen Analytics-logboekregistratie op de client voor uw implementatie is ingeschakeld, moet u de Adobe Analytics-configuratie in uw [datastream](../../../datastreams/overview.md).

![Configuratie van analysegegevensstroom uitgeschakeld](../assets/disable-analytics-datastream.png)

### Ophalen [!DNL A4T] gegevens van de SDK en deze naar Analytics verzenden {#a4t-to-analytics}

Deze rapportmethode werkt alleen correct als u de opdracht [!DNL A4T] verwante gegevens die zijn opgehaald uit de [`sendEvent`](../../../fundamentals/tracking-events.md) in de hit Analytics.

Wanneer Target Edge een reactie op proposities berekent, wordt gecontroleerd of Logboekregistratie aan de clientzijde van Analytics is ingeschakeld (bijvoorbeeld of Analytics is uitgeschakeld in uw gegevensstroom). Als het cliënt-zijregistreren wordt toegelaten, voegt het systeem een teken van Analytics aan elk voorstel in de reactie toe.

De stroom ziet er ongeveer als volgt uit:

![Logboekstroom aan de clientzijde](../assets/analytics-client-side-logging.png)

Hieronder ziet u een voorbeeld van een `interact` reactie wanneer Analytics client-side logboekregistratie is ingeschakeld. Als het voorstel betrekking heeft op een activiteit waarvoor Analytics-rapportage wordt uitgevoerd, heeft het een `scopeDetails.characteristics.analyticsToken` eigenschap.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Voorstellen voor Form-based Experience Composer-activiteiten kunnen zowel inhoud bevatten als metrische items klikken onder hetzelfde voorstel. Dus in plaats van één analysetoken voor weergave van inhoud in `scopeDetails.characteristics.analyticsToken` eigenschap, deze kunnen zowel een analysetoken voor weergave als een klik hebben die onder `scopeDetails.characteristics.analyticsTokens` object, in `display` en `click` eigendommen, overeenkomstig.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventTokens": {
                "display": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
                "click": "E0gb6q1+WyFW3FMbbQJmrg=="
              },
              "analyticsTokens": {
                "display": "434689:0:0|2,434689:0:0|1",
                "click": "434689:0:0|32767"
              }
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Alle waarden van `scopeDetails.characteristics.analyticsToken`, alsmede `scopeDetails.characteristics.analyticsTokens.display` (voor weergegeven inhoud) en `scopeDetails.characteristics.analyticsTokens.click` (voor klikmetriek) zijn de nuttige ladingen A4T die moeten worden verzameld en inbegrepen als `tnta` in de [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) vraag.

>[!IMPORTANT]
>
>Merk op dat sommige `analyticsToken`/`analyticsTokens` eigenschappen kunnen meerdere tokens bevatten, samengevoegd als één door komma&#39;s gescheiden tekenreeks.
>
>In de implementatievoorbeelden in de volgende sectie worden meerdere analytische tokens intern verzameld. Als u een array van analytische tokens wilt aaneenschakelen, gebruikt u een soortgelijke functie:
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Voorbeelden van implementaties {#implementation-examples}

De volgende subsecties tonen aan hoe te om cliënt-zijregistreren van Analytics voor gemeenschappelijke gebruiksgevallen uit te voeren.

### Formuliergebaseerde composeractiviteiten {#form-based-composer}

U kunt SDK van het Web gebruiken om de uitvoering van voorstellen van te controleren [Adobe Target Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) activiteiten.

Wanneer u om voorstellen voor een specifiek besluitwerkingsgebied verzoekt, bevat het teruggekeerde voorstel zijn aangewezen token Analytics. De beste praktijken moeten de SDK van het Web van het Platform ketenen `sendEvent` en doorloopt de geretourneerde voorstellingen om deze uit te voeren terwijl de tokens Analytics tegelijkertijd worden verzameld.

U kunt een `sendEvent` bevel voor een vorm-Gebaseerd de activiteitenwerkingsgebied van de Composer van de Ervaring als dit:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Van hier, moet u code uitvoeren om de voorstellen uit te voeren en een lading te construeren die uiteindelijk naar Analytics zal worden verzonden. Dit is een voorbeeld van wat `results.propositions` kan bevatten:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
        "eventTokens": {
          "display": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "click": "Tagb6q1+WyFW3FMbbQJrtg=="
        },
        "analyticsTokens": {
          "display": "434688:0:0|2,434688:0:0|1",
          "click": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Als u het token Analytics uit een voorstel met inhoudsitems wilt extraheren, kunt u een functie implementeren die lijkt op het volgende:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.display;
  }
  return characteristics.analyticsToken;
}
```

Een voorstel kan verschillende typen punten hebben, zoals die door `schema` eigendom van het betrokken artikel. Er zijn vier schema&#39;s van het projectitems die voor op vorm-gebaseerde activiteiten van de Composer van de Ervaring worden gesteund:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` en `JSON_SCHEMA` zijn de schema&#39;s die het soort aanbieding weerspiegelen, terwijl `MEASUREMENT_SCHEMA` wijst op de metriek die aan een element DOM zou moeten worden vastgemaakt.

Analyseladingen voor klikmetriek zouden afzonderlijk van inhoudspunten moeten worden verzameld en worden verzonden naar Analytics, op het ogenblik dat de bezoeker eigenlijk op de eerder getoonde inhoud klikt.

De volgende hulpfunctie voor het krijgen van de klik metrische A4T nuttige lasten zal in dit geval in handvat komen:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.click;
  }
  return characteristics.analyticsToken;
}
```

#### Overzicht van implementatie {#implementation-summary}

Samengevat, moeten de volgende stappen worden uitgevoerd wanneer het toepassen van de Form-Based activiteiten van de Composer van de Ervaring met het Web SDK van het Platform:

1. Verzend een gebeurtenis die op vorm-Gebaseerde de activiteitenvoorstellen van de Composer van de Ervaring haalt;
1. Pas de inhoudswijzigingen toe op de pagina;
1. Verzend de `decisioning.propositionDisplay` meldingsgebeurtenis;
1. Verzamel de analytische vertoningstokens van de reactie van SDK en construeer een lading voor de treffer Analytics;
1. Verstuur de lading naar Analytics gebruikend [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Als er klikmetriek in geleverde voorstellingen zijn, zouden de klikluisteraars opstelling moeten zijn zodat wanneer een klik wordt uitgevoerd, het verzendt `decisioning.propositionInteract` notification-gebeurtenis. De `onBeforeEventSend` de manager zou moeten worden gevormd zodat wanneer het onderscheppen `decisioning.propositionInteract` De volgende acties worden uitgevoerd:
   1. De click Analytics-tokens verzamelen van `xdm._experience.decisioning.propositions`
   1. De click Analytics verzenden die met de verzamelde Analytics-payload via [API voor gegevensinvoer](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Visual Experience Composer-activiteiten {#visual-experience-composer-acitivties}

De SDK van het Web staat u toe om aanbiedingen te behandelen die werden authoring gebruikend [Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>De stappen voor de implementatie van dit gebruiksgeval lijken sterk op de stappen voor [Formuliergebaseerde composeractiviteiten](#form-based-composer). Lees de vorige sectie voor meer informatie.

Wanneer automatische rendering is ingeschakeld, kunt u de tokens Analytics verzamelen van de voorstellingen die op de pagina zijn uitgevoerd. De beste praktijken moeten de SDK van het Web van het Platform ketenen `sendEvent` bevel en herhaling door de teruggekeerde voorstellingen om die te filtreren die SDK van het Web heeft geprobeerd terug te geven.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Gebruiken `onBeforeEventSend` om de afmetingen van pagina&#39;s af te handelen {#using-onbeforeeventsend}

Met Adobe Target-activiteiten kunt u verschillende metriek instellen op de pagina, handmatig gekoppeld aan het DOM of automatisch gekoppeld aan het DOM (VEC authored Activities). Beide typen vormen een vertraagde interactie van de eindgebruiker op de webpagina.

Om dit te verantwoorden, is de beste praktijk om de ladingen van de Analyse te verzamelen gebruikend `onBeforeEventSend` Adobe Experience Platform Web SDK-haak. De `onBeforeEventSend` haak zou moeten worden gevormd gebruikend `configure` en wordt weerspiegeld in alle gebeurtenissen die via de gegevensstroom worden verzonden.

Hieronder ziet u hoe `onBeforeEventSent` kan worden geconfigureerd om Analytics-hits te activeren:

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Volgende stappen {#next-steps}

Deze gids behandelde cliënt-zijregistreren voor A4T gegevens in het Web SDK. Zie de handleiding op [logboekregistratie op de server](server-side.md) voor meer informatie over hoe te om A4T gegevens over het Netwerk van de Rand te behandelen.
