---
title: Typen gegevenselementen voor randextensies
description: Leer hoe u een bibliotheekmodule van het gegevenstype data-element definieert voor een tagextensie in een randeigenschap.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Typen gegevenselementen in randextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In tags zijn gegevenselementen aliassen voor gegevens op een webpagina of mobiele pagina, ongeacht de locatie van de gegevens in de gebeurtenis die de server heeft ontvangen. Een gegevenselement kan door regels worden van verwijzingen voorzien en als abstractie voor de toegang tot van deze stukken van gegevens dienst doen. Wanneer de locatie van de gegevens in de toekomst verandert (bijvoorbeeld door de gebeurtenissleutel te wijzigen die de waarde bevat), kan één gegevenselement opnieuw worden geconfigureerd, terwijl alle regels die naar dat gegevenselement verwijzen ongewijzigd kunnen blijven.

Gegevenselementen worden opgegeven door extensies en de auteur van de extensie bepaalt hoe dit gegevenselement wordt opgehaald. U kunt bijvoorbeeld een gegevenselementtype gebruiken om Adobe Experience Platform-gebruikers toe te staan gegevens op te halen uit de XDM-laag of uit hun aangepaste gegevenslaag.

In dit document wordt beschreven hoe u gegevenselemetypen definieert voor een randextensie in Adobe Experience Platform.

>[!IMPORTANT]
>
>Als u een webextensie ontwikkelt, raadpleegt u de handleiding op [gegevenselemetypen voor webextensies](../web/data-element-types.md) in plaats daarvan.
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in randextensies. Als u een inleiding nodig hebt, raadpleegt u het overzicht over [Opmaak van de module Bibliotheek](./format.md) voordat u terugkeert naar deze handleiding.

Gegevenselementen bestaan gewoonlijk uit de volgende elementen:

1. Een mening die binnen UI van het Experience Platform en UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor het gegevenselement te wijzigen.
2. Een bibliotheekmodule die in de tagruntimebibliotheek wordt uitgestraald om de instellingen te interpreteren en gegevens op te halen.

Als u gebruikers wilt toestaan om een stuk gegevens van de laag van douanegegevens terug te winnen, kan uw module als dit voorbeeld kijken.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Als u de gegevens die voor de gegevenslaag worden teruggegeven door de gebruiker van Adobe Experience Platform configureerbaar wilt maken, kunt u de gebruiker toestaan om een zeer belangrijke naam in te voeren en dan sparen de naam aan `settings` object. Het object zou er ongeveer zo kunnen uitzien.

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

Alle gegevenselementmodules hebben toegang tot een `context` variabele die wordt verstrekt wanneer de module wordt geroepen. Meer informatie [hier](./context.md).
