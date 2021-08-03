---
title: Gebeurtenistypen in de Adobe Experience Platform Web SDK-extensie
description: Leer hoe u gebeurtenistypen gebruikt die door de Adobe Experience Platform Web SDK-extensie in Adobe Experience Platform Launch worden geleverd.
solution: Experience Platform
feature: Web SDK
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Gebeurtenistypen

Op deze pagina worden de Adobe Experience Platform-gebeurtenistypen beschreven die worden geleverd door de tagextensie Adobe Experience Platform Web SDK. Deze worden gebruikt aan [bouwt regels](https://experienceleague.adobe.com/docs/launch-learn/tutorials/fundamentals/building-rules-in-launch.html) en zouden niet met het [`eventType` gebied in XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) moeten worden verward.

## [!UICONTROL Send event complete]

Doorgaans zou uw eigenschap een of meer regels hebben met de handeling [[!UICONTROL Send event]](action-types.md#send-event) om gebeurtenissen naar Adobe Experience Platform Edge Network te verzenden. Elke keer dat een gebeurtenis naar Edge Network wordt verzonden, wordt een reactie met nuttige gegevens geretourneerd aan de browser. Zonder het gebeurtenistype [!UICONTROL Send event complete] hebt u geen toegang tot deze geretourneerde gegevens.

Om tot de teruggekeerde gegevens toegang te hebben, creeer een afzonderlijke regel, dan voeg een [!UICONTROL Send event complete] gebeurtenis aan de regel toe. Deze regel wordt geactiveerd telkens wanneer een geslaagde reactie van de server wordt ontvangen als gevolg van een [!UICONTROL Send event]-actie.

Wanneer een gebeurtenis [!UICONTROL Send event complete] een regel activeert, levert deze gegevens die door de server worden geretourneerd, die nuttig kunnen zijn om bepaalde taken uit te voeren. Meestal voegt u een [!UICONTROL Custom code]-handeling (van de extensie [!UICONTROL Core]) toe aan dezelfde regel die de gebeurtenis [!UICONTROL Send event complete] bevat. In de [!UICONTROL Custom code] actie, zal uw douanecode toegang tot een variabele genoemd `event` hebben. Deze `event`-variabele bevat de gegevens die door de server worden geretourneerd.

Uw regel voor de behandeling van gegevens die van het Netwerk van de Rand zijn teruggekeerd zou iets als dit kunnen kijken:

![](./assets/send-event-complete.png)

Hieronder volgen enkele voorbeelden van hoe u bepaalde taken kunt uitvoeren met de handeling [!UICONTROL Custom code] in deze regel.

### Persoonlijke inhoud handmatig renderen

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Hiervoor typt u de volgende aangepaste code:

```javascript
var propositions = event.propositions;
```

Als `event.propositions` bestaat, is het een serie die voorwerpen van het verpersoonlijkingsvoorstel bevat. De voorstellingen die in de array zijn opgenomen, worden grotendeels bepaald door de manier waarop de gebeurtenis naar de server is verzonden.

Voor dit eerste scenario, veronderstel u niet [!UICONTROL Render decisions] checkbox hebt gecontroleerd en geen [!UICONTROL decision scopes] binnen de [!UICONTROL Send event] actie verstrekt verantwoordelijk voor het verzenden van de gebeurtenis.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In dit voorbeeld bevat de array `propositions` alleen voorstellingen met betrekking tot de gebeurtenis die in aanmerking komen voor automatische rendering.

De array `propositions` kan er ongeveer als volgt uitzien:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

Tijdens het verzenden van de gebeurtenis is het selectievakje [!UICONTROL Render decisions] niet ingeschakeld, zodat de SDK niet heeft geprobeerd om automatisch inhoud te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering, en heeft deze aan u doorgegeven om de inhoud handmatig te renderen als u dat wilt. Merk op dat elk propositievoorwerp zijn `renderAttempted` bezit heeft die aan `false` wordt geplaatst.

Als u in plaats daarvan het selectievakje [!UICONTROL Render decisions] zou hebben ingeschakeld bij het verzenden van de gebeurtenis, zou de SDK hebben geprobeerd om eventuele profielen te renderen die in aanmerking komen voor automatische rendering. Dientengevolge, zou elk van de propositievoorwerpen zijn `renderAttempted` bezit hebben die aan `true` wordt geplaatst. In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot dusver, hebt u slechts tot verpersoonlijkingsinhoud gekeken die voor automatische teruggeven (bijvoorbeeld, om het even welke inhoud die in Adobe Target Visual Experience Composer wordt gecreeerd) verkiest. Om om het even welke verpersoonlijkingsinhoud _niet_ terug te winnen geschikt voor automatische het teruggeven, verzoek de inhoud door besluitvormingswerkingsgebied te verstrekken gebruikend [!UICONTROL Decision scopes] gebied in [!UICONTROL Send event] actie. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

De actie [!UICONTROL Send event] zou als volgt kijken:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

Als in dit voorbeeld proposities worden gevonden op de server die overeenkomt met het bereik `salutation` of `discount`, worden deze geretourneerd en opgenomen in de array `propositions`. Houd er rekening mee dat proposities die in aanmerking komen voor automatische rendering, blijven worden opgenomen in de `propositions`-array, ongeacht hoe u de [!UICONTROL Render decisions]- of [!UICONTROL Decision scopes]-velden in de [!UICONTROL Send event]-handeling configureert. De `propositions`-array zou er in dit geval ongeveer als volgt uitzien:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld is het voorstel dat overeenkomt met het bereik `discount` een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Veronderstel u een element op uw pagina met identiteitskaart van `daily-special` hebt en wenst om de inhoud van het `discount` voorstel in het `daily-special` element terug te geven. Ga als volgt te werk:

1. Extraheer voorstellingen uit het object `event`.
1. Lijn door elk voorstel, zoekend het voorstel met een werkingsgebied van `discount`.
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat HTML-inhoud is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u het element `daily-special` op de pagina en vervangt u de HTML van het item door de gepersonaliseerde inhoud.

Uw aangepaste code in de handeling [!UICONTROL Custom code] kan er als volgt uitzien:

```javascript
var propositions = event.propositions;

var discountProposition;
if (propositions) {
  // Find the discount proposition, if it exists.
  for (var i = 0; i < propositions.length; i++) {
    var proposition = propositions[i]; 
    if (proposition.scope === "discount") {
      discountProposition = proposition;
      break;
    }
  }
}

var discountHtml;
if (discountProposition) {
  // Find the item from proposition that should be rendered.
  // Rather than assuming there a single item that has HTML
  // content, find the first item whose schema indicates
  // it contains HTML content.
  for (var j = 0; j < discountProposition.items.length; j++) {
    var discountPropositionItem = discountProposition.items[i]; 
    if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
      discountHtml = discountPropositionItem.data.content;
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### Adobe Target-respontokens openen

De inhoud van de Personalisatie die van Adobe Target is teruggekeerd omvat [reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het gebruikersinterface van Adobe Target worden gevormd.

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Typ hiertoe de volgende aangepaste code:

```javascript
var propositions = event.propositions;
```

Als `event.propositions` bestaat, is het een serie die voorwerpen van het verpersoonlijkingsvoorstel bevat. Zie [Persoonlijke inhoud handmatig renderen](#manually-render-personalized-content) voor meer informatie over de inhoud van `result.propositions`.

Stel dat u alle activiteitennamen wilt verzamelen van alle voorstellingen die automatisch door de web-SDK zijn gerenderd en deze in één array wilt plaatsen. Vervolgens kunt u de ene array naar een derde verzenden. In dit geval, schrijf douanecode binnen de [!UICONTROL Custom code] actie aan:

1. Extraheer voorstellingen uit het object `event`.
1. Doorloop elk voorstel.
1. Bepaal of de SDK het voorstel heeft weergegeven.
1. Als zo, lijn door elk punt in het voorstel.
1. Haal de naam van de activiteit van het `meta` bezit terug, dat een voorwerp is dat reactietokens bevat.
1. Zet de naam van de activiteit in een array.
1. Verzend de namen van de activiteiten naar een derde.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(item.meta);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```





