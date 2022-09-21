---
title: Typen handelingen voor webextensies
description: Leer hoe u een bibliotheekmodule van het type action definieert voor een tagextensie in een webeigenschap.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Typen handelingen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In de context van de markeringen van de gegevensinzameling, is een actie iets dat wordt uitgevoerd nadat een regelgebeurtenis is voorgekomen en alle voorwaarden evaluatie hebben overgegaan.

Een extensie kan bijvoorbeeld een actietype &#39;showsupport chat&#39; weergeven, dat een dialoogvenster voor supportchatten kan weergeven om gebruikers te helpen die problemen kunnen ondervinden bij het uitchecken.

In dit document wordt beschreven hoe u actietypen voor een webextensie in Adobe Experience Platform definieert.

>[!IMPORTANT]
>
>In dit document worden actietypen voor webextensies besproken. Als u een randuitbreiding ontwikkelt, zie de gids op [actietypen voor randextensies](../edge/action-types.md) in plaats daarvan.
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze in webextensies zijn geïntegreerd. Als u een inleiding nodig hebt, raadpleegt u het overzicht over [Opmaak van de module Bibliotheek](./format.md) voordat u terugkeert naar deze handleiding.

Handelingstypen bestaan doorgaans uit:

1. A [weergave](./views.md) getoond binnen UI van het Experience Platform en de Inzameling UI van Gegevens die gebruikers toestaat om montages voor de actie te wijzigen.
2. Een bibliotheekmodule die in de tagruntimebibliotheek wordt uitgestraald om de instellingen te interpreteren en een actie uit te voeren.

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

De `event` object moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `$type` | Een tekenreeks die de naam van de extensie en de gebeurtenis beschrijft en waaraan een punt is toegevoegd. Bijvoorbeeld, `youtube.play`. |
| `$rule` | Een object dat informatie bevat over de regel die momenteel wordt uitgevoerd. Het object moet de volgende subeigenschappen bevatten:<ul><li>`id`: De id van de regel die momenteel wordt uitgevoerd.</li><li>`name`: De naam van de regel die momenteel wordt uitgevoerd.</li></ul> |

De uitbreiding die het gebeurtenistype verstrekt dat de regel teweegbracht kan andere nuttige informatie aan dit optioneel toevoegen `event` object.
