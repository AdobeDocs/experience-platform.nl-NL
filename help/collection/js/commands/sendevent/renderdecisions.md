---
title: renderDecisions
description: Render gepersonaliseerde inhoud die in aanmerking komt voor automatische rendering.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

Met de eigenschap `renderDecisions` kunt u de Web SDK dwingen gepersonaliseerde inhoud te renderen die in aanmerking komt voor automatische rendering.

Stel de Booleaanse waarde `renderDecisions` in wanneer u de opdracht `sendEvent` uitvoert. Als deze eigenschap wordt weggelaten, wordt deze standaard ingesteld op `false` . Stel deze eigenschap in op `true` als u gepersonaliseerde inhoud automatisch wilt renderen.

>[!IMPORTANT]
>
>De eigenschap `renderDecisions` is niet compatibel met de eigenschap [`documentUnloading`](documentunloading.md) . Stel beide eigenschappen niet tegelijkertijd in op `true` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Wanneer u deze eigenschap instelt op `true` , moet u ook het bijbehorende bereik of de bijbehorende oppervlakken opnemen. Dit bereik of deze oppervlakken kunnen automatisch worden aangevraagd (bijvoorbeeld bij de eerste `sendEvent` -opdracht op een pagina) of expliciet (met [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) of [`personalization.surfaces`](personalization.md#personalizationsurfaces) ). Een veel voorkomend probleem bij het renderen van personalisatie is het volgende scenario:

1. Een `sendEvent` -opdracht wordt eerder uitgevoerd op de pagina die een standaardaanpassing aanvraagt, maar `renderDecisions` niet ingesteld (de standaardwaarde is `false` ). Proposities worden opgehaald maar niet gerenderd.
1. Later op de pagina wordt een andere `sendEvent` -gebeurtenis geactiveerd waarbij `renderDecisions` is ingesteld op `true` , maar zonder bereik of oppervlak. Aangezien er geen werkingsgebied of oppervlakten in deze tweede vraag zijn, wordt niets teruggegeven.

U kunt dit probleem voorkomen door:

* `renderDecisions` instellen op `true` bij de eerste `sendEvent` -aanroep; of
* Expliciet `decisionScopes` of `surfaces` instellen voor een volgende `sendEvent` oproep bij het instellen van `renderDecisions` op `true` .

## Beslissingen renderen met de Web SDK-tagextensie

Het de markeringsequivalent van SDK van het Web van dit bezit is [**geeft visuele verpersoonlijkingsbesluiten**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) controledoos binnen de &quot;[!UICONTROL Send event]&quot;actie terug.
