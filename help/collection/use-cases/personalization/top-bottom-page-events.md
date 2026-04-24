---
title: Vorm bovenkant en bodem van paginagebeurtenissen in SDK van het Web
description: In dit artikel wordt uitgelegd hoe boven- en onderaan-pagina-gebeurtenissen in Web SDK kunnen worden gebruikt.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---


# Vorm bovenkant en bodem van paginagebeurtenissen in SDK van het Web

Wanneer u persoonlijke ervaringen opdoet, is de laadtijd van een webpagina essentieel. Om de tijd te minimaliseren een gebruiker op gepersonaliseerde inhoud wacht, steunt SDK van het Web de configuratie van bovenkant en bodem van paginagebeurtenissen.

Boven en onder aan paginagebeurtenissen vindt u een methode voor het asynchroon laden van verschillende elementen op de pagina, terwijl de laadtijd van de pagina minimaal blijft:

* De gebeurtenis boven aan de pagina vraagt om personalisatie zodra de pagina begint te laden.
* De onderkant van de paginagebeurtenis neemt een paginaweergave op wanneer de pagina klaar is met laden.

Adobe Analytics negeert de bovenkant van paginagebeurtenissen, wat tot nauwkeurigere metriek opname leidt aangezien slechts één paginareactie wordt geregistreerd (de bodem van paginagebeurtenis).

