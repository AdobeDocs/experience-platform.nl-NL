---
title: Gebeurtenistypen in de Adobe Experience Platform Web SDK-extensie
description: Leer hoe u gebeurtenistypen gebruikt die door de Adobe Experience Platform Web SDK-extensie in Adobe Experience Platform Launch worden geleverd.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 666e8c6fcccf08d0841c5796677890409b22d794
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 0%

---

# Gebeurtenistypen

Op deze pagina worden de Adobe Experience Platform-gebeurtenistypen beschreven die worden geleverd door de tagextensie Adobe Experience Platform Web SDK. Deze worden gebruikt aan [ bouwt regels ](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) en zou niet met het `eventType` gebied in het [`xdm` voorwerp ](/help/web-sdk/commands/sendevent/xdm.md) moeten worden verward.

## [!UICONTROL Send event complete]

Typisch, zou uw bezit één of meerdere regels hebben gebruikend [[!UICONTROL Send event] actie ](action-types.md#send-event) om gebeurtenissen naar de Edge Network van Adobe Experience Platform te verzenden. Telkens wanneer een gebeurtenis naar de Edge Network wordt verzonden, wordt een reactie teruggegeven aan browser met nuttige gegevens. Zonder het gebeurtenistype [!UICONTROL Send event complete] hebt u geen toegang tot deze geretourneerde gegevens.

Als u toegang wilt krijgen tot de geretourneerde gegevens, maakt u een aparte regel en voegt u vervolgens een [!UICONTROL Send event complete] -gebeurtenis aan de regel toe. Deze regel wordt geactiveerd telkens wanneer een geslaagde reactie van de server wordt ontvangen als gevolg van een [!UICONTROL Send event] -actie.

Wanneer een [!UICONTROL Send event complete] -gebeurtenis een regel activeert, levert deze gegevens die door de server worden geretourneerd, die nuttig kunnen zijn om bepaalde taken uit te voeren. Meestal voegt u een [!UICONTROL Custom code] -actie (van de [!UICONTROL Core] -extensie) toe aan dezelfde regel die de [!UICONTROL Send event complete] -gebeurtenis bevat. In de handeling [!UICONTROL Custom code] heeft uw aangepaste code toegang tot een variabele met de naam `event` . Deze `event` -variabele bevat de gegevens die door de server worden geretourneerd.

Uw regel voor de behandeling van gegevens die van Edge Network zijn teruggekeerd zou iets als dit kunnen kijken:

![](assets/send-event-complete.png)

Hieronder volgen enkele voorbeelden van het uitvoeren van bepaalde taken met behulp van de handeling [!UICONTROL Custom code] in deze regel.

### Persoonlijke inhoud handmatig renderen

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Hiervoor typt u de volgende aangepaste code:

```javascript
var propositions = event.propositions;
```

Als `event.propositions` bestaat, is het een array die objecten voor een verpersoonlijkingsvoorstel bevat. De voorstellingen die in de array zijn opgenomen, worden grotendeels bepaald door de manier waarop de gebeurtenis naar de server is verzonden.

Voor dit eerste scenario gaat u ervan uit dat u het selectievakje [!UICONTROL Render decisions] niet hebt ingeschakeld en geen [!UICONTROL decision scopes] in de [!UICONTROL Send event] -actie hebt opgegeven die verantwoordelijk is voor het verzenden van de gebeurtenis.

![ img.png ](assets/send-event-render-unchecked-without-scopes.png)

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

Tijdens het verzenden van de gebeurtenis is het selectievakje [!UICONTROL Render decisions] niet ingeschakeld. De SDK heeft dus niet geprobeerd om automatisch inhoud te renderen. De SDK heeft echter nog steeds automatisch de inhoud opgehaald die in aanmerking komt voor automatische rendering, en heeft deze aan u doorgegeven om de inhoud handmatig te renderen als u dat wilt. Voor elk propositieobject is de eigenschap `renderAttempted` ingesteld op `false` .

Als u in plaats daarvan het selectievakje [!UICONTROL Render decisions] zou hebben ingeschakeld bij het verzenden van de gebeurtenis, zou de SDK hebben geprobeerd om eventuele profielen te renderen die in aanmerking komen voor automatische rendering. Als gevolg hiervan zou de eigenschap `renderAttempted` van elk propositieobject zijn ingesteld op `true` . In dit geval is het niet nodig deze voorstellen handmatig weer te geven.

Tot dusver, hebt u slechts tot verpersoonlijkingsinhoud gekeken die voor automatische teruggeven (bijvoorbeeld, om het even welke inhoud die in Adobe Target Visual Experience Composer wordt gecreeerd) verkiest. Om om het even welke verpersoonlijkingsinhoud terug te winnen _niet_ geschikt voor automatische teruggeven, verzoek de inhoud door besluitvormingswerkingsgebied te verstrekken gebruikend het [!UICONTROL Decision scopes] gebied in de [!UICONTROL Send event] actie. Een werkingsgebied is een koord dat een bepaald voorstel identificeert u van de server zou willen terugwinnen.

De handeling [!UICONTROL Send event] ziet er als volgt uit:

![ img.png ](assets/send-event-render-unchecked-with-scopes.png)

Als in dit voorbeeld proposities worden gevonden op de server die overeenkomt met het bereik `salutation` of `discount` , worden deze geretourneerd en opgenomen in de array `propositions` . Houd er rekening mee dat proposities die in aanmerking komen voor automatische rendering, ook in de toekomst in de array `propositions` worden opgenomen, ongeacht hoe u de velden [!UICONTROL Render decisions] of [!UICONTROL Decision scopes] in de handeling [!UICONTROL Send event] configureert. De array `propositions` ziet er in dit geval ongeveer als volgt uit:

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

Op dit punt kunt u propositie-inhoud naar eigen inzicht renderen. In dit voorbeeld is het voorstel dat overeenkomt met het bereik van `discount` een HTML-voorstel dat is gemaakt met behulp van Adobe Target Form-based Experience Composer. Stel dat u een element op de pagina hebt met de id `daily-special` en de inhoud van het `discount` proposition wilt weergeven in het `daily-special` -element. Ga als volgt te werk:

1. Extraheer voorstellen uit het `event` -object.
1. Doorloop elk voorstel en zoek het voorstel met een bereik van `discount` .
1. Als u een voorstel vindt, doorloopt u elk item in het voorstel en zoekt u het item dat de inhoud van HTML is. (Het is beter om te controleren dan om te veronderstellen.)
1. Als u een item vindt dat HTML-inhoud bevat, zoekt u het `daily-special` -element op de pagina en vervangt u de HTML door de gepersonaliseerde inhoud.

De aangepaste code in de handeling [!UICONTROL Custom code] kan er als volgt uitzien:

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

De inhoud van Personalization die van Adobe Target is teruggekeerd omvat [ reactietokens ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die details over de activiteit, de aanbieding, de ervaring, het gebruikersprofiel, geo informatie, en meer zijn. Deze details kunnen met derdehulpmiddelen worden gedeeld of voor het zuiveren worden gebruikt. De tokens van de reactie kunnen in het gebruikersinterface van Adobe Target worden gevormd.

In de actie van de Code van de Douane, die in de regel voor de behandeling van reactiegegevens is, kunt u tot verpersoonlijkingsvoorstellen toegang hebben die van de server zijn teruggekeerd. Voer hiertoe de volgende aangepaste code in:

```javascript
var propositions = event.propositions;
```

Als `event.propositions` bestaat, is het een array die objecten voor een verpersoonlijkingsvoorstel bevat. Zie [ manueel gepersonaliseerde inhoud ](#manually-render-personalized-content) voor meer informatie over de inhoud van `result.propositions` teruggeven.

Stel dat u alle activiteitennamen wilt verzamelen van alle voorstellingen die automatisch door de web-SDK zijn gerenderd en deze in één array wilt plaatsen. Vervolgens kunt u de ene array naar een derde verzenden. In dit geval schrijft u aangepaste code binnen de handeling [!UICONTROL Custom code] naar:

1. Extraheer voorstellen uit het `event` -object.
1. Lijn door elk voorstel.
1. Bepaal of de SDK het voorstel heeft weergegeven.
1. Als zo, lijn door elk punt in het voorstel.
1. Haal de naam van de activiteit op uit de eigenschap `meta` . Dit is een object dat responstokens bevat.
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

## [!UICONTROL Subscribe ruleset items] {#subscribe-ruleset-items}

Met het gebeurtenistype **[!UICONTROL Subscribe ruleset items]** kunt u zich abonneren op Adobe Journey Optimizer-inhoudskaarten voor een oppervlak. Telkens wanneer de regels worden geëvalueerd, ontvangt de callback die aan dit bevel wordt verstrekt een resultaatvoorwerp met voorstellen die de gegevens van de inhoudskaart houden.

![ Beeld van het gebruikersinterface van de markeringen van het Experience Platform die het de puntgebeurtenistype van de Linialen van het Abonneren tonen.](assets/subscribe-ruleset-items.png)

Dit gebeurtenistype ondersteunt de volgende configureerbare eigenschappen:

* **[!UICONTROL Schemas]**: Een array van schema&#39;s waarvoor u zich op inhoudskaarten wilt abonneren. U kunt de schema&#39;s manueel ingaan of door een gegevenselement te verstrekken.
* **[!UICONTROL Surfaces]**: een array met oppervlakken waarvoor u zich wilt abonneren op inhoudskaarten. U kunt de oppervlakken handmatig invoeren of een gegevenselement opgeven.
