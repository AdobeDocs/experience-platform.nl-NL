---
title: Vorm bovenkant en bodem van paginagebeurtenissen in Web SDK
description: Dit artikel verklaart hoe te om bovenkant en bodem van paginagebeurtenissen in Web SDK te gebruiken.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 4d0895c6ad38523f5527c9630931c3c0b8ef83c0
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Vorm bovenkant en bodem van paginagebeurtenissen in Web SDK

Wanneer u uw klanten persoonlijke ervaringen wilt bieden, is de laadtijd van een webpagina van essentieel belang.

Om de ladingstijden te optimaliseren en verpersoonlijking zo snel mogelijk te leveren, steunt SDK van het Web de configuratie van bovenkant en bodem van paginagebeurtenissen.

Boven en onder aan paginagebeurtenissen wordt een methode beschreven voor het asynchroon laden van verschillende elementen op de pagina, terwijl de laadtijd van de pagina tot een minimum wordt beperkt.

Deze configuratie minimaliseert de hoeveelheid tijd een gebruiker moet wachten tot de gepersonaliseerde inhoud wordt geladen.

Wat de meetnauwkeurigheid betreft, kan Adobe Analytics gebeurtenissen boven aan de pagina negeren. Dit leidt tot nauwkeurigere meetgegevens, aangezien slechts één paginakit wordt opgenomen (de onderkant van de paginagebeurtenis).

## Gebruiksscenario’s {#use-cases}

Een detailhandelaar in sportkleding wil hun klanten persoonlijke ervaringen bieden, terwijl de wrijving van de gebruiker bij het bezoeken van hun website tot een minimum wordt beperkt, terwijl hij tegelijkertijd de meetgegevens van de bezoeker nauwkeurig kan verzamelen.

Door bovenkant en bodem van paginagebeurtenissen in Web SDK te gebruiken, kan het marketing team hun verpersoonlijkingslevering op de meest optimale manier vormen:

* Web SDK verzendt een verpersoonlijkingsverzoek dat wordt geladen zodra de pagina begint te laden. Dit is een top van page-gebeurtenis.
* Wanneer de pagina klaar is met laden, wordt een gebeurtenis in de paginaweergave opgenomen. Dit gebeurt later tijdens het laden van de pagina. Dit is een onderkant van een paginagebeurtenis.

## Boven aan pagina, gebeurtenisvoorbeeld {#top-of-page}