U kunt boven- en onderzijde van paginagebeurtenissen op twee manieren configureren: door de SDK JavaScript-bibliotheek van het Web (`alloy()`) rechtstreeks aan te roepen of door de extensie van de SDK-tag Web te gebruiken in de UI Tags voor Adobe Experience Platform. De actie van de markeringsuitbreiding [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) omvat een &quot;[!UICONTROL Use guided events]&quot;optie die pre-vormt gebiedswaarden voor ([!UICONTROL Request personalization]&#39; (bovenkant van pagina) en ([!UICONTROL Collect analytics]&#39; (bodem van pagina) scenario&#39;s. In elk van de onderstaande voorbeelden worden beide implementaties getoond.

## De gebeurtenis Boven aan pagina {#top-of-page}

Het voorbeeld hieronder vormt een bovenkant van paginagebeurtenis die om verpersoonlijking verzoekt maar [&#x200B; vertoningsgebeurtenissen &#x200B;](display-events.md) voor automatisch teruggegeven voorstellingen onderdrukt. Deze weergavegebeurtenissen worden verzonden met de onderzijde van de paginagebeurtenis.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parameter | Vereist/optioneel | Beschrijving |
| --- | --- | --- |
| `type` | Vereist | Stel deze parameter in op `decisioning.propositionFetch` . Dit speciale gebeurtenistype instrueert Adobe Analytics deze gebeurtenis te laten vallen. Wanneer u Customer Journey Analytics gebruikt, kunt u ook een filter instellen om deze gebeurtenissen te neerzetten. Zie [&#x200B; de gebeurtenistypen van Edge Network in Adobe Analytics &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types) voor meer informatie. |
| `renderDecisions` | Vereist | Stel deze parameter in op `true` . Deze parameter vertelt Web SDK om besluiten terug te geven die door Edge Network zijn teruggekeerd. |
| `personalization.sendDisplayEvent` | Vereist | Stel deze parameter in op `false` . Met deze parameter wordt gestopt met het verzenden van weergavegebeurtenissen. |

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

Configureer een [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) -actie in de regel die boven aan de pagina wordt geactiveerd. Schakel **[!UICONTROL Use guided events]** in en selecteer vervolgens **[!UICONTROL Request personalization]** . Deze optie sluit &#39;[!UICONTROL Type]&#39; aan &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;, &#39;[!UICONTROL Render visual personalization decisions]&#39; aan toegelaten, en &#39;[!UICONTROL Automatically send a display event]&#39; aan gehandicapten.

Als u deze velden handmatig wilt instellen, laat u **[!UICONTROL Use guided events]** uitgeschakeld en configureert u elk veld zelf.

>[!ENDTABS]

## Voorbeelden van gebeurtenissen onder aan pagina {#bottom-of-page}

### Automatisch gerenderde voorstellingen {#bottom-auto-rendered}

Het voorbeeld hieronder vormt een bodem van paginagebeurtenis die vertoningsgebeurtenissen voor voorstellen verzendt die automatisch op de pagina werden teruggegeven maar in de [&#x200B; bovenkant van pagina &#x200B;](#top-of-page) gebeurtenis onderdrukt.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Vereist/optioneel | Beschrijving |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Vereist | Stel deze parameter in op `true` . Deze parameter laat het verzenden van vertoningsgebeurtenissen toe die in de bovenkant van paginagebeurtenis werden onderdrukt. |
| `xdm` | Optioneel | Gebruik dit object om alle gegevens op te nemen die u onder aan de paginagebeurtenis wilt weergeven. |

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

Configureer een [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) -actie in de regel die onder aan de pagina wordt geactiveerd. Schakel **[!UICONTROL Use guided events]** in en selecteer vervolgens **[!UICONTROL Collect analytics]** . Deze optie sluit &#39;[!UICONTROL Include rendered propositions]&#39; aan toegelaten.

Als u dit veld handmatig wilt instellen, laat u **[!UICONTROL Use guided events]** uitgeschakeld en schakelt u **[!UICONTROL Include rendered propositions]** rechtstreeks in. Naar keuze, bevolk het **[!UICONTROL XDM]** gebied met een [&#x200B; XDM voorwerp &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) gegevenselement dat uw paginagegevens draagt.

>[!ENDTABS]

### Handmatig gerenderde voorstellingen {#bottom-manually-rendered}

In het onderstaande voorbeeld wordt een onderkant van een paginagebeurtenis geconfigureerd die weergavegebeurtenissen verzendt voor voorstellen die handmatig op de pagina zijn weergegeven (dat wil zeggen voor aangepaste beslissingsbereiken of oppervlakken).

>[!NOTE]
>
>In dit scenario moet de onderkant van de paginagebeurtenis wachten tot de gebeurtenis top van de pagina is voltooid, zodat de voorstellen kunnen worden weergegeven en opgenomen.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

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

| Parameter | Vereist/optioneel | Beschrijving |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Vereist | Deze sectie bepaalt manueel teruggegeven voorstellingen. U moet de voorstelling `id` , `scope` en `scopeDetails` opnemen. Zie [&#x200B; vertoningsgebeurtenissen &#x200B;](display-events.md) voor meer informatie beheren. Handmatig gerenderde verpersoonlijkingsinhoud moet onder aan de paginagebeurtenis worden opgenomen. |
| `xdm._experience.decisioning.propositionEventType` | Vereist | Stel deze parameter in op `display: 1` . |
| `xdm` | Optioneel | Gebruik dit object om alle gegevens op te nemen die u onder aan de paginagebeurtenis wilt weergeven. |

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

De optie &#39;[!UICONTROL Use guided events]&#39; behandelt dit scenario niet, zodat vormt manueel de actie:

1. Creeer een [&#x200B; voorwerp XDM &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (of [&#x200B; Variabele &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)) gegevenselement dat `_experience.decisioning.propositions` met elk teruggegeven voorstel `id` bevolkt, `scope`, en `scopeDetails`, en plaatst `_experience.decisioning.propositionEventType.display` aan `1`. Zie [&#x200B; vertoningsgebeurtenissen &#x200B;](display-events.md) voor meer informatie beheren.
1. Laat in de handeling [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) voor de onderzijde van de paginalijn **[!UICONTROL Use guided events]** uitgeschakeld en verwijs naar het gegevenselement in het veld **[!UICONTROL XDM]** .

>[!ENDTABS]

## Toepassing van één pagina met boven- en onderzijde van paginagebeurtenissen {#spa-example}

In een toepassing van één pagina, moet u de meningsnaam op elke meningsverandering specificeren zodat het Web SDK de correcte verpersoonlijking bij de bovenkant van de pagina teruggeeft en de correcte mening bij de bodem van de pagina registreert.

### Weergave eerste pagina {#spa-first-view}

In dit voorbeeld is `home` de weergave die wordt geladen op de eerste pagina die wordt geladen.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

De hoogste vraag vraagt verpersoonlijking voor de `home` mening zonder een Analytics te registreren of vertoningsgebeurtenissen te ontslaan. In de onderste aanroep wordt de paginaweergave vastgelegd en worden de onderdrukte weergavegebeurtenissen geactiveerd. Neem dezelfde `viewName` op in beide aanroepen, zodat de weergave consistent wordt opgenomen.

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

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

1. Creeer een [&#x200B; XDM voorwerp &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) gegevenselement dat `web.webPageDetails.viewName` aan de naam van de mening (bijvoorbeeld, `home`) plaatst.
1. Vorm een bovenkant van pagina [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) actie: laat **[!UICONTROL Use guided events]** toe, selecteer **[!UICONTROL Request personalization]**, en verwijs het gegevenselement in het **[!UICONTROL XDM]** gebied.
1. Vorm een bodem van pagina **[!UICONTROL Send event]** actie: laat **[!UICONTROL Use guided events]** toe, selecteer **[!UICONTROL Collect analytics]**, en verwijs het zelfde gegevenselement in het **[!UICONTROL XDM]** gebied zodat `viewName` in beide gebeurtenissen aanpast.

>[!ENDTABS]

### Weergave tweede pagina — optie 1 {#spa-second-view-option-1}

In dit voorbeeld is één gebeurtenis voldoende omdat de personalisatie voor de pagina al is opgehaald.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

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

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

1. Creeer een [&#x200B; XDM voorwerp &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) gegevenselement dat `web.webPageDetails.viewName` aan de naam van de nieuwe mening (bijvoorbeeld, `cart`) plaatst.
1. Configureer bij de wijziging van de weergave één [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) -actie: laat **[!UICONTROL Use guided events]** uitgeschakeld, schakel **[!UICONTROL Render visual personalization decisions]** in en verwijs naar het gegevenselement in het **[!UICONTROL XDM]** -veld.

>[!ENDTABS]

### Weergave tweede pagina — optie 2 {#spa-second-view-option-2}

Gebruik deze aanpak wanneer u de onderkant van een paginagebeurtenis moet vertragen (bijvoorbeeld wanneer de analysegegevens van de pagina niet gereed zijn op het moment dat de weergave wordt gewijzigd). Verwerk de wijziging van de weergave in twee stappen:

1. Geef boven aan de pagina de al opgehaalde voorstellen weer zonder een Edge Network-aanroep te maken.
1. Als de analysegegevens gereed zijn, verzendt u de onderkant van de paginagebeurtenis.

Neem dezelfde `viewName` op in beide aanroepen, zodat de weergave consistent wordt opgenomen.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

Roep [`applyPropositions`](/help/collection/js/commands/applypropositions.md) boven aan de pagina aan om de in de cache opgeslagen voorstellingen voor de nieuwe weergave weer te geven. Roep vervolgens `sendEvent` onder aan de pagina aan met `includeRenderedPropositions: true` , zodat de onderdrukte weergavegebeurtenissen worden geactiveerd.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

1. Creeer een [&#x200B; XDM voorwerp &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) gegevenselement dat `web.webPageDetails.viewName` aan de naam van de nieuwe mening (bijvoorbeeld, `cart`) plaatst.
1. Voor de bovenkant van de paginagebeurtenis configureert u een [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) -actie en stelt u het **[!UICONTROL View name]** -veld in op de naam van de weergave (bijvoorbeeld `cart` ). Met deze handeling worden de al opgehaalde voorstellen weergegeven zonder contact op te nemen met de Edge Network.
1. Voor de onderzijde van de paginagebeurtenis configureert u een [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) -actie: enable **[!UICONTROL Use guided events]** , select **[!UICONTROL Collect analytics]** en reference the data element in the **[!UICONTROL XDM]** field.

>[!ENDTABS]

## GitHub-voorbeeld {#github-sample}

Het [&#x200B; top-en-ondersteekproef in de legy-samples bewaarplaats &#x200B;](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) toont aan hoe te om verpersoonlijking bij de bovenkant van de pagina te verzoeken en analysegegevens bij de bodem te verzenden. Download het voorbeeld en voer het lokaal uit om te zien hoe de boven- en onderkant van paginagebeurtenissen werken. Het voorbeeld gebruikt rechtstreeks de JavaScript-bibliotheek; dezelfde patronen worden toegepast wanneer u equivalente regels configureert in de Web SDK-tagextensie.
