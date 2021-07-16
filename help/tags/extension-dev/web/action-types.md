---
title: Typen handelingen voor webextensies
description: Leer hoe u een bibliotheekmodule van het type action definieert voor een tagextensie in een webeigenschap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Typen handelingen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een bibliotheekmodule van het handelingstype is bedoeld om een vooraf gedefinieerde handeling uit te voeren. Wat deze actie doet, is volledig aan u. Wilt u een baken verzenden, een aanbieding tonen, de gebruiker bedanken voor het bezoeken, sparen een koekje, of een steunpraatje openen?

>[!IMPORTANT]
>
>In dit document worden actietypen voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie in plaats daarvan de gids op [actietypes voor randuitbreidingen](../edge/action-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Als u het bericht bijvoorbeeld configureerbaar wilt maken voor de Adobe Experience Platform-gebruiker, kunt u de gebruiker toestaan een bericht in te voeren en op te slaan naar het instellingsobject. Het object ziet er ongeveer als volgt uit:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Om op het user-defined bericht te werken, zou uw module aan dit moeten veranderen:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Contextafhankelijke gebeurtenisgegevens

Een tweede argument zou dan aan uw module moeten worden overgegaan die de contextuele informatie over de gebeurtenis bevat die de regel in werking stelt. Het kan in bepaalde gevallen nuttig zijn en kan als volgt worden benaderd:

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
