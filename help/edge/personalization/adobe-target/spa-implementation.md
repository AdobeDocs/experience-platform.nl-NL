---
title: Toepassing van één pagina voor de SDK van het Web van Adobe Experience Platform
description: Leer hoe u een toepassing (SPA) van één pagina maakt met Adobe Target.
keywords: target;adobe target;xdm views; weergaven;toepassingen van één pagina;SPA;SPA levenscyclus;cliënt-kant;AB het testen;AB;De ervaring richt zich;XT;VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# Implementatie van één pagina

Adobe Experience Platform Web SDK verstrekt rijke eigenschappen die uw zaken uitrusten om verpersoonlijking op volgende-generatie, cliënt-zijtechnologieën zoals single-page toepassingen (SPA) uit te voeren.

Traditionele websites werkten aan navigatiemodellen &quot;van pagina tot pagina&quot;, ook wel bekend als Toepassingen van meerdere pagina&#39;s, waarbij websiteontwerpen nauw gekoppeld waren aan URL&#39;s en overgangen van de ene webpagina naar de andere een pagina moesten laden.

De moderne Webtoepassingen, zoals enig-paginatoepassingen, hebben in plaats daarvan een model aangenomen dat snel gebruik van browser UI teruggeeft, die vaak van paginaatherladingen onafhankelijk is. Deze ervaringen kunnen door klanteninteractie, zoals rollen, klikken, en curseurbewegingen worden teweeggebracht. Naarmate de paradigma&#39;s van het moderne web zijn geëvolueerd, werkt de relevantie van traditionele generieke gebeurtenissen, zoals het laden van een pagina, voor het implementeren van personalisatie en experimenten niet meer.

![](assets/spa-vs-traditional-lifecycle.png)

## Voordelen van Platform Web SDK voor SPA

Hier volgen enkele voordelen van Adobe Experience Platform Web SDK voor uw single-page toepassingen:

* De capaciteit om alle aanbiedingen op pagina-lading in het voorgeheugen onder te brengen om veelvoudige servervraag aan één enkele servervraag te verminderen.
* Verbeter de gebruikerservaring op uw site aanzienlijk omdat aanbiedingen direct via de cache worden weergegeven zonder vertraging die door traditionele serveraanroepen is geïntroduceerd.
* Één enkele lijn van code en éénmalige ontwikkelaarsopstelling laat marketers toe om A/B en Ervaring het richten (XT) activiteiten via Visual Experience Composer (VEC) op uw SPA tot stand te brengen en in werking te stellen.

## XDM-weergaven en toepassingen van één pagina

Adobe Target VEC for SPA maakt gebruik van het concept Views: een logische groep visuele elementen die samen een SPA ervaring vormen. Een toepassing van één pagina kan daarom worden beschouwd als het overgaan door Meningen, in plaats van URLs, die op gebruikersinteractie wordt gebaseerd. Een weergave kan doorgaans een hele site of gegroepeerde visuele elementen binnen een site vertegenwoordigen.

Om verder uit te leggen welke Weergaven zijn, gebruikt het volgende voorbeeld een hypothetische online e-commercesite die in React wordt uitgevoerd om voorbeeldweergaven te onderzoeken.

Na het navigeren naar de thuissite bevordert een hoofdafbeelding een paasverkoop en de nieuwste producten die op de site beschikbaar zijn. In dit geval kan een weergave worden gedefinieerd voor het gehele beginscherm. Deze weergave kan gewoon &#39;thuis&#39; worden genoemd.

![](assets/example-views.png)

Naarmate de klant meer interesse krijgt in de producten die het bedrijf verkoopt, besluit hij of zij op de koppeling **Producten** te klikken. Net als op de thuissite kan de hele productsite worden gedefinieerd als een weergave. Deze weergave kan de naam &quot;products-all&quot; hebben.

![](assets/example-products-all.png)

Aangezien een Mening als volledige plaats of een groep visuele elementen op een plaats kan worden bepaald, zouden de vier producten die op de productplaats worden getoond als Mening kunnen worden gegroepeerd en worden beschouwd. Deze weergave kan &#39;producten&#39; worden genoemd.

![](assets/example-products.png)

Wanneer de klant besluit op de knop **Meer laden** te klikken om meer producten op de site te verkennen, verandert de URL van de website in dit geval niet, maar u kunt hier een weergave maken die alleen de tweede rij producten vertegenwoordigt die wordt weergegeven. De weergavenaam kan &#39;products-page-2&#39; zijn.

![](assets/example-load-more.png)

