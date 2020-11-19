---
title: Aangepaste inhoud renderen
seo-title: Adobe Experience Platform Web SDK Persoonlijke inhoud renderen
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven
seo-description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Overzicht van opties voor personalisatie

Adobe Experience Platform [!DNL Web SDK] ondersteunt het opvragen van personalisatieoplossingen bij Adobe, waaronder Adobe Target. Er zijn twee wijzen voor verpersoonlijking: ophalen, inhoud die automatisch kan worden gerenderd en inhoud die de ontwikkelaar moet renderen. De SDK biedt ook mogelijkheden om flikkering te [beheren](../personalization/manage-flicker.md).

## Inhoud automatisch renderen

De SDK rendert automatisch gepersonaliseerde inhoud wanneer u een gebeurtenis naar de server verzendt en instelt `renderDecisions` op `true` als optie voor de gebeurtenis.

```javascript
alloy("sendEvent", {
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
});
```

Het renderen van gepersonaliseerde inhoud is asynchroon, dus er mag geen enkele veronderstelling bestaan wanneer een bepaald stuk inhoud deel uitmaakt van de pagina.

## Inhoud handmatig renderen

U kunt de lijst van besluiten verzoeken om als belofte op het `sendEvent` bevel te zijn teruggekeerd door de `decisionScopes` optie te specificeren. Een werkingsgebied is een koord de laat de verpersoonlijkingsoplossing weten welk besluit u zou willen.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Dit zal een lijst van besluiten als voorwerp JSON voor elke besluiten terugkeren.

```json
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Als u [!DNL Target], werkingsgebied wordt mBoxes op de server gebruikt, slechts worden zij allen gevraagd tegelijkertijd in plaats van individueel. Het globale mbox wordt altijd verzonden.

### Automatische inhoud ophalen

Als u de automatische renderbare beslissingen `result.decisions` wilt opnemen en NIET automatisch renderen wilt hebben, kunt u instellen `renderDecisions` op `false`en het speciale bereik opnemen `__view__`.
