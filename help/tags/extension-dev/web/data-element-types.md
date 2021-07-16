---
title: Typen gegevenselementen voor webextensies
description: Leer hoe u een bibliotheekmodule van het gegevenstype data-element definieert voor een tagextensie in een webeigenschap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Gegevenselementstypen voor randextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Het doel van een module van het type gegevenselement is een stuk gegevens terug te winnen. De methode voor deze herwinning is klantgericht. Met verschillende gegevenselementen kunnen Adobe Experience Platform-gebruikers gegevens ophalen van lokale opslag, een cookie of een DOM-element.

>[!IMPORTANT]
>
>Dit document bevat informatie over gegevenselemetypen voor webextensies. Als u een randuitbreiding ontwikkelt, zie in plaats daarvan de gids op [gegevens-elementtypes voor randuitbreidingen](../edge/data-element-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

Overweeg een situatie waarin u gebruikers wilt toestaan om gegevens op te halen uit een lokaal opslagitem met de naam `productName`. Uw module kan als volgt kijken:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Als u de naam van het lokale opslagitem configureerbaar wilt maken voor de Adobe Experience Platform-gebruiker, kunt u toestaan dat de gebruiker een naam invoert en de naam vervolgens opslaat in het `settings`-object. Het object kan er ongeveer als volgt uitzien:

```js
{
  itemName: "campaignId"
}
```

Als u wilt werken met de door de gebruiker gedefinieerde naam van het lokale opslagitem, moet u de module als volgt wijzigen:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Ondersteuning van standaardwaarden

Houd er rekening mee dat gebruikers de optie hebben om een standaardwaarde voor elk gegevenselement te configureren. Als de bibliotheekmodule voor gegevenselementen de waarde `undefined` of `null` retourneert, wordt deze automatisch vervangen door de standaardwaarde die de gebruiker voor het gegevenselement heeft geconfigureerd.

## Contextafhankelijke gebeurtenisgegevens

Als het gegevenselement als resultaat van een regel wordt teruggewonnen die (bijvoorbeeld, gegevenselementen worden gebruikt in de voorwaarden en de acties van de regel), zal een tweede argument worden overgegaan tot uw module die contextuele informatie betreffende de gebeurtenis bevat die de regel in brand stak. Het kan in bepaalde gevallen nuttig zijn en kan als volgt worden benaderd:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

Het object `event` moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `$type` | Een tekenreeks die de naam van de extensie en de gebeurtenis beschrijft en waaraan een punt is toegevoegd. Bijvoorbeeld, `youtube.play`. |
| `$rule` | Een object dat informatie bevat over de regel die momenteel wordt uitgevoerd. Het object moet de volgende subeigenschappen bevatten:<ul><li>`id`: De id van de regel die momenteel wordt uitgevoerd.</li><li>`name`: De naam van de regel die momenteel wordt uitgevoerd.</li></ul> |

De uitbreiding die het gebeurtenistype verstrekt dat de regel teweegbracht kan naar keuze om het even welke andere nuttige informatie aan dit `event` voorwerp toevoegen.