De klant besluit een paar producten van de site te kopen en gaat verder naar het uitcheckscherm. Op de uitchecksite krijgt de klant opties om normale levering of expreslevering te kiezen. Een weergave kan uit elke groep visuele elementen op een site bestaan. Een weergave kan dus worden gemaakt voor leveringsvoorkeuren en &quot;Leveringsvoorkeuren&quot; worden genoemd.

![](assets/example-check-out.png)

Het concept van standpunten kan veel verder worden uitgebreid. Dit zijn slechts een paar voorbeelden van weergaven die op een site kunnen worden gedefinieerd.

## XDM-weergaven implementeren

XDM-weergaven kunnen in Adobe Target worden gebruikt om marketers in staat te stellen A/B- en XT-tests uit te voeren op SPA via Visual Experience Composer. Hiervoor moeten de volgende stappen worden uitgevoerd om een eenmalige ontwikkelaarsinstelling te voltooien:

1. [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md) installeren
2. Bepaal alle XDM-weergaven in uw toepassing voor één pagina die u wilt aanpassen.
3. Na het bepalen van de meningen XDM, om AB of XT VEC activiteiten te leveren, voer de `sendEvent()` functie met `renderDecisions` uit die aan `true` en de overeenkomstige Mening XDM in uw Enige Toepassing van de Pagina wordt geplaatst. De XDM-weergave moet worden doorgegeven in `xdm.web.webPageDetails.viewName`. Met deze stap kunnen marketers de Visual Experience Composer gebruiken om A/B- en XT-tests voor die XDM te starten.

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
>Voor de eerste `sendEvent()` vraag, zullen alle Meningen XDM die aan de eindgebruiker zouden moeten worden teruggegeven worden opgehaald en in het voorgeheugen ondergebracht. Volgende `sendEvent()`-aanroepen met doorgegeven XDM Views worden gelezen uit de cache en gerenderd zonder een serveraanroep.

## `sendEvent()` functievoorbeelden

Deze sectie schetst drie voorbeelden die tonen hoe te om de `sendEvent()` functie in React voor een hypothetische e-commerce SPA aan te halen.

### Voorbeeld 1: Introductiepagina van A/B-test

Het marketing team wil tests A/B op de volledige homepage in werking stellen.

![](assets/use-case-1.png)

Als u A/B-tests wilt uitvoeren op de hele thuissite, moet `sendEvent()` worden aangeroepen met de XDM `viewName` ingesteld op `home`:

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

Het marketingteam wil de tweede rij producten aanpassen door de kleur van het prijsetiket in rood te veranderen nadat de gebruiker **Meer laden** klikt.

![](assets/use-case-2.png)

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
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Voorbeeld 3: Voorkeuren voor A/B-testlevering

Het marketingteam wil een A/B-test uitvoeren om te zien of het wijzigen van de kleur van de knop van blauw in rood wanneer **Uitdrukkelijke levering** wordt geselecteerd, conversies kan stimuleren (in plaats van de knopkleur blauw te houden voor beide leveringsopties).

![](assets/use-case-3.png)

Als u de inhoud op de site wilt aanpassen, afhankelijk van de geselecteerde leveringsvoorkeur, kunt u een weergave maken voor elke leveringsvoorkeur. Wanneer **Normale levering** wordt geselecteerd, kan de Mening &quot;checkout-normal&quot;worden genoemd. Als **Uitdrukkelijke Levering** wordt geselecteerd, kan de Mening &quot;checkout-express&quot;worden genoemd.

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

Als u klaar bent met het definiëren van uw XDM-weergaven en `sendEvent()` hebt geïmplementeerd met de XDM Views die zijn doorgegeven, kan de VEC deze weergaven detecteren en gebruikers toestaan handelingen en wijzigingen voor A/B- of XT-activiteiten te maken.

