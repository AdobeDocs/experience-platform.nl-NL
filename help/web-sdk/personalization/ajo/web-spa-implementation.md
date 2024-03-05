---
title: Implementatie van één pagina
description: Leer hoe u SPA weergaven implementeert in Adobe Journey Optimizer
exl-id: 1883251b-2d59-46d3-ac74-b8657edd0325
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Toepassingen van één pagina implementeren (SPA) {#web-spa-implementation}

Adobe Experience Platform Web SDK verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende-generatie, cliënt-zijtechnologieën, zoals single-page toepassingen (SPA) uit te voeren.

Traditionele websites werken met navigatiemodellen &quot;van pagina tot pagina&quot;, ook wel bekend als toepassingen met meerdere pagina&#39;s, waarbij websiteontwerpen nauw aan URL&#39;s zijn gekoppeld en voor overgangen van de ene webpagina naar de andere een pagina moet worden geladen.

De moderne Webtoepassingen, zoals enig-paginatoepassingen (SPA), hebben in plaats daarvan een model aangenomen dat snel gebruik van browser UI teruggeeft, die vaak van paginaatherladingen onafhankelijk is. Deze ervaringen kunnen door klanteninteractie, zoals rollen, klikken, en curseurbewegingen worden teweeggebracht. Naarmate de paradigma&#39;s van het moderne web zijn geëvolueerd, werkt de relevantie van traditionele generieke gebeurtenissen, zoals het laden van een pagina, voor het implementeren van personalisatie en experimenten niet meer.

![Levenscyclusdiagram van de pagina.](assets/web-spa-vs-traditional-lifecycle.png)

## Voordelen van het gebruik van Web SDK voor SPA {#web-spa-benefits}

Hier zijn sommige voordelen om SDK van het Web voor uw enig-paginatoepassingen te gebruiken:

* De capaciteit om alle aanbiedingen op pagina-lading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* De gebruikerservaring op uw site aanzienlijk verbeteren omdat aanbiedingen direct via de cache worden weergegeven, zonder vertraging die door traditionele serveraanroepen wordt geïntroduceerd.
* Eenmalige ontwikkelaarsopstelling laat marketers toe om verpersoonlijking en experimenteringsactiviteiten via de visuele redacteur van het Web van Adobe Journey Optimizer op uw SPA tot stand te brengen en in werking te stellen.

## XDM-weergaven en toepassingen van één pagina {#web-spa-xdm}

De Journey Optimizer-webeditor maakt gebruik van een concept dat _views_.

Weergaven zijn een logische groep visuele elementen die samen een SPA ervaring vormen. Een toepassing van één pagina kan daarom worden beschouwd als een overgang door meningen, in plaats van URLs, die op gebruikersinteractie wordt gebaseerd. Een weergave kan doorgaans een hele site, een enkele pagina of gegroepeerde visuele elementen op een pagina vertegenwoordigen.

In het volgende voorbeeld wordt een hypothetische online e-commercesite gebruikt om nader uit te leggen welke weergaven er zijn.

* Na het navigeren aan de huisplaats, bevordert een heldenbeeld seizoensgebonden inzamelingen evenals de verschillende productcatalogi beschikbaar op de plaats. In dit geval kan een weergave voor het gehele beginscherm worden gedefinieerd. Deze mening zou eenvoudig &quot;thuis&quot;kunnen worden genoemd.

  ![Voorbeeld van websitepagina weergeven.](assets/web-spa-home.png)

* Aangezien de klant meer in de producten wordt geinteresseerd die de zaken verkopen, besluiten zij om te klikken **Mannen** koppeling. Net als op de homepage, de gehele **Mannen** Deze pagina kan worden gedefinieerd als een weergave. Deze mening zou &quot;mannen&quot;kunnen worden genoemd.

  ![Voorbeeld van een websiteafbeelding met een specifieke weergave.](assets/web-spa-men.png)

* Aangezien een weergave kan worden gedefinieerd als een hele site of een groep visuele elementen op een site, kunnen de vier producten die op de productsite worden weergegeven, worden gegroepeerd en als een weergave worden beschouwd. Deze weergave zou &quot;producten&quot; kunnen worden genoemd.

  ![Voorbeeld van een websiteafbeelding met een specifieke weergave.](assets/web-spa-men-products.png)

* Wanneer de klant besluit op de knop **ALLE MANNEN** als u meer producten op de site wilt verkennen, verandert de URL van de website in dit geval niet, maar u kunt hier een weergave maken die alleen de tweede rij producten vertegenwoordigt die wordt weergegeven. De weergavenaam kan &#39;products-page-2&#39; zijn.

* De klant besluit een paar producten van de site te kopen en gaat verder naar het uitcheckscherm. Het kaartscherm zelf kan worden gekoppeld aan een weergave met de naam &quot;kar&quot;. U kunt ook een andere weergave in het kasscherm gebruiken om de aanbevolen producten hieronder af te handelen.

  ![Voorbeeld van een websiteafbeelding met een specifieke weergave.](assets/web-spa-cart.png)

Het concept van de standpunten kan veel verder worden uitgebreid. Dit zijn slechts een paar voorbeelden van weergaven die op een site kunnen worden gedefinieerd.

## XDM-weergaven implementeren {#implement-xdm-views}

XDM-weergaven kunnen in Adobe Journey Optimizer worden gebruikt om marketers in staat te stellen via de visuele editor van Journey Optimizer webpersonalisatie- en experimentatiecampagnes uit te voeren op SPA.

Hiervoor moeten de volgende stappen worden uitgevoerd om een eenmalige ontwikkelaarsinstelling te voltooien:

1. Installeren [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md) en de [webkanaalvereisten](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html) pagina.

2. Bepaal alle XDM meningen in uw enig-paginatoepassing die u wilt personaliseren.

3. Nadat u de XDM-weergaven hebt gedefinieerd, moet u de `sendEvent()` functie met `renderDecisions` instellen op `true` en de bijbehorende XDM-weergave in uw toepassing van één pagina. De XDM-weergave moet worden doorgegeven `xdm.web.webPageDetails.viewName`. Met deze stap kunnen marketers deze weergaven ontdekken in de Journey Optimizer-webeditor en er inhoudwijzigingen op toepassen:

```js
 alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
   "web": {
    "webPageDetails": {
    "viewName":"home"
   }
  }
 }
});
```

>[!NOTE]
>
>Op de eerste `sendEvent()` alle XDM-weergaven die aan de eindgebruiker moeten worden gerenderd, worden opgehaald en in cache geplaatst. Volgende `sendEvent()` De vraag met binnen overgegaan meningen XDM zal van het geheime voorgeheugen worden gelezen en zonder een servervraag teruggegeven.

## `sendEvent()` functievoorbeelden

Deze sectie schetst twee voorbeelden die tonen hoe te om te roepen `sendEvent()` in React voor een hypothetische e-commerce SPA.

### Voorbeeld 1: Introductiepagina A/B-test {#web-spa-sample-1}

Het marketing team wil tests A/B op de volledige homepage in werking stellen.

![Voorbeeldpagina van toepassing van één pagina.](assets/web-spa-home.png)

A/B-tests uitvoeren op de hele thuislocatie, `sendEvent()` moet worden aangeroepen met de XDM `viewName` instellen op `home`:

```js
function onViewChange() {

  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

  viewName = viewName || 'home'; // view name cannot be empty

  // Sanitize viewName to get rid of any trailing symbols derived from URL

  if (viewName.startsWith('#') || viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }

  alloy("sendEvent", {
    "renderDecisions": true,

    "xdm": {
      "web": {
        "webPageDetails": {
          "viewName":"home"
        }
      }
    }
  });
}

// react router v4

const history = syncHistoryWithStore(createBrowserHistory(), store);

history.listen(onViewChange);

// react router v3

<Router history={hashHistory} onUpdate={onViewChange} >
```

### Voorbeeld 2: Persoonlijke producten {#web-spa-sample-2}

Het marketingteam wil de tweede rij producten aanpassen door de kleur van het prijsetiket in rood te veranderen nadat een gebruiker klikt om alle producten van Men te zien.

![Voorbeeldpagina van een toepassing van één pagina met gepersonaliseerde producten.](assets/web-spa-men-products.png)

```js
function onViewChange(viewName) {

    alloy("sendEvent", {
        "renderDecisions": true,
        "xdm": {
            "web": {
                "webPageDetails": {
                    "viewName": viewName
                }
            }
        }
    });
}

class Products extends Component {

    render() {
        return (

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
