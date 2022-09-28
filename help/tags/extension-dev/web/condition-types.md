---
title: Voorwaardetypen voor webextensies
description: Leer hoe u een bibliotheekmodule van het type condition definieert voor een tagextensie in een webeigenschap.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Voorwaardetypen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In de context van een regel wordt een voorwaarde geëvalueerd nadat een gebeurtenis heeft plaatsgevonden. Alle voorwaarden moeten waar terugkeren opdat de regel verder verwerkt. De uitzondering is wanneer de gebruikers uitdrukkelijk voorwaarden in een &quot;uitzondering&quot;emmer plaatsen, in welk geval alle voorwaarden binnen het emmertje vals voor de regel moeten terugkeren om verwerking voort te zetten.

Een extensie kan bijvoorbeeld een voorwaardetype &#39;viewport contains&#39; weergeven waarin de gebruiker een CSS-kiezer kan opgeven. Wanneer de voorwaarde op de website van de cliënt wordt geëvalueerd, zou de uitbreiding elementen kunnen vinden die de CSS selecteur aanpassen en terugkeren of om het even welk van hen binnen viewport van de gebruiker bevat.

In dit document wordt beschreven hoe u voorwaardetypen voor een webextensie in Adobe Experience Platform definieert.

>[!NOTE]
>
>Als u een randuitbreiding ontwikkelt, zie de gids op [voorwaardetypen voor randextensies](../edge/condition-types.md) in plaats daarvan.
>
>In dit document wordt ervan uitgegaan dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in webextensies. Als u een inleiding nodig hebt, raadpleegt u het overzicht over [Opmaak van de module Bibliotheek](./format.md) voordat u terugkeert naar deze handleiding.

Voorwaardetypen bestaan gewoonlijk uit het volgende:

1. A [weergave](./views.md) getoond binnen UI van het Experience Platform en de Inzameling UI van Gegevens die gebruikers toestaat om montages voor de voorwaarde te wijzigen.
2. Een bibliotheekmodule die in de tagruntime-bibliotheek wordt uitgestraald om de instellingen te interpreteren en een voorwaarde te evalueren.

Een voorwaardetype bibliotheekmodule heeft één doel: evalueren of iets waar of onwaar is. Wat het evalueert, is aan jou.

Als u bijvoorbeeld wilt beoordelen of de gebruiker zich op de host bevindt `example.com`, ziet uw module er mogelijk als volgt uit:

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

De `event` object moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `$type` | Een tekenreeks die de naam van de extensie en de gebeurtenis beschrijft en waaraan een punt is toegevoegd. Bijvoorbeeld, `youtube.play`. |
| `$rule` | Een object dat informatie bevat over de regel die momenteel wordt uitgevoerd. Het object moet de volgende subeigenschappen bevatten:<ul><li>`id`: De id van de regel die momenteel wordt uitgevoerd.</li><li>`name`: De naam van de regel die momenteel wordt uitgevoerd.</li></ul> |

De uitbreiding die het gebeurtenistype verstrekt dat de regel teweegbracht kan andere nuttige informatie aan dit optioneel toevoegen `event` object.
