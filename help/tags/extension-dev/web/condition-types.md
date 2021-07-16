---
title: Voorwaardetypen voor webextensies
description: Leer hoe u een bibliotheekmodule van het type condition definieert voor een tagextensie in een webeigenschap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Voorwaardetypen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een module van het voorwaardetype bibliotheek heeft één doel: evalueren of iets waar of onwaar is. Wat het evalueert, is aan jou.

>[!NOTE]
>
>In dit document worden voorwaardetypen voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie in plaats daarvan de gids op [voorwaardetypes voor randuitbreidingen](../edge/condition-types.md).
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze worden geïntegreerd in tagextensies. Als u een inleiding vereist, zie het overzicht op [bibliotheekmodule formatteren](./format.md) alvorens aan deze gids terug te keren.

Bijvoorbeeld, als u wilde evalueren of de gebruiker op de gastheer `example.com` is, kan uw module als dit kijken:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Nu, overweeg een situatie waarin u hostname door de gebruiker van Adobe Experience Platform configureerbaar wilt maken. U kunt toestaan dat de gebruiker een hostnaam invoert en vervolgens de hostnaam in het instellingenobject opslaat. Het object kan er ongeveer als volgt uitzien:

```js
{
  "hostname": "example.com"
}
```

Om op user-defined hostname te werken, zou uw module aan dit moeten veranderen:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Contextafhankelijke gebeurtenisgegevens

Een tweede argument wordt overgegaan tot uw module die contextafhankelijke informatie betreffende de gebeurtenis bevat die de regel in werking stelde. Het kan in bepaalde gevallen nuttig zijn en kan als volgt worden benaderd:

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
