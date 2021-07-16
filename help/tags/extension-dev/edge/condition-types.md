---
title: Voorwaardetypen voor randextensies
description: Leer hoe u een voorwaardetype-bibliotheekmodule voor een randuitbreiding in Adobe Experience Platform definieert.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Voorwaardetypen voor randextensies

>[!NOTE]
>
> Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een voorwaardetype bibliotheekmodule evalueert of iets waar of vals is en keert een booleaanse waarde terug.

>[!IMPORTANT]
>
>Dit document behandelt voorwaardetypen voor randuitbreidingen. Als u een webextensie ontwikkelt, raadpleegt u in plaats daarvan de handleiding over voorwaardetypen [voor webextensies](../web/condition-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

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
