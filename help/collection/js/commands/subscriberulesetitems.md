---
title: subscribeRulesetItems
description: Abonneren op inhoudskaarten voor een specifieke oppervlakte gebruikend het subscribeRulesetItems bevel.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: 3ecfc2258e63a34a739ab8b296437c357d1dd9d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# `subscribeRulesetItems`

Met de opdracht `subscribeRulesetItems` kunt u zich abonneren op voorstellingen die het resultaat zijn van bevredigende linialen. U kunt dit doen door te specificeren op welke oppervlakken en schema&#39;s moet worden gefilterd, en een callback functie te verstrekken.

Regels worden elke keer geëvalueerd wanneer een opdracht [`sendEvent`](sendevent/overview.md) wordt verzonden. De callback-functie ontvangt een `result` -object met daarin een array van voorstellingen.

>[!IMPORTANT]
>
>De opdracht `subscribeRulesetItems` is de enige manier om voorstellen op te halen die afkomstig zijn van regels, aangezien deze niet worden geretourneerd naast de resultaten van [`sendEvent`](sendevent/overview.md) . U moet uw abonnement instellen voordat u `sendEvent` aanroept om ervoor te zorgen dat de voorstellingen worden vastgelegd.


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

## Opdrachtopties {#command-options}

Deze opdracht heeft een `options` -object met de volgende eigenschappen:

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| `surfaces` | Tekenreeksarray | Een lijst met oppervlakken. De callback functie zal slechts voorstellen ontvangen als zij één van de hier verstrekte oppervlakten aanpassen. |
| `schemas` | Tekenreeksarray | Een lijst met schema&#39;s. De voorstellen zullen slechts door de callback functie worden ontvangen als zij één van de hier verstrekte schema&#39;s aanpassen. |
| `callback` | Functie | Een callback-functie die wordt aangeroepen wanneer proposities het resultaat zijn van bevredigende linialen. De callback-functie ontvangt twee parameters wanneer deze wordt aangeroepen: `result` en `collectEvent` . Zie [&#x200B; callback parameters &#x200B;](#callback-parameters) voor details. |

>[!TIP]
>
>U kunt zich in één opdracht abonneren op meerdere oppervlakken en schema&#39;s door extra waarden door te geven aan de arrays `surfaces` en `schemas` .

### Callback-parameters {#callback-parameters}

De callback functie ontvangt de twee parameters die in de lijst hieronder worden beschreven wanneer aangehaald.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| `result` | Object | Dit object bevat een array `propositions` .  Deze voorstellen zijn het directe resultaat van tevreden regels. Het `result` voorwerp is gestructureerd het zelfde als het [&#x200B; resultaatvoorwerp &#x200B;](command-responses.md) dat door `sendEvent` gebruikend een `then` clausule is teruggekeerd. |
| `collectEvent` | Functie | Een gebruiksvriendelijke functie die u kunt gebruiken om Edge Network-gebeurtenissen te verzenden om interacties, weergaven en andere gebeurtenissen te volgen. |

### `collectEvent` functie {#collectevent-function}

De functie `collectEvent` is een handige functie die u kunt gebruiken om Edge Network-gebeurtenissen te verzenden om interacties, weergaven en andere gebeurtenissen te volgen. De twee parameters die in de onderstaande tabel worden beschreven, worden geaccepteerd.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| Het type Event | String | Een tekenreeks die aangeeft welk type propositiegebeurtenis moet worden verzonden. Ondersteunde gebeurtenistypen zijn `display` , `interact` of `dismiss` . |
| `propositions` | Array | Een array met voorstellen die overeenkomen met de gebeurtenis. |


De functie `collectEvent` kan onafhankelijk buiten de callback worden geroepen. Het aanroepen van deze functie is handig wanneer u een interactie of ontslag op een later moment bijhoudt, bijvoorbeeld als reactie op een actie van de gebruiker.

```js
collectEvent("interact", propositions);
```

## Abonneren op inhoudskaarten met de Web SDK-tagextensie

De Web SDK-tagextensie die gelijk is aan opdrachtreacties, is een regel die zich abonneert op de [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items) -gebeurtenis. Met deze gebeurtenis kunt u de gewenste schema&#39;s en oppervlakken opgeven.
