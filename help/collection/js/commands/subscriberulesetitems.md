---
title: subscribeRulesetItems
description: Abonneren op inhoudskaarten voor een specifieke oppervlakte gebruikend het subscribeRulesetItems bevel.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---

# `subscribeRulesetItems`

Met de opdracht `subscribeRulesetItems` kunt u zich abonneren op voorstellingen die het resultaat zijn van bevredigende linialen. U kunt dit doen door te specificeren op welke oppervlakken en schema&#39;s moet worden gefilterd, en een callback functie te verstrekken.

Wanneer tijdlinialen worden geëvalueerd, ontvangt de callback-functie een `result` -object met daarin een array van voorstellingen.

>[!IMPORTANT]
>
>De opdracht `subscribeRulesetItems` is de enige manier om voorstellen op te halen die afkomstig zijn van regels, aangezien deze niet worden geretourneerd naast de resultaten van [`sendEvent`](sendevent/overview.md) .


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

De bovenstaande code abonneert zich op het oppervlak van `web://example.com/#welcome` voor inhoudskaarten en gebruikt de methode `collectEvent` uit `display` om gebeurtenissen voor alle proposities uit te zenden.

## Opdrachten {#command-options}

Deze opdracht heeft een `options` -object met de volgende eigenschappen:

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| `surfaces` | Tekenreeksarray | Een lijst met oppervlakken. De callback functie zal slechts voorstellen ontvangen als zij één van de hier verstrekte oppervlakten aanpassen. |
| `schemas` | Tekenreeksarray | Een lijst met schema&#39;s. De voorstellen zullen slechts door de callback functie worden ontvangen als zij één van de hier verstrekte schema&#39;s aanpassen. |
| `callback` | Functie | Een callback-functie die wordt aangeroepen wanneer voorstellingen het resultaat zijn van bevredigende regels. De callback-functie ontvangt twee parameters wanneer deze wordt aangeroepen: `result` en `collectEvent` . Zie [ callback parameters ](#callback-parameters) voor details. |

### Callback-parameters {#callback-parameters}

De callback functie ontvangt de twee parameters die in de lijst hieronder worden beschreven wanneer aangehaald.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| `result` | Object | Dit object bevat een array `propositions` .  Deze voorstellen zijn het directe resultaat van tevreden regels. Het `result` voorwerp is gestructureerd het zelfde als het [ resultaatvoorwerp ](command-responses.md) dat door `sendEvent` gebruikend een `then` clausule is teruggekeerd. |
| `collectEvent` | Functie | Een gebruiksvriendelijke functie die u kunt gebruiken om Edge Network-gebeurtenissen te verzenden om interacties, weergaven en andere gebeurtenissen te volgen. |

### `collectEvent` functie {#collectevent-function}

De functie `collectEvent` is een handige functie waarmee u Edge Network-gebeurtenissen kunt verzenden om interacties, weergaven en andere gebeurtenissen te volgen. De twee parameters die in de onderstaande tabel worden beschreven, worden geaccepteerd.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| Het type Event | String | Een tekenreeks die aangeeft welk type propositiegebeurtenis moet worden verzonden. Ondersteunde gebeurtenistypen zijn `display` , `interact` of `dismiss` . |
| `propositions` | Array | Een array met voorstellen die overeenkomen met de gebeurtenis. |

## Abonneren op inhoudskaarten met de Web SDK-tagextensie

De Web SDK-tagextensie die gelijk is aan opdrachtreacties, is een regel die zich abonneert op de [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items) -gebeurtenis. Met deze gebeurtenis kunt u de gewenste schema&#39;s en oppervlakken opgeven.
