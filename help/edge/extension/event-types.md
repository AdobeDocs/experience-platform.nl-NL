---
title: Gebeurtenistypen in de Adobe Experience Platform Web SDK-extensie
description: Leer hoe u gebeurtenistypen gebruikt die door de Adobe Experience Platform Web SDK-extensie in Adobe Experience Platform Launch worden geleverd.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# Gebeurtenistypen

Op deze pagina worden de Adobe Experience Platform-gebeurtenistypen beschreven die worden geleverd door de tagextensie Adobe Experience Platform Web SDK. Deze worden gebruikt om [bouwregels](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) en mag niet worden verward met de [`eventType` veld in XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).

## [!UICONTROL Send event complete]

Typisch, zou uw bezit één of meerdere regels hebben gebruikend [[!UICONTROL Send event] action](action-types.md#send-event) om gebeurtenissen naar Adobe Experience Platform Edge Network te verzenden. Elke keer dat een gebeurtenis naar Edge Network wordt verzonden, wordt een reactie met nuttige gegevens geretourneerd aan de browser. Zonder de [!UICONTROL Send event complete] gebeurtenistype, hebt u geen toegang tot deze geretourneerde gegevens.

Om tot de teruggekeerde gegevens toegang te hebben, creeer een afzonderlijke regel, dan voeg een [!UICONTROL Send event complete] aan de regel. Deze regel wordt teweeggebracht telkens als een succesvolle reactie van de server als resultaat van wordt ontvangen [!UICONTROL Send event] handeling.

Wanneer een [!UICONTROL Send event complete] Deze gebeurtenis activeert een regel en verschaft gegevens die door de server worden geretourneerd. Deze gegevens kunnen nuttig zijn voor het uitvoeren van bepaalde taken. Meestal voegt u een [!UICONTROL Custom code] handeling (van de [!UICONTROL Core] extensie) op dezelfde regel als die met de [!UICONTROL Send event complete] gebeurtenis. In de [!UICONTROL Custom code] handeling, heeft uw aangepaste code toegang tot een variabele met de naam `event`. Dit `event` De variabele bevat de gegevens die door de server worden geretourneerd.

Uw regel voor de behandeling van gegevens die van het Netwerk van de Rand zijn teruggekeerd zou iets als dit kunnen kijken:

![](./assets/send-event-complete.png)

Hieronder volgen enkele voorbeelden van het uitvoeren van bepaalde taken met behulp van de [!UICONTROL Custom code] in deze regel.

### Persoonlijke inhoud handmatig renderen

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Hiervoor typt u de volgende aangepaste code:

```javascript
var propositions = event.propositions;
```

Indien `event.propositions` bestaat, is het een serie die de voorwerpen van het verpersoonlijkingsvoorstel bevat. De voorstellingen die in de array zijn opgenomen, worden grotendeels bepaald door de manier waarop de gebeurtenis naar de server is verzonden.

Voor dit eerste scenario, veronderstel u niet hebt gecontroleerd [!UICONTROL Render decisions] Selectievakje en geen gegevens opgegeven [!UICONTROL decision scopes] binnen [!UICONTROL Send event] handeling die verantwoordelijk is voor het verzenden van de gebeurtenis.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In dit voorbeeld wordt `propositions` array bevat alleen voorstellingen met betrekking tot de gebeurtenis die in aanmerking komen voor automatische rendering.

De `propositions` array kan er ongeveer zo uitzien als in dit voorbeeld:

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

Wanneer u de gebeurtenis verzendt, wordt [!UICONTROL Render decisions] selectievakje is niet ingeschakeld, zodat de SDK niet heeft geprobeerd om inhoud automatisch te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering, en heeft deze aan u doorgegeven om de inhoud handmatig te renderen als u dat wilt. Merk op dat elk projectobject zijn `renderAttempted` eigenschap ingesteld op `false`.

Als u in plaats daarvan de [!UICONTROL Render decisions] Schakel het selectievakje in wanneer de gebeurtenis wordt verzonden. De SDK heeft dan geprobeerd alle profielen te renderen die in aanmerking komen voor automatische rendering. Dientengevolge zou elk van de propositievoorwerpen zijn hebben `renderAttempted` eigenschap ingesteld op `true`. In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot nu toe, hebt u slechts verpersoonlijkingsinhoud bekeken die voor automatische teruggeven (bijvoorbeeld, om het even welke inhoud die in Adobe Target Visual Experience Composer wordt gecreeerd) verkiest. Om het even welke verpersoonlijkingsinhoud terug te winnen _niet_ die in aanmerking komen voor automatische rendering, de inhoud aanvragen door het besluitvormingsbereik te bepalen met behulp van de [!UICONTROL Decision scopes] in het [!UICONTROL Send event] handeling. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

De [!UICONTROL Send event] de actie ziet er als volgt uit :

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In dit voorbeeld, als de voorstellen op de server worden gevonden die overeenkomt met `salutation` of `discount` bereik, worden ze geretourneerd en opgenomen in de `propositions` array. Houd er rekening mee dat voorstellingen die in aanmerking komen voor automatische rendering, ook in de toekomst worden opgenomen in de `propositions` array, ongeacht hoe u de [!UICONTROL Render decisions] of [!UICONTROL Decision scopes] in de [!UICONTROL Send event] handeling. De `propositions` array, in dit geval, zou er hetzelfde uitzien als in dit voorbeeld:

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

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld komt de voorgestelde toepassing overeen met de `discount` bereik is een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Stel dat u een element op uw pagina hebt met de id van `daily-special` en de inhoud van de `discount` voorstel in de `daily-special` element. Ga als volgt te werk:

1. Proposities verwijderen uit de `event` object.
1. Lijn door elk voorstel, zoekend het voorstel met een werkingsgebied van `discount`.
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat de inhoud van HTML is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u de `daily-special` -element op de pagina en vervang de HTML door de gepersonaliseerde inhoud.

Uw aangepaste code in het dialoogvenster [!UICONTROL Custom code] de actie kan er als volgt uitzien :

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

Tot de personalisatie-inhoud die door Adobe Target wordt geretourneerd, behoren [reactietokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het gebruikersinterface van Adobe Target worden gevormd.

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Typ hiertoe de volgende aangepaste code:

```javascript
var propositions = event.propositions;
```

Indien `event.propositions` bestaat, is het een serie die de voorwerpen van het verpersoonlijkingsvoorstel bevat. Zie [Persoonlijke inhoud handmatig renderen](#manually-render-personalized-content) voor meer informatie over de inhoud van `result.propositions`.

Stel dat u alle activiteitennamen wilt verzamelen van alle voorstellingen die automatisch door de web-SDK zijn gerenderd en deze in één array wilt plaatsen. Vervolgens kunt u de ene array naar een derde verzenden. In dit geval schrijft u aangepaste code in het dialoogvenster [!UICONTROL Custom code] actie voor:

1. Proposities verwijderen uit de `event` object.
1. Doorloop elk voorstel.
1. Bepaal of de SDK het voorstel heeft weergegeven.
1. Als zo, lijn door elk punt in het voorstel.
1. De naam van de activiteit ophalen uit het dialoogvenster `meta` eigenschap, dat een object is dat responstokens bevat.
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
            activityNames.push(activityName);  
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
