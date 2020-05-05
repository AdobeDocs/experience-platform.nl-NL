---
title: Aangepaste inhoud renderen
seo-title: Adobe Experience Platform Web SDK Persoonlijke inhoud renderen
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Platform van de Ervaring terug te geven
seo-description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Platform van de Ervaring terug te geven
translation-type: tm+mt
source-git-commit: bb3841da8a566105fde1b7ac78dccd79a7ea15d4

---


# (Bèta) Overzicht van de Opties van de Personalisatie

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De Adobe Experience Platform Web SDK ondersteunt het opvragen van de personalisatieoplossingen bij Adobe, waaronder Adobe Target. Er zijn twee wijzen voor verpersoonlijking: ophalen, inhoud die automatisch kan worden gerenderd en inhoud die de ontwikkelaar moet renderen. De SDK biedt ook mogelijkheden om flikkering te [beheren](managing-flicker.md).

## Inhoud automatisch renderen

De SDK rendert automatisch gepersonaliseerde inhoud wanneer u een gebeurtenis naar de server verzendt en instelt `renderDecisions` op `true` als optie voor de gebeurtenis.

```javascript
alloy("event", {
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
alloy("event",{
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

{info}Als u het werkingsgebied van het Doel wordt mBox op de server, slechts zijn zij alle verzoeken in één keer in plaats van individueel. Het globale mbox wordt altijd verzonden.
{info}

### Automatische inhoud ophalen

Als u de automatische renderbare beslissingen wilt opnemen, kunt u instellen `result.decisions` `renderDecisions` op false en het speciale bereik opnemen `__view__`
