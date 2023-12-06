---
title: Toepassing van één pagina voor de SDK van het Web van Adobe Experience Platform
description: Leer hoe u een toepassing (SPA) van één pagina maakt met Adobe Target.
keywords: doel;adobe target;xdm meningen; meningen;enige paginatoepassingen;SPA;SPA levenscyclus;cliënt-kant;AB het testen;AB;De ervaring richt;XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 0%

---


# Implementatie van één pagina

Adobe Experience Platform Web SDK verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende-generatie, cliënt-zijtechnologieën zoals enig-paginatoepassingen (SPA) uit te voeren.

Traditionele websites werkten aan navigatiemodellen &quot;van pagina tot pagina&quot;, ook wel bekend als Toepassingen van meerdere pagina&#39;s, waarbij websiteontwerpen nauw gekoppeld waren aan URL&#39;s en overgangen van de ene webpagina naar de andere een pagina moesten laden.

De moderne Webtoepassingen, zoals enig-paginatoepassingen, hebben in plaats daarvan een model aangenomen dat snel gebruik van browser UI teruggeeft, die vaak onafhankelijk van paginaherladingen is. Deze ervaringen kunnen door klanteninteractie, zoals rollen, klikken, en curseurbewegingen worden teweeggebracht. Naarmate de paradigma&#39;s van het moderne web zijn geëvolueerd, werkt de relevantie van traditionele generieke gebeurtenissen, zoals het laden van een pagina, voor het implementeren van personalisatie en experimenten niet meer.

![Diagram waarin de SPA levenscyclus wordt weergegeven in vergelijking met de traditionele levenscyclus van de pagina.](assets/spa-vs-traditional-lifecycle.png)

## Voordelen van Platform Web SDK voor SPA

Hier volgen enkele voordelen van Adobe Experience Platform Web SDK voor uw single-page toepassingen:

* De capaciteit om alle aanbiedingen op pagina-lading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* Verbeter de gebruikerservaring op uw site aanzienlijk omdat aanbiedingen direct via de cache worden weergegeven zonder vertraging die door traditionele serveraanroepen is geïntroduceerd.
* Één enkele lijn van code en éénmalige ontwikkelaarsopstelling laat marketers toe om A/B en de Ervaring te creëren richtend (XT) activiteiten via Visual Experience Composer (VEC) op uw SPA.

## XDM-weergaven en toepassingen van één pagina

Adobe Target VEC for SPA maakt gebruik van een concept genaamd Views: een logische groep visuele elementen die samen een SPA ervaring vormen. Een toepassing van één pagina kan daarom worden beschouwd als het overgaan door Meningen, in plaats van URLs, die op gebruikersinteractie wordt gebaseerd. Een weergave kan doorgaans een hele site of gegroepeerde visuele elementen binnen een site vertegenwoordigen.

Om verder uit te leggen welke Weergaven zijn, gebruikt het volgende voorbeeld een hypothetische online e-commercesite die in React wordt uitgevoerd om voorbeeldweergaven te onderzoeken.

Na het navigeren naar de thuissite bevordert een hoofdafbeelding een paasverkoop en de nieuwste producten die op de site beschikbaar zijn. In dit geval kan een weergave worden gedefinieerd voor het gehele beginscherm. Deze weergave kan gewoon &#39;thuis&#39; worden genoemd.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster.](assets/example-views.png)

Aangezien de klant meer in de producten wordt geinteresseerd die de zaken verkopen, besluiten zij om te klikken **Producten** koppeling. Net als op de thuissite kan de hele productsite worden gedefinieerd als een weergave. Deze weergave kan de naam &quot;products-all&quot; hebben.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster, met alle producten weergegeven.](assets/example-products-all.png)

Aangezien een Mening als volledige plaats of een groep visuele elementen op een plaats kan worden bepaald, zouden de vier producten die op de productplaats worden getoond als Mening kunnen worden gegroepeerd en worden beschouwd. Deze weergave kan &#39;producten&#39; worden genoemd.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster, met voorbeeldproducten die worden weergegeven.](assets/example-products.png)

Wanneer de klant besluit op de knop **Meer laden** als u meer producten op de site wilt verkennen, verandert de URL van de website in dit geval niet, maar u kunt hier een weergave maken die alleen de tweede rij producten vertegenwoordigt die wordt weergegeven. De weergavenaam kan &#39;products-page-2&#39; zijn.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster, met voorbeeldproducten die op een extra pagina worden weergegeven.](assets/example-load-more.png)

De klant besluit een paar producten van de site te kopen en gaat verder naar het uitcheckscherm. Op de uitchecksite krijgt de klant opties om normale levering of expreslevering te kiezen. Een weergave kan uit elke groep visuele elementen op een site bestaan. Een weergave kan dus worden gemaakt voor leveringsvoorkeuren en &quot;Leveringsvoorkeuren&quot; worden genoemd.

