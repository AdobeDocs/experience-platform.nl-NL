---
title: Voorwaardetypen voor randextensies
description: Leer hoe u een voorwaardetype-bibliotheekmodule voor een randuitbreiding in Adobe Experience Platform definieert.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Voorwaardetypen voor randextensies

>[!NOTE]
>
> Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In een labelregel wordt een voorwaarde geëvalueerd nadat een gebeurtenis heeft plaatsgevonden. Alle voorwaarden moeten waar terugkeren opdat de regel verder verwerkt. Voorwaardetypen worden geleverd door extensies en evalueren of iets waar of onwaar is en er een booleaanse waarde wordt geretourneerd.

Een extensie kan bijvoorbeeld een voorwaardetype &#39;viewport contains&#39; weergeven waarin de gebruiker een CSS-kiezer kan opgeven. Wanneer de voorwaarde op de website van de cliënt wordt geëvalueerd, zou de uitbreiding elementen kunnen vinden die de CSS selecteur aanpassen en terugkeren of om het even welk van hen binnen viewport van de gebruiker bevat.

In dit document wordt beschreven hoe u voorwaardetypen voor een randextensie in Adobe Experience Platform definieert.

>[!IMPORTANT]
>
>Als u een webextensie ontwikkelt, raadpleegt u in plaats daarvan de handleiding over voorwaardetypen [voor webextensies](../web/condition-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in randextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

Voorwaardetypen bestaan gewoonlijk uit het volgende:

1. Een mening die binnen UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor de voorwaarde te wijzigen.
2. Een bibliotheekmodule die in de tagruntime-bibliotheek wordt uitgestraald om de instellingen te interpreteren en een voorwaarde te evalueren.

Bijvoorbeeld, als u wilt evalueren of de gebruiker op de gastheer `example.com` is, kan uw module als dit kijken.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Als u de hostnaam door de gebruiker configureerbaar wilt maken om de invoer van een hostnaam toe te staan en deze op te slaan naar het instellingenobject, ziet het object er mogelijk hetzelfde uit als dit voorbeeld.

```js
{
  "hostname": "example.com"
}
```

Om op user-defined hostname te werken, zou uw module aan dit moeten veranderen:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Voorwaarderesultaat

Het resultaat dat door een voorwaardenmodule wordt geretourneerd, kan een van de volgende zijn:

1. Een booleaanse waarde (`true` of `false`).
1. Een [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) die een booleaanse waarde retourneert zodra deze is opgelost.

## Context van de module Bibliotheek

Alle voorwaardemodules hebben toegang tot een `context` variabele die wordt verstrekt wanneer de module wordt geroepen. U kunt meer [hier](./context.md) leren.
