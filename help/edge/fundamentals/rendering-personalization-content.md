---
title: Aangepaste inhoud renderen
seo-title: Adobe Experience Platform Web SDK gepersonaliseerde inhoud renderen
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven
seo-description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Overzicht van opties voor personalisatie

De SDK van het Web van de Adobe Experience Platform steunt het vragen van de verpersoonlijkingsoplossingen bij Adobe, met inbegrip van Adobe Target. Er zijn twee wijzen voor verpersoonlijking: ophalen, inhoud die automatisch kan worden gerenderd en inhoud die de ontwikkelaar moet renderen. De SDK biedt ook mogelijkheden om flikkering te [beheren](../../edge/solution-specific/target/flicker-management.md).

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

U kunt de lijst van besluiten verzoeken om als belofte op het `event` bevel te zijn teruggekeerd door te gebruiken `scopes`. Een werkingsgebied is een koord de laat de verpersoonlijkingsoplossing weten welk besluit u zou willen.

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
    }
  })
```

Dit zal een lijst van besluiten als voorwerp JSON voor elke besluiten terugkeren.

```javascript
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
> Als u Target-bereik gebruikt als een box op de server, zijn alleen alle aanvragen tegelijk in plaats van afzonderlijk ingediend. Het globale mbox wordt altijd verzonden.

### Automatische inhoud ophalen

Als u wilt dat de automatische renderbare beslissingen in de selectie worden opgenomen, kunt u instellen `result.decisions` op false en het speciale bereik opnemen `renderDecisions` `__view__`.
