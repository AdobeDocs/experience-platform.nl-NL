---
title: Adobe Target gebruiken met de SDK van het Web van het Platform
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 835fbee335c1b125f22a33f1806680514dfd9a6f
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# [!DNL Adobe Target] gebruiken met [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen leveren en weergeven die in  [!DNL Adobe Target] het webkanaal worden beheerd. U kunt een redacteur WYSIWYG, genoemd [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), of een niet-visuele interface, [Op vorm-gebaseerde Composer van de Ervaring](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), gebruiken om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

De volgende functies zijn getest en worden momenteel ondersteund in [!DNL Target]:

* [A/B-tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Rapportage van indrukking en conversie](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-activiteiten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Gerichte ervaring](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [MVT (Multivariate Tests)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Native doelindruk en conversiemelding](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-ondersteuning](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Adobe Target] inschakelen

Ga als volgt te werk om [!DNL Target] in te schakelen:

1. Schakel [!DNL Target] in uw [datastream](../../fundamentals/datastreams.md) in met de juiste clientcode.
1. Voeg de optie `renderDecisions` toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook de volgende opties toevoegen:

* **`decisionScopes`**: Haal specifieke activiteiten op (handig voor activiteiten die zijn gemaakt met de op formulieren gebaseerde composer) door deze optie aan uw gebeurtenissen toe te voegen.
* **[Fragment](../manage-flicker.md)** vooraf verbergen: Alleen bepaalde delen van de pagina verbergen.

## Adobe Target VEC gebruiken

Als u de VEC met een [!DNL Platform Web SDK]-implementatie wilt gebruiken, installeert en activeert u de [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Voor meer informatie, zie [de helperuitbreiding van de Composer van de Visuele Ervaring](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) in *Adobe Target gids*.

## VEC-activiteiten automatisch renderen

De [!DNL Adobe Experience Platform Web SDK] heeft de macht om uw ervaringen automatisch terug te geven die via VEC van [!DNL Adobe Target] op het Web voor uw gebruikers worden bepaald. Als u aan [!DNL Experience Platform Web SDK] wilt aangeven dat VEC-activiteiten automatisch moeten worden gerenderd, verzendt u een gebeurtenis met `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
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
  }
);
```

## De op formulieren gebaseerde composer gebruiken

De [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) is een niet-visuele interface die nuttig is voor het configureren van [!UICONTROL A/B Tests]-, [!UICONTROL Experience Targeting]-, [!UICONTROL Automated Personalization]- en [!UICONTROL Recommendations]-activiteiten met verschillende typen reacties, zoals JSON, HTML, Image, enz. Afhankelijk van het reactietype of de beslissing die door [!DNL Target] zijn teruggekeerd, kan uw kernbedrijfslogica worden uitgevoerd. Om besluiten voor uw op vorm-Gebaseerde Composer activiteiten terug te winnen, verzend een gebeurtenis met alle &quot;DecisionScopes&quot;u een besluit voor wilt terugwinnen.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
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
    }
  );
```

## Beslissingsgebieden

`decisionScopes` definieert secties, locaties of delen van uw pagina&#39;s waar u een persoonlijke ervaring wilt weergeven. Deze `decisionScopes` zijn aanpasbaar en user-defined. Voor huidige [!DNL Target]-klanten wordt `decisionScopes` ook wel ‘mboxes’ genoemd. In [!DNL Target] UI, `decisionScopes` verschijnen als &quot;plaatsen.&quot;

## Het `__view__`-bereik

[!DNL Experience Platform Web SDK] verstrekt functionaliteit om acties terug te winnen VEC zonder zich het verlaten van SDK om de acties VEC voor u terug te geven. Verzend een gebeurtenis met `__view__` die als `decisionScopes` wordt bepaald.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Soorten publiek in XDM

Bij het bepalen van publiek voor uw [!DNL Target] activiteiten die via [!DNL Platform Web SDK] worden geleverd, [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) moet worden bepaald en worden gebruikt. Nadat u XDM schema&#39;s, klassen, en de groepen van het schemagebied bepaalt, kunt u [!DNL Target] publieksregel tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen [!DNL Target], worden XDM gegevens getoond in [!UICONTROL Audience Builder] als douaneparameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld, `web.webPageDetails.name`).

Als u [!DNL Target] activiteiten met vooraf bepaald publiek hebt die douaneparameters of een gebruikersprofiel gebruiken, worden zij niet correct geleverd via SDK. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box publiek dat zich richt op velden die worden ondersteund via de [!DNL Platform Web SDK] en die geen XDM vereisen. Deze velden zijn beschikbaar in de interface [!DNL Target] die geen XDM vereist:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

Zie [Categorieën voor soorten publiek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) in de *Adobe Target-gids* voor meer informatie.

### Eén profiel bijwerken

Met [!DNL Platform Web SDK] kunt u het profiel bijwerken naar het [!DNL Target]-profiel en naar [!DNL Platform Web SDK] als een ervaringsgebeurtenis.

Als u een [!DNL Target]-profiel wilt bijwerken, moet u ervoor zorgen dat de profielgegevens worden doorgegeven met het volgende:

* Onder `“data {“`
* Onder `“__adobe”`
* Voorvoegsel `“profile.”` bijv. als hieronder

| Sleutel | Type | Beschrijving |
| --- | --- | --- |
| `renderDecisions` | Boolean | Instrueert de personaliseringscomponent of het DOM acties zou moeten interpreteren |
| `decisionScopes` | Array `<String>` | Een lijst van werkingsgebied om besluiten voor terug te winnen |
| `xdm` | Object | Gegevens geformatteerd in XDM die in het Web SDK van het Platform als ervaringsgebeurtenis landen |
| `data` | Object | Willekeurige sleutel/waardeparen verzonden naar [!DNL Target] oplossingen onder de doelklasse. |

De typische [!DNL Platform Web SDK] code die dit bevel gebruikt kijkt als het volgende:

**`sendEvent`met profielgegevens**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform stuff (event & profile) }
});
```

**Voorbeeldcode**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
}) 
.then(console.log);
```

## Terminologie

__Besluiten:__ In  [!DNL Target]verband hebben beslissingen betrekking op de ervaring die is gekozen uit een activiteit.

__Schema:__ Het schema van een besluit is het soort aanbod in  [!DNL Target].

__Toepassingsgebied:__ het toepassingsgebied van de beschikking. In [!DNL Target], is het werkingsgebied mBox. Het globale mBox is het `__view__` werkingsgebied.

__XDM:__ XDM wordt geserialiseerd in puntnotatie en dan gezet in  [!DNL Target] als parameters mBox.