![Voorbeeldafbeelding van een pagina voor het uitchecken van toepassingen in een browservenster.](assets/example-check-out.png)

Het concept van standpunten kan veel verder worden uitgebreid. Dit zijn slechts een paar voorbeelden van weergaven die op een site kunnen worden gedefinieerd.

## XDM-weergaven implementeren

XDM-weergaven kunnen in Adobe Target worden gebruikt om marketers in staat te stellen A/B- en XT-tests uit te voeren op SPA via Visual Experience Composer. Hiervoor moeten de volgende stappen worden uitgevoerd om een eenmalige ontwikkelaarsinstelling te voltooien:

1. Installeren [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Bepaal alle XDM-weergaven in uw toepassing voor één pagina die u wilt aanpassen.
3. Na het bepalen van de Meningen XDM, om de activiteiten van AB of XT VEC te leveren, voer uit `sendEvent()` functie met `renderDecisions` instellen op `true` en de bijbehorende XDM-weergave in uw toepassing Eén pagina. De XDM-weergave moet worden doorgegeven `xdm.web.webPageDetails.viewName`. Met deze stap kunnen marketers de Visual Experience Composer gebruiken om A/B- en XT-tests voor die XDM te starten.

   ```javascript
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
>Op de eerste `sendEvent()` alle XDM-weergaven die aan de eindgebruiker moeten worden gerenderd, worden opgehaald en in cache geplaatst. Volgende `sendEvent()` De vraag met binnen overgegaane Mening XDM zal van het geheime voorgeheugen worden gelezen en zonder een servervraag teruggegeven.

## `sendEvent()` functievoorbeelden

Deze sectie schetst drie voorbeelden die tonen hoe te om te roepen `sendEvent()` in React voor een hypothetische e-commerce SPA.

### Voorbeeld 1: Introductiepagina A/B-test

Het marketing team wil tests A/B op de volledige homepage in werking stellen.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster.](assets/use-case-1.png)

A/B-tests uitvoeren op de hele thuislocatie, `sendEvent()` moet worden aangeroepen met de XDM `viewName` instellen op `home`:

```jsx
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

### Voorbeeld 2: Persoonlijke producten

Het marketingteam wil de tweede rij producten personaliseren door de kleur van het prijslabel in rood te wijzigen nadat de gebruiker heeft geklikt **Meer laden**.

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster, met gepersonaliseerde aanbiedingen.](assets/use-case-2.png)

```jsx
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
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Voorbeeld 3: Voorkeuren voor de aflevering van een A/B-test

Het marketingteam wil een A/B-test uitvoeren om te zien of de kleur van de knop verandert van blauw in rood wanneer **Expreslevering** is geselecteerd, kan conversies stimuleren (in tegenstelling tot het blauw houden van de knopkleur voor beide leveringsopties).

![Voorbeeldafbeelding van een toepassing van één pagina in een browservenster, met A/B-tests.](assets/use-case-3.png)

Als u de inhoud op de site wilt aanpassen, afhankelijk van de gekozen leveringsvoorkeur, kunt u een weergave maken voor elke leveringsvoorkeur. Wanneer **Normale levering** is geselecteerd, kan de Mening &quot;controle-normaal&quot;worden genoemd. Indien **Expreslevering** is geselecteerd, kan de Mening &quot;checkout-express&quot;worden genoemd.

```jsx
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

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Het gebruiken van Visual Experience Composer voor een SPA

Als u klaar bent met het definiëren van uw XDM-weergaven en deze hebt geïmplementeerd `sendEvent()` met die Meningen XDM binnen worden overgegaan, zal VEC deze Meningen kunnen ontdekken en gebruikers toestaan om acties en wijzigingen voor A/B of XT activiteiten tot stand te brengen.

