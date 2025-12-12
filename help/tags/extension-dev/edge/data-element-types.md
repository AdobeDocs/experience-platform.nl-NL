---
title: Gegevenstelelementtypen voor Edge-extensies
description: Leer hoe u een bibliotheekmodule van het gegevenstype data-element definieert voor een tagextensie in een randeigenschap.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Typen gegevenselementen in randextensies

In tags zijn gegevenselementen aliassen voor gegevens op een webpagina of mobiele pagina, ongeacht de locatie van de gegevens in de gebeurtenis die de server heeft ontvangen. Een gegevenselement kan door regels worden van verwijzingen voorzien en als abstractie voor de toegang tot van deze stukken van gegevens dienst doen. Wanneer de locatie van de gegevens in de toekomst verandert (bijvoorbeeld door de gebeurtenissleutel te wijzigen die de waarde bevat), kan één gegevenselement opnieuw worden geconfigureerd, terwijl alle regels die naar dat gegevenselement verwijzen ongewijzigd kunnen blijven.

Gegevenselementen worden opgegeven door extensies en de auteur van de extensie bepaalt hoe dit gegevenselement wordt opgehaald. U kunt bijvoorbeeld een gegevenselementtype gebruiken om Adobe Experience Platform-gebruikers toe te staan gegevens op te halen uit de XDM-laag of uit hun aangepaste gegevenslaag.

In dit document wordt beschreven hoe u gegevenselemetypen definieert voor een randextensie in Adobe Experience Platform.

>[!IMPORTANT]
>
>Als u een Webuitbreiding ontwikkelt, zie in plaats daarvan de gids over [ types van gegevenselement voor Webuitbreidingen ](../web/data-element-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in randextensies. Als u een inleiding vereist, zie het overzicht op [ het formatteren van de bibliotheekmodule ](./format.md) alvorens aan deze gids terug te keren.

Gegevenselementen bestaan gewoonlijk uit de volgende elementen:

1. Een mening die binnen UI van Experience Platform en UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor het gegevenselement te wijzigen.
2. Een bibliotheekmodule die in de tagruntimebibliotheek wordt uitgestraald om de instellingen te interpreteren en gegevens op te halen.

Als u gebruikers wilt toestaan om een stuk gegevens van de laag van douanegegevens terug te winnen, kan uw module als dit voorbeeld kijken.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Als u de gegevens die voor de gegevenslaag worden geretourneerd, door de Adobe Experience Platform-gebruiker configureerbaar wilt maken, kunt u de gebruiker toestaan een sleutelnaam in te voeren en de naam vervolgens op te slaan in het `settings` -object. Het object zou er ongeveer zo kunnen uitzien.

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

Alle modules van gegevenselementen hebben toegang tot een `context` variabele die wordt verstrekt wanneer de module wordt geroepen. U kunt meer [ hier ](./context.md) leren.
