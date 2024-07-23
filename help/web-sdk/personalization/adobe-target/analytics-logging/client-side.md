---
title: Logboekregistratie aan de clientzijde voor A4T-gegevens in de Platform Web SDK
description: Leer hoe te om cliënt-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van het Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: doel;a4t;registreren;web sdk;ervaring;platform;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Logboekregistratie aan de clientzijde voor A4T-gegevens in de Platform Web SDK

## Overzicht {#overview}

SDK van het Web van Adobe Experience Platform staat u toe om [ Adobe Analytics voor Doel (A4T) ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) gegevens over de cliëntkant van uw Webtoepassing te verzamelen.

Logboekregistratie aan de clientzijde betekent dat relevante [!DNL Target] gegevens worden geretourneerd aan de clientzijde, zodat u deze kunt verzamelen en delen met Analytics. Deze optie zou moeten worden toegelaten als u van plan bent gegevens aan Analytics manueel te verzenden gebruikend de [ Invoeging API van Gegevens ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Een methode om dit uit te voeren gebruikend [ AppMeasurement.js ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) is momenteel in ontwikkeling en zal in de nabije toekomst beschikbaar zijn.

Dit document behandelt de stappen voor vestiging cliënt-kant het registreren A4T voor het Web SDK en verstrekt sommige implementatievoorbeelden voor gemeenschappelijke gebruiksgevallen.

## Vereisten {#prerequisites}

Dit leerprogramma veronderstelt dat u met de fundamentele concepten en processen vertrouwd bent met het gebruiken van SDK van het Web voor verpersoonlijkingsdoeleinden. Raadpleeg de volgende documentatie als u een inleiding nodig hebt:

* [De SDK van het Web configureren](/help/web-sdk/commands/configure/overview.md)
* [Gebeurtenissen verzenden](/help/web-sdk/commands/sendevent/overview.md)
* [Renderen van personalisatie-inhoud](../../rendering-personalization-content.md)

## Logboekregistratie op de client van Analytics instellen {#set-up-client-side-logging}

De volgende subsecties schetsen hoe te om cliënt-zijregistreren van Analytics voor uw implementatie van SDK van het Web toe te laten.

### Logboekregistratie op de client voor Analytics inschakelen {#enable-analytics-client-side-logging}

Om Analytics cliënt-zijregistreren te overwegen die voor uw implementatie wordt toegelaten, moet u de configuratie van Adobe Analytics in uw [ datastream ](../../../../datastreams/overview.md) onbruikbaar maken.

![ de configuratie van de Analyse gegevensstroom gehandicapte ](../assets/disable-analytics-datastream.png)

### Haal [!DNL A4T] -gegevens op van de SDK en verzend deze naar Analytics {#a4t-to-analytics}

Deze rapportmethode werkt alleen correct als u de [!DNL A4T] -gerelateerde gegevens verzendt die zijn opgehaald via de opdracht [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) in de hit Analytics.

Wanneer Target Edge een reactie op proposities berekent, wordt gecontroleerd of Logboekregistratie aan de clientzijde van Analytics is ingeschakeld (bijvoorbeeld of Analytics is uitgeschakeld in uw gegevensstroom). Als het cliënt-zijregistreren wordt toegelaten, voegt het systeem een teken van Analytics aan elk voorstel in de reactie toe.

De stroom ziet er ongeveer als volgt uit:

![ cliënt-kant registrerenstroom ](../assets/analytics-client-side-logging.png)

Hieronder ziet u een voorbeeld van een `interact` -reactie als Logboekregistratie op de client van Analytics is ingeschakeld. Als het voorstel voor een activiteit is waarvoor Analytics-rapportage wordt gebruikt, heeft het de eigenschap `scopeDetails.characteristics.analyticsToken` .

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

Voorstellen voor Form-based Experience Composer-activiteiten kunnen zowel inhoud bevatten als metrische items klikken onder hetzelfde voorstel. In plaats van één analysetoken voor inhoudsweergave in de eigenschap `scopeDetails.characteristics.analyticsToken` , kunnen er dus zowel een display- als een click-analysetoken worden opgegeven in de eigenschappen `scopeDetails.characteristics.analyticsDisplayToken` en `scopeDetails.characteristics.analyticsClickToken` .

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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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

Alle waarden van `scopeDetails.characteristics.analyticsToken`, evenals `scopeDetails.characteristics.analyticsDisplayToken` (voor getoonde inhoud) en `scopeDetails.characteristics.analyticsClickToken` (voor klikmetriek) zijn de nuttige ladingen A4T die moeten worden verzameld en als `tnta` markering in de [ API van de Invoeging van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) vraag worden omvat.

>[!IMPORTANT]
>
>De eigenschappen `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` kunnen meerdere tokens bevatten, samengevoegd als één door komma&#39;s gescheiden tekenreeks.
>
>In de implementatievoorbeelden in de volgende sectie worden meerdere analytische tokens intern verzameld. Als u een array van analytische tokens wilt aaneenschakelen, gebruikt u een soortgelijke functie:
>
>```javascript
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

U kunt SDK van het Web gebruiken om de uitvoering van voorstellen van [ op vorm-Gebaseerde Composer van de Ervaring van Adobe Target te controleren ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) activiteiten.

Wanneer u om voorstellen voor een specifiek besluitwerkingsgebied verzoekt, bevat het teruggekeerde voorstel zijn aangewezen token Analytics. De beste praktijken moeten het bevel van SDK van het Web van het Platform `sendEvent` ketenen en door de teruggekeerde voorstellen herhalen om hen uit te voeren terwijl het verzamelen van de tokens van de Analytics tezelfdertijd.

U kunt een opdracht `sendEvent` activeren voor een werkgebied van Composer-activiteiten op basis van een formulier, zoals:

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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
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
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Een voorstel kan verschillende soorten punten hebben, zoals die door het `schema` bezit van het punt in kwestie worden vermeld. Er zijn vier schema&#39;s van het projectitems die voor op vorm-gebaseerde activiteiten van de Composer van de Ervaring worden gesteund:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` en `JSON_SCHEMA` zijn de schema&#39;s die het type van de aanbieding weerspiegelen, terwijl `MEASUREMENT_SCHEMA` de metriek weerspiegelt die aan een DOM element zou moeten worden vastgemaakt.

Analyseladingen voor klikmetriek zouden afzonderlijk van inhoudspunten moeten worden verzameld en worden verzonden naar Analytics, op het ogenblik dat de bezoeker eigenlijk op de eerder getoonde inhoud klikt.

De volgende hulpfunctie voor het krijgen van de klik metrische A4T nuttige lasten zal in dit geval in handvat komen:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Overzicht van implementatie {#implementation-summary}

Samengevat, moeten de volgende stappen worden uitgevoerd wanneer het toepassen van de Form-Based Composer van de Ervaring activiteiten met het Web SDK van het Platform:

1. Verzend een gebeurtenis die op vorm-Gebaseerde de activiteitenvoorstellen van de Composer van de Ervaring haalt;
1. Pas de inhoudswijzigingen toe op de pagina;
1. Verzend de `decisioning.propositionDisplay` notification-gebeurtenis;
1. Verzamel de analytische vertoningstokens van de reactie van SDK en construeer een lading voor de treffer Analytics;
1. Verzend de nuttige lading naar Analytics gebruikend de [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Als er klikmetriek in geleverde voorstellen zijn, zouden de klikluisteraars opstelling moeten zijn zodat wanneer een klik wordt uitgevoerd, het de `decisioning.propositionInteract` berichtgebeurtenis verzendt. De `onBeforeEventSend` -handler moet zo worden geconfigureerd dat bij het onderscheppen van `decisioning.propositionInteract` -gebeurtenissen de volgende handelingen plaatsvinden:
   1. De click Analytics-tokens verzamelen uit `xdm._experience.decisioning.propositions`
   1. Verzenden van de klikAnalytics met de verzamelde nuttige lading van Analytics via [ Invoeging API van Gegevens ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

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

SDK van het Web staat u toe om aanbiedingen te behandelen die gebruikend [ Visual Experience Composer (VEC) ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) werden authored.

>[!NOTE]
>
>De stappen voor het uitvoeren van dit gebruiksgeval zijn zeer gelijkaardig aan de stappen voor [ op vorm-Gebaseerde activiteiten van de Composer van de Ervaring ](#form-based-composer). Lees de vorige sectie voor meer informatie.

Wanneer automatische rendering is ingeschakeld, kunt u de tokens Analytics verzamelen van de voorstellingen die op de pagina zijn uitgevoerd. De beste praktijken moeten het bevel van SDK van het Web van het Platform `sendEvent` ketenen en door de teruggekeerde voorstellen herhalen om die te filtreren die SDK van het Web heeft geprobeerd terug te geven.

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

### Werken met `onBeforeEventSend` voor het verwerken van paginageometrische gegevens {#using-onbeforeeventsend}

Met Adobe Target-activiteiten kunt u verschillende metriek instellen op de pagina, handmatig gekoppeld aan het DOM of automatisch gekoppeld aan het DOM (VEC authored Activities). Beide typen vormen een vertraagde interactie van de eindgebruiker op de webpagina.

Hiervoor kunt u het beste analytische ladingen verzamelen met de `onBeforeEventSend` Adobe Experience Platform Web SDK-haak. De `onBeforeEventSend` haak moet worden geconfigureerd met de opdracht `configure` en wordt weerspiegeld in alle gebeurtenissen die door de gegevensstroom worden verzonden.

Hieronder ziet u hoe `onBeforeEventSent` kan worden geconfigureerd om analyses uit te lokken:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
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

Deze gids behandelde cliënt-zijregistreren voor A4T gegevens in het Web SDK. Zie de gids op [ server-zijregistreren ](server-side.md) voor meer informatie over hoe te om A4T gegevens over de Edge Network te behandelen.