>[!NOTE]
>
>Om VEC voor uw SPA te gebruiken, moet u of installeren en activeren [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chroom](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

### Deelvenster Wijzigingen

In het deelvenster Wijzigingen worden de acties vastgelegd die voor een bepaalde weergave zijn gemaakt. Alle acties voor een weergave worden gegroepeerd onder die weergave.

![Het deelvenster Wijzigingen met opties voor het laden van pagina&#39;s die worden weergegeven in de zijbalk van het browservenster.](assets/modifications-panel.png)

### Acties

Wanneer u op een handeling klikt, wordt het element op de site gemarkeerd waarop deze handeling wordt toegepast. Elke VEC-actie die onder een Weergave wordt gemaakt, heeft de volgende pictogrammen: **Informatie**, **Bewerken**, **Klonen**, **Verplaatsen**, en **Verwijderen**. Deze pictogrammen worden nader toegelicht in de onderstaande tabel.

![Actiepictogrammen](assets/action-icons.png)

| Pictogram | Beschrijving |
|---|---|
| Informatie | Geeft de details van de handeling weer. |
| Bewerken | Hiermee kunt u de eigenschappen van de handeling rechtstreeks bewerken. |
| Klonen | Kloont de actie aan één of meerdere Weergaven die op het paneel van Aanpassingen of aan één of meerdere Weergaven bestaan die u hebt doorzocht en aan in VEC genavigeerd. De handeling hoeft niet noodzakelijkerwijs in het deelvenster Wijzigingen te staan.<br/><br/>**Opmerking:** Nadat een kloonverrichting wordt gemaakt, moet u aan de Mening in VEC via Browse navigeren om te zien of de gekloonde actie een geldige verrichting was. Als de actie niet op de Mening kan worden toegepast, zult u een fout zien. |
| Verplaatsen | Hiermee wordt de handeling verplaatst naar een gebeurtenis Pagina laden of een andere weergave die al bestaat in het deelvenster Wijzigingen.<br/><br/>**Gebeurtenis bij laden van pagina:** Alle handelingen die overeenkomen met de gebeurtenis load van de pagina worden toegepast op de eerste pagina die wordt geladen van uw webtoepassing. <br/><br/>**Opmerking:** Nadat een bewegingsverrichting wordt gemaakt, moet u aan de Mening in VEC via Browse navigeren om te zien of de beweging een geldige verrichting was. Als de actie niet op de Mening kan worden toegepast, zult u een fout zien. |
| Verwijderen | Hiermee verwijdert u de handeling. |

## VEC gebruiken voor SPA voorbeelden

Deze sectie schetst drie voorbeelden om de Visuele Composer van de Ervaring te gebruiken om acties en wijzigingen voor A/B of XT activiteiten tot stand te brengen.

### Voorbeeld 1: &quot;home&quot;-weergave bijwerken

Eerder in dit document is een weergave met de naam &quot;home&quot; gedefinieerd voor de gehele thuissite. Nu wil het marketingteam de weergave &quot;home&quot; op de volgende manieren bijwerken:

* Wijzig de **Toevoegen aan winkelwagentje** en **leuk** knoppen naar een lichter aandeel blauw. Dit moet gebeuren tijdens het laden van de pagina, omdat hierbij componenten van de koptekst worden gewijzigd.
* Wijzig de **Nieuwste producten voor 2019** label aan **Hottest-producten voor 2019** en wijzig de tekstkleur in paars.

Selecteer **Samenstellen** en pas deze wijzigingen toe op de weergave &quot;home&quot;.

![Voorbeeldpagina van Visual Experience Composer.](assets/vec-home.png)

### Voorbeeld 2: productlabels wijzigen

Voor de weergave &quot;products-page-2&quot; wil het marketingteam de **Prijs** label aan **Verkoopprijs** en wijzigt u de labelkleur in rood.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteren **Bladeren** in de VEC.
2. Selecteren **Producten** in de bovenste navigatie van de site.
3. Selecteren **Meer laden** één keer om de tweede rij producten te bekijken.
4. Selecteren **Samenstellen** in de VEC.
5. Handelingen toepassen om het tekstlabel te wijzigen in **Verkoopprijs** en de kleur rood.

![Voorbeeldpagina van Visual Experience Composer met productlabels.](assets/vec-products-page-2.png)

### Voorbeeld 3: Opmaak van leveringsvoorkeuren aanpassen

Weergaven kunnen worden gedefinieerd op korrelig niveau, zoals een status of een optie van een keuzerondje. Eerder in dit document zijn weergaven gedefinieerd voor leveringsvoorkeuren, &quot;uitchecken-normaal&quot; en &quot;uitchecken-express&quot;. Het marketingteam wil de kleur van de knop wijzigen in rood voor de weergave &quot;uitchecken-uitdrukken&quot;.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteren **Bladeren** in de VEC.
2. Voeg op de site producten toe aan het winkelwagentje.
3. Selecteer het winkelwagentje in de rechterbovenhoek van de site.
4. Selecteren **Je bestelling afhandelen**.
5. Selecteer de **Expreslevering** keuzerondje onder **Leveringsvoorkeuren**.
6. Selecteren **Samenstellen** in de VEC.
7. Wijzig de **Betalen** kleur naar rood.

>[!NOTE]
>
>De weergave Uitchecken wordt pas in het deelvenster Wijzigingen weergegeven als de **Expreslevering** keuzerondje is geselecteerd. Dit komt omdat de `sendEvent()` functie wordt uitgevoerd wanneer de **Expreslevering** Het keuzerondje is geselecteerd. De VEC is daarom niet op de hoogte van de weergave &quot;uitchecken&quot; totdat het keuzerondje is geselecteerd.

![Visuele Experience Composer die de voorkeurenkiezer voor levering weergeeft.](assets/vec-delivery-preference.png)
