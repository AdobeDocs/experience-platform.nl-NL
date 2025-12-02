---
title: autoCollectPropositionInteractions
description: Automatisch gegevens verzamelen wanneer op een koppeling wordt geklikt.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

De eigenschap `autoCollectPropositionInteractions` is een optionele instelling die bepaalt of de Web SDK automatisch propositieinteracties verzamelt. De waarde is een kaart van besluitvormingsleveranciers, elk met waarde die erop wijst hoe de automatische voorstellingsinteractie zou moeten worden behandeld.

Wanneer u automatische het volgen van propositieinteractie toelaat, worden om het even welke kliks binnen een proposition element dat aan DOM wordt teruggegeven automatisch verzameld door het Web SDK. Deze verzameling bevat alle ervaringen die automatisch door de Web SDK aan de DOM worden gerenderd en ervaringen die met de opdracht [`applyPropositions`](../applypropositions.md) aan de DOM zijn gerenderd.

Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `{"AJO": "always", "TGT": "never"}` gebruikt. Als u propositieinteracties liever niet automatisch wilt bijhouden, stelt u de waarde in op `{"AJO": "never", "TGT": "never"}` .

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Tot de ondersteunde eigenschappen in dit object behoren:

| Eigenschap | Beschrijving |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Mogelijke waarden voor elke eigenschap zijn:

| Waarde | Beschrijving |
| --- | --- |
| **`always`** | Verzamel altijd automatisch `interact` -gebeurtenissen voor alle elementen die aan een voorstel zijn gekoppeld. |
| **`never`** | Verzamel nooit automatisch `interact` -gebeurtenissen voor elementen die aan een voorstel zijn gekoppeld. |
| **`decoratedElementsOnly`** | Verzamel automatisch `interact` -gebeurtenissen voor elementen die aan een voorstel zijn gekoppeld als het element gegevenskenmerken bevat die een label of token opgeven. |

## Gegevenskenmerken {#data-attributes}

U kunt gegevenskenmerken op elementen gebruiken om specificiteit aan een interactie toe te voegen.

| Naam | Gegevenskenmerk | Beschrijving |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Wanneer het kenmerk labelgegevens aanwezig is op een aangeklikt element, wordt dit opgenomen met de interactiedetails die naar de Edge Network worden verzonden. De SDK van het Web zoekt een attribuut van etiketgegevens die met het element beginnen klikte en omhoog lopend de boom DOM. Het Web SDK gebruikt het eerste etiket het vindt. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Gebruik dit teken wanneer het leveraging van besluitvormingsbeleid in [ op code-gebaseerde campagnes van Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). U kunt het teken gebruiken om te onderscheiden welk punt van het besluitvormingsbeleid werd geklikt. Wanneer het kenmerk voor tokengegevens aanwezig is op een aangeklikt element, wordt dit opgenomen met de interactiedetails die naar de Edge Network worden verzonden. De SDK van het Web zoekt naar een attribuut van symbolische gegevens die met het element beginnen klikte en omhoog lopend de boom DOM. Het Web SDK gebruikt het eerste teken het vindt. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Web SDK voegt deze unieke id automatisch toe aan containerelementen bij het renderen van voorstellingen. Web SDK gebruikt deze id om DOM-elementen te correleren met voorstellingen. Aangezien dit een identiteitskaart door het Web SDK wordt vereist, zou u het op geen enkele manier moeten veranderen. U kunt het veilig negeren. |

## Voorbeeld

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### `autoCollectPropositionInteractions` gebruiken met de opdracht `applyPropositions` {#apply-propositions}

De opdracht [`applyPropositions`](../applypropositions.md) is een handige manier om voorstellingen te renderen naar de DOM. In het geval van op code-gebaseerde campagnes met JSON, kunt u dit bevel gebruiken om een bestaand element van DOM (of de die uw toepassingscode aan het scherm te correleren dat op de waarden JSON wordt gebaseerd) met een voorstel te correleren.

Deze correlatie activeert automatische interactietracering voor dat element en wijst dat element het aangewezen voorstel toe. Stel hiertoe de waarde `actionType` in op `track` .

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Automatische propositieinteracties configureren voor de Web SDK-tagextensie

De volgende twee vervolgkeuzemenu&#39;s bij het configureren van de Web SDK-tagextensie zijn het equivalent van dit object:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
