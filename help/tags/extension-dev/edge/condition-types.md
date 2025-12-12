---
title: Voorwaardetypen voor Edge-extensies
description: Leer hoe u een voorwaardetype-bibliotheekmodule voor een randuitbreiding in Adobe Experience Platform definieert.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Type voorwaarde voor randextensies

In een labelregel wordt een voorwaarde geëvalueerd nadat een gebeurtenis heeft plaatsgevonden. Alle voorwaarden moeten waar terugkeren opdat de regel verder verwerkt. Voorwaardetypen worden geleverd door extensies en evalueren of iets waar of onwaar is en een booleaanse waarde retourneert.

Een extensie kan bijvoorbeeld een voorwaardetype &#39;viewport contains&#39; weergeven waarin de gebruiker een CSS-kiezer kan opgeven. Wanneer de voorwaarde op de website van de cliënt wordt geëvalueerd, zou de uitbreiding elementen kunnen vinden die de CSS selecteur aanpassen en terugkeren of om het even welk van hen binnen viewport van de gebruiker bevat.

In dit document wordt beschreven hoe u voorwaardetypen voor een randextensie in Adobe Experience Platform definieert.

>[!IMPORTANT]
>
>Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids op [&#x200B; voorwaardetypen voor Webuitbreidingen &#x200B;](../web/condition-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in randextensies. Als u een inleiding vereist, zie het overzicht op [&#x200B; het formatteren van de bibliotheekmodule &#x200B;](./format.md) alvorens aan deze gids terug te keren.

Voorwaardetypen bestaan gewoonlijk uit het volgende:

1. Een weergave die wordt weergegeven in de gebruikersinterface van Experience Platform en de gebruikersinterface voor gegevensverzameling waarmee gebruikers instellingen voor de voorwaarde kunnen wijzigen.
2. Een bibliotheekmodule die in de tagruntime-bibliotheek wordt uitgestraald om de instellingen te interpreteren en een voorwaarde te evalueren.

Als u bijvoorbeeld wilt beoordelen of de gebruiker zich op de host bevindt `example.com` , ziet uw module er mogelijk als volgt uit.

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
1. A [&#x200B; belofte &#x200B;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) die een booleaanse waarde eens terugkeert opgelost.

## Context van de module Bibliotheek

Alle voorwaardemodules hebben toegang tot een variabele `context` die wordt verstrekt wanneer de module wordt geroepen. U kunt meer [&#x200B; hier &#x200B;](./context.md) leren.
