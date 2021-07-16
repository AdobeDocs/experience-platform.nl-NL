---
title: Typen handelingen voor randextensies
description: Leer hoe u een bibliotheekmodule van het type action definieert voor een tagextensie in een randeigenschap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Typen handelingen voor randextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een actie-type bibliotheekmodule wordt ontworpen om een vooraf bepaalde actie te nemen. Het effect van deze handeling wordt volledig gedefinieerd door de auteur. De module zou als baken kunnen worden gecreeerd of zelfs sommige gegevens van de gebeurtenis transformeren.

>[!IMPORTANT]
>
>Dit document behandelt actietypen voor randuitbreidingen. Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids over [actietypes voor Webuitbreidingen](../web/action-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

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

Het resultaat dat door een actiemodule wordt geretourneerd, kan om het even welk zijn. Als de actie een asynchrone taak moet uitvoeren, kunt u [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) terugkeren die het resultaat terugkeert u wilt zodra het oplost.

Het actieresultaat wordt opgeslagen in een `ruleStash` sleutel die aan alle modules door de `context` parameter (`context.arc.ruleStash`) ter beschikking wordt gesteld. U kunt meer over `ruleStash` [hier](./context.md#rulestash) leren.
