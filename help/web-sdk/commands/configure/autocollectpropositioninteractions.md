---
title: autoCollectPropositionInteractions
description: Leer hoe te om het Web SDK van het Experience Platform te vormen om verbindingsgegevens automatisch te verzamelen.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: 55c656e7fd08e98b75c20f0688a6697baf533291
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# `autoCollectPropositionInteractions`

De eigenschap `autoCollectPropositionInteractions` is een optionele instelling die bepaalt of de Web SDK automatisch propositieinteracties moet verzamelen.

De waarde is een kaart van besluitvormingsleveranciers, elk met waarde die erop wijst hoe de automatische voorstellingsinteractie zou moeten worden behandeld.

## Ondersteunde waarden {#supported-values}

Door gebrek, worden de automatische voorzettingsinteractie _altijd verzameld_ voor Adobe Journey Optimizer (`AJO`), en _nooit_ verzameld voor Adobe Target (`TGT`).

De standaardwaarde van `autoTrackPropositionInteractions` wordt hieronder weergegeven.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Raadpleeg de onderstaande tabel voor de ondersteunde configuratiewaarden voor elke beslissingsprovider.

| Waarde | Beschrijving |
| --- | --- |
| `always` | [!DNL Web SDK] verzamelt altijd automatisch `interact` -gebeurtenissen voor alle elementen die aan een voorstel zijn gekoppeld. |
| `never` | [!DNL Web SDK] verzamelt nooit automatisch `interact` -gebeurtenissen voor elementen die aan een voorstel zijn gekoppeld. |
| `decoratedElementsOnly` | [!DNL Web SDK] verzamelt automatisch `interact` -gebeurtenissen voor elementen die aan een voorstel zijn gekoppeld, maar alleen als het element gegevenskenmerken bevat die een label of token opgeven. |

## Automatisch interactieve elementen bijhouden {#logic}

Wanneer u automatische het volgen van propositieinteractie toelaat, zullen om het even welke kliks binnen een proposition element dat aan DOM wordt teruggegeven automatisch worden verzameld door [!DNL Web SDK]. Dit omvat alle ervaringen die door [!DNL Web SDK] automatisch naar de DOM worden gerenderd en ervaringen die met de opdracht [`applyPropositions`](../applypropositions.md) aan de DOM zijn gerenderd.

### Gegevenskenmerken {#data-attributes}

U kunt gegevenskenmerken op elementen gebruiken om specificiteit aan een interactie toe te voegen.

| Naam | Gegevenskenmerk | Beschrijving |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Wanneer het kenmerk labelgegevens aanwezig is op een aangeklikt element, wordt dit opgenomen met de interactiedetails die naar de [!DNL Edge Network] worden verzonden. [!DNL Web SDK] zoekt naar een kenmerk van labelgegevens dat begint met het element waarop is geklikt en dat de DOM-structuur doorloopt. De [!DNL Web SDK] gebruikt het eerste label dat wordt gevonden. |
| [!DNL Token] | `data-aep-click-token` | Gebruik dit teken wanneer het leveraging van besluitvormingsbeleid in [ op code-gebaseerde campagnes van Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). U kunt het teken gebruiken om te onderscheiden welk punt van het besluitvormingsbeleid werd geklikt. Wanneer het attribuut van symbolische gegevens op een geklikt element aanwezig is, is het inbegrepen met de interactiedetails die naar de Edge Network worden verzonden. De [!DNL Web SDK] zoekt naar een kenmerk voor tokengegevens dat begint met het element waarop is geklikt en dat de DOM-structuur doorloopt. De [!DNL Web SDK] gebruikt de eerste token die wordt gevonden. |
| [!DNL Interact ID] | `data-aep-interact-id` | De [!DNL Web SDK] voegt deze unieke id automatisch toe aan containerelementen bij het renderen van voorstellingen. Web SDK gebruikt deze id om [!DNL DOM] -elementen te correleren met voorstellingen. Aangezien dit een id is die vereist is door de [!DNL Web SDK] , mag u deze op geen enkele manier wijzigen. U kunt het veilig negeren. |

**Voorbeeld**

Raadpleeg het codefragment hieronder voor een voorbeeld van het gebruik van gegevenskenmerken.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### De opdracht `applyPropositions` {#apply-propositions}

Raadpleeg de documentatie bij [`applyPropositions`](../applypropositions.md) voor meer informatie over de werking van deze opdracht.

De opdracht `applyPropositions` is een handige manier om voorstellingen te renderen naar de [!DNL DOM] . In het geval van op code gebaseerde campagnes met `JSON` kunt u deze opdracht echter gebruiken om een bestaand [!DNL DOM] -element (of het element dat uw toepassingscode naar het scherm rendert op basis van de `JSON` -waarden) te correleren met een voorstel.

Deze correlatie activeert automatische interactietracering voor dat element en wijst dat element het aangewezen voorstel toe. Stel hiertoe de waarde `actionType` in op `track` .

**Voorbeeld**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Automatische voorstellingen en interacties inschakelen en klikken op bijhouden via de Web SDK-tagextensie {#tag-extension}

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw referentie van Adobe ID.
1. Navigeer aan **de Inzameling van Gegevens** > **Markeringen**.
1. Selecteer de gewenste eigenschap voor tags.
1. Navigeer aan **Uitbreidingen**, dan selecteren **&#x200B;**&#x200B;op de kaart van SDK van het Web van Adobe Experience Platform vormt.
1. De rol neer aan de **[!UICONTROL Data Collection]** sectie, dan selecteert checkbox **laat voorstellingen en interactie het volgen** toe.
1. Selecteer **sparen**, dan publiceer uw veranderingen.

## Automatische proposities en interactiekoppelingen bijhouden inschakelen via de Web SDK JavaScript-bibliotheek {#library}

In [!DNL Web SDK] is het bijhouden van voorstellen standaard ingeschakeld. U kunt deze echter verder configureren met de waarde `autoCollectPropositionInteractions` wanneer u de opdracht [`configure`](../configure/overview.md) uitvoert.

Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `{"AJO": "always", "TGT": "never"}` gebruikt. Als u propositieinteracties liever niet automatisch wilt bijhouden, stelt u de waarde in op `{"AJO": "never", "TGT": "never"}` .

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoCollectPropositionInteractions": {"AJO": "always", "TGT": "never"}
});
```
