---
title: Typen gegevenselementen voor randextensies
description: Leer hoe u een bibliotheekmodule van het gegevenstype data-element definieert voor een tagextensie in een randeigenschap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Typen gegevenselementen in randextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een gegevenselement-type bibliotheekmodule wint een stuk gegevens terug. De moduleauteur bepaalt hoe dit stuk gegevens wordt teruggewonnen. U kunt bijvoorbeeld een gegevenselementtype gebruiken om Adobe Experience Platform-gebruikers toe te staan gegevens op te halen uit de XDM-laag of uit hun aangepaste gegevenslaag.

>[!IMPORTANT]
>
>Dit document behandelt gegevenselementen voor randuitbreidingen. Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids over [gegevens-elementtypes voor Webuitbreidingen](../web/data-element-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

Als u gebruikers wilt toestaan om een stuk gegevens van de laag van douanegegevens terug te winnen, kan uw module als dit voorbeeld kijken.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Als u de gegevens die voor de gegevenslaag worden teruggegeven configureerbaar wilt maken door de gebruiker van Adobe Experience Platform, kunt u de gebruiker toestaan om een zeer belangrijke naam in te voeren en dan de naam aan het `settings` voorwerp te bewaren. Het object zou er ongeveer zo kunnen uitzien.

```js
{
  keyName: "campaignId"
}
```

Als u wilt werken met de door de gebruiker gedefinieerde naam van het lokale opslagitem, moet u de module als volgt wijzigen:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Context van de module Bibliotheek

Alle gegevenselementmodules hebben toegang tot een `context` variabele die wordt verstrekt wanneer de module wordt geroepen. U kunt meer [hier](./context.md) leren.
