---
title: Typen handelingen voor Edge-extensies
description: Leer hoe u een bibliotheekmodule van het type action definieert voor een tagextensie in een randeigenschap.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Typen handelingen voor randextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

In een markeringsregel, is een actie iets dat wordt uitgevoerd nadat de regelvoorwaarden evaluatie hebben overgegaan. Actietypen worden geleverd door extensies en de effecten ervan worden volledig gedefinieerd door de auteur van de extensie.

Een extensie kan bijvoorbeeld een actietype &#39;showsupport chat&#39; weergeven, dat een dialoogvenster voor supportchatten kan weergeven om gebruikers te helpen die problemen kunnen ondervinden bij het uitchecken.

In dit document wordt beschreven hoe u actietypen voor een randextensie in Adobe Experience Platform definieert.

>[!IMPORTANT]
>
>Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids op [ actietypen voor Webuitbreidingen ](../web/action-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in randextensies. Als u een inleiding vereist, zie het overzicht op [ het formatteren van de bibliotheekmodule ](./format.md) alvorens aan deze gids terug te keren.

Handelingstypen bestaan doorgaans uit:

1. Een mening die binnen UI van het Experience Platform en UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor de actie te wijzigen.
2. Een bibliotheekmodule die in de tagruntimebibliotheek wordt uitgestraald om de instellingen te interpreteren en een actie uit te voeren.

Bijvoorbeeld, kan een module om sommige gegevens aan een derdeeindpunt door:sturen als dit kijken.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Als u het eindpunt door de gebruiker configureerbaar wilt maken, en de input en persistentie van een eindpunt aan het montagesobject binnen de module toestaan, zou het voorwerp gelijkaardig aan dit kijken.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Om op het user-defined eindpunt te werken, zou uw module in het volgende voorbeeld moeten veranderen.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Handelingsresultaat

Het resultaat dat door een actiemodule wordt geretourneerd, kan om het even welk zijn. Als de actie een asynchrone taak moet uitvoeren, kunt u a [ belofte ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) terugkeren die het resultaat terugkeert u wilt zodra het oplost.

Het resultaat van de handeling wordt opgeslagen in een `ruleStash` -toets die via de `context` -parameter (`context.arc.ruleStash` ) beschikbaar wordt gemaakt voor alle modules. U kunt meer over `ruleStash` [ hier ](./context.md#rulestash) leren.
