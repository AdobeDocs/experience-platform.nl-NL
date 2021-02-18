---
title: Persoonlijke inhoud renderen met de SDK van het Adobe Experience Platform-web
description: Leer hoe u persoonlijke inhoud kunt renderen met de SDK van Adobe Experience Platform Web.
keywords: personalization;renderDecisions;sendEvent;decisions;resultScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Aangepaste inhoud renderen

Adobe Experience Platform [!DNL Web SDK] biedt ondersteuning voor het opvragen van persoonlijke oplossingen bij Adobe, waaronder Adobe Target. Er zijn twee wijzen voor verpersoonlijking: ophalen, inhoud die automatisch kan worden gerenderd en inhoud die de ontwikkelaar moet renderen. De SDK biedt ook mogelijkheden om flikkering](../personalization/manage-flicker.md) te beheren.[

## Inhoud automatisch renderen

De SDK rendert automatisch gepersonaliseerde inhoud wanneer u een gebeurtenis naar de server verzendt en `renderDecisions` als optie voor de gebeurtenis instelt op `true`.

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

U kunt verzoeken om de lijst van besluiten die als belofte op `sendEvent` bevel moeten worden teruggekeerd door `decisionScopes` optie te specificeren. Een werkingsgebied is een koord de laat de verpersoonlijkingsoplossing weten welk besluit u zou willen.

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
> Als u [!DNL Target] gebruikt, worden bereiken mBox op de server, slechts worden zij allen onmiddellijk gevraagd in plaats van individueel. Het globale mbox wordt altijd verzonden.

### Automatische inhoud ophalen

Als u `result.decisions` zou willen om de automatische terug te geven besluiten op te nemen en NIET automatisch laat teruggeven hen hebben, kunt u `renderDecisions` aan `false` plaatsen, en het speciale werkingsgebied `__view__` omvatten.