>[!NOTE]
>
>Als u de VEC voor uw SPA wilt gebruiken, moet u de [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension installeren en activeren.

### Deelvenster Wijzigingen

In het deelvenster Wijzigingen worden de acties vastgelegd die voor een bepaalde weergave zijn gemaakt. Alle acties voor een weergave worden gegroepeerd onder die weergave.

![](assets/modifications-panel.png)

### Acties

Wanneer u op een handeling klikt, wordt het element op de site gemarkeerd waarop deze handeling wordt toegepast. Elke VEC-actie die onder een Weergave wordt gemaakt, heeft de volgende pictogrammen: **Informatie**, **Bewerken**, **Klonen**, **Verplaatsen** en **Verwijderen**. Deze pictogrammen worden nader toegelicht in de onderstaande tabel.

![](assets/action-icons.png)

| Pictogram | Beschrijving |
|---|---|
| Informatie | Geeft de details van de handeling weer. |
| Bewerken | Hiermee kunt u de eigenschappen van de handeling rechtstreeks bewerken. |
| Klonen | Kloont de actie aan één of meerdere Weergaven die op het paneel van Aanpassingen of aan één of meerdere Weergaven bestaan die u hebt doorzocht en aan in VEC genavigeerd. De handeling hoeft niet noodzakelijkerwijs in het deelvenster Wijzigingen te staan.<br/><br/>**Opmerking:** Nadat een kloonbewerking is uitgevoerd, moet u naar de Weergave in de VEC navigeren via Bladeren om te zien of de gekloonde actie een geldige bewerking was. Als de actie niet op de Mening kan worden toegepast, zult u een fout zien. |
| Verplaatsen | Hiermee wordt de handeling verplaatst naar een gebeurtenis Pagina laden of een andere weergave die al bestaat in het deelvenster Wijzigingen.<br/><br/>**Gebeurtenis bij laden van pagina:** alle handelingen die overeenkomen met de gebeurtenis load van de pagina worden toegepast op het eerste laden van de pagina van de webtoepassing. <br/><br/>**Nota:** nadat een bewegingsverrichting wordt gemaakt, moet u aan de Mening in VEC via Browse navigeren om te zien of de beweging een geldige verrichting was. Als de actie niet op de Mening kan worden toegepast, zult u een fout zien. |
| Verwijderen | Hiermee verwijdert u de handeling. |

## VEC gebruiken voor SPA voorbeelden

Deze sectie schetst drie voorbeelden om de Visuele Composer van de Ervaring te gebruiken om acties en wijzigingen voor A/B of XT activiteiten tot stand te brengen.

### Voorbeeld 1: &quot;home&quot;-weergave bijwerken

Eerder in dit document is een weergave met de naam &quot;home&quot; gedefinieerd voor de gehele thuissite. Nu wil het marketingteam de weergave &quot;home&quot; op de volgende manieren bijwerken:

* Wijzig de knoppen **Toevoegen aan winkelwagentje** en **Zoals** in een lichtere deelkleur blauw. Dit moet gebeuren tijdens het laden van de pagina, omdat hierbij componenten van de koptekst worden gewijzigd.
* Wijzig het **Nieuwste product voor 2019**-label in **Hottest-producten voor 2019** en wijzig de tekstkleur in paars.

Als u deze updates in de VEC wilt uitvoeren, selecteert u **Samenstellen** en past u deze wijzigingen toe op de weergave &quot;home&quot;.

![](assets/vec-home.png)

### Voorbeeld 2: Productlabels wijzigen

Voor de weergave &quot;products-page-2&quot; wil het marketingteam het label **Price** wijzigen in **Verkoopprijs** en de labelkleur wijzigen in rood.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteer **Browse** in VEC.
2. Selecteer **Producten** in de hoogste navigatie van de plaats.
3. Selecteer **Meer laden** eenmaal om de tweede rij producten weer te geven.
4. Selecteer **Samenstellen** in VEC.
5. Pas acties toe om het tekstlabel te wijzigen in **Verkoopprijs** en de kleur in rood.

![](assets/vec-products-page-2.png)

### Voorbeeld 3: Voorkeursindeling voor levering aanpassen

Weergaven kunnen worden gedefinieerd op korrelig niveau, zoals een status of een optie van een keuzerondje. Eerder in dit document zijn weergaven gedefinieerd voor leveringsvoorkeuren, &quot;uitchecken-normaal&quot; en &quot;uitchecken-express&quot;. Het marketingteam wil de kleur van de knop wijzigen in rood voor de weergave &quot;uitchecken-uitdrukken&quot;.

Om deze updates in VEC te maken, zijn de volgende stappen vereist:

1. Selecteer **Browse** in VEC.
2. Voeg op de site producten toe aan het winkelwagentje.
3. Selecteer het winkelwagentje in de rechterbovenhoek van de site.
4. Selecteer **Uw bestelling uitchecken**.
5. Selecteer het keuzerondje **Expreslevering** onder **Leveringsvoorkeuren**.
6. Selecteer **Samenstellen** in VEC.
7. Wijzig de **Pay** knopkleur in rood.

>[!NOTE]
>
>De weergave Uitchecken wordt pas weergegeven in het deelvenster Wijzigingen als het keuzerondje **Uitdrukkelijke levering** is geselecteerd. De reden hiervoor is dat de functie `sendEvent()` wordt uitgevoerd wanneer het keuzerondje **Express Delivery** is geselecteerd. Daarom is de VEC niet op de hoogte van de weergave &quot;uitchecken-express&quot; totdat het keuzerondje is geselecteerd.

![](assets/vec-delivery-preference.png)