De codesteekproef hieronder illustreert een bovenkant van de configuratie van de paginagebeurtenis die om verpersoonlijking verzoekt maar niet [ vertoningsgebeurtenissen ](../personalization/display-events.md#send-sendEvent-calls) voor automatisch teruggegeven voorstellingen verzendt. De [ vertoningsgebeurtenissen ](../personalization/display-events.md#send-sendEvent-calls) zullen als deel van de bodem-van-pagina gebeurtenis worden verzonden.

>[!BEGINTABS]

>[!TAB  Boven aan paginagebeurtenis ]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Paramter | Vereist/optioneel | Beschrijving |
|---|---|---|
| `type` | Vereist | Stel deze parameter in op `decisioning.propositionFetch` . Dit speciale gebeurtenistype instrueert Adobe Analytics deze gebeurtenis te laten vallen. Wanneer u Customer Journey Analytics gebruikt, kunt u ook een filter instellen om deze gebeurtenissen neer te zetten. |
| `renderDecisions` | Vereist | Stel deze parameter in op `true` . Deze parameter vertelt Web SDK om besluiten terug te geven die door de Edge Network zijn teruggekeerd. |
| `personalization.sendDisplayEvent` | Vereist | Stel deze parameter in op `false` . Hiermee voorkomt u dat weergavegebeurtenissen worden verzonden. |

>[!ENDTABS]

## Voorbeelden van gebeurtenissen onder aan pagina {#bottom-of-page}

>[!BEGINTABS]

>[!TAB  Auto-teruggegeven voorstellingen ]

De codesteekproef hieronder illustreert een bodem van de configuratie van de paginagebeurtenis die vertoningsgebeurtenissen voor voorstellingen verzendt die automatisch op de pagina werden teruggegeven maar waarvoor de vertoningsgebeurtenissen in [ bovenkant van pagina ](#top-of-page) gebeurtenis werden onderdrukt.

>[!NOTE]
>
>In dit scenario, moet u de bodem van paginagebeurtenis _na_ de bovenkant van pagina één roepen. De onderzijde van de gebeurtenis page hoeft echter niet te wachten tot de bovenzijde van pagina één is voltooid.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Vereist/optioneel | Beschrijving |
|---|---|---|
| `personalization.includeRenderedPropositions` | Vereist | Stel deze parameter in op `true` . Hierdoor kunnen weergavegebeurtenissen worden verzonden die boven aan de paginagebeurtenis zijn onderdrukt. |
| `xdm` | Optioneel | Gebruik deze sectie om alle gegevens op te nemen die u onder aan de paginagebeurtenis nodig hebt. |

>[!TAB  manueel teruggegeven voorstellingen ]

In het onderstaande codevoorbeeld ziet u een onderkant van de configuratie van een paginagebeurtenis die weergavegebeurtenissen verzendt voor voorstellen die handmatig op de pagina zijn weergegeven (bijvoorbeeld voor aangepaste beslissingsbereiken of oppervlakken).

>[!NOTE]
>
>In dit scenario moet de onderkant van de paginagebeurtenis wachten tot de gebeurtenis boven aan de pagina is voltooid. Zo kunt u de voorstellen renderen en de onderkant van de paginagebeurtenis opnemen.

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| Paramter | Vereist/optioneel | Beschrijving |
|---|---|---|
| `xdm._experience.decisioning.propositions` | Vereist | Deze sectie bepaalt manueel teruggegeven voorstellingen. U moet de voorstelling `ID` , `scope` en `scopeDetails` opnemen. Zie de documentatie op hoe te [ verpersoonlijking ](../personalization/rendering-personalization-content.md#manually) voor meer informatie manueel teruggeven over hoe te om vertoningsgebeurtenissen voor manueel teruggegeven inhoud te registreren. Handmatig gerenderde verpersoonlijkingsinhoud moet onder aan de paginaklok worden opgenomen. |
| `xdm._experience.decisioning.propositionEventType` | Vereist | Stel deze parameter in op `display: 1` . |
| `xdm` | Optioneel | Gebruik deze sectie om alle gegevens op te nemen die u onder aan de paginagebeurtenis nodig hebt. |

>[!ENDTABS]


## Toepassing van één pagina met bovenkant en onderste paginakijken {#spa-example}


>[!BEGINTABS]

>[!TAB  Eerste paginamening ]

In het onderstaande voorbeeld wordt de parameter `xdm.web.webPageDetails.viewName` toegevoegd. Dit is wat het tot één-paginatoepassing maakt. De `viewName` in dit voorbeeld is de weergave die wordt geladen op de pagina die wordt geladen.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB  Tweede paginamening (Optie 1) ]

In dit voorbeeld is het niet nodig om boven/onder pagina te splitsen, omdat de personalisatie voor de pagina al is opgehaald.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB  Tweede paginamening (Optie 2) ]

Als u nog steeds de onderkant van een paginaklok moet vertragen, kunt u `applyPropositions` gebruiken voor de bovenkant van een paginaklok. Aangezien geen verpersoonlijking moet worden opgehaald en geen Analytische gegevens moeten worden geregistreerd, is het niet nodig om een verzoek aan de Edge Network te richten.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

## GitHub-voorbeeld {#github-sample}

De steekproef die bij [ wordt gevonden dit adres ](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) toont aan hoe te om Experience Platform en Web SDK te gebruiken om verpersoonlijking bij de bovenkant van de pagina te verzoeken, en analysemetriek bij de bodem te verzenden. U kunt het voorbeeld downloaden en lokaal uitvoeren om te begrijpen hoe boven- en onderaan pagina-gebeurtenissen werken.
