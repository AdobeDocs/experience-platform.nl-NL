---
title: Typen gegevenselementen voor webextensies
description: Leer hoe u een bibliotheekmodule van het gegevenstype data-element definieert voor een tagextensie in een webeigenschap.
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Gegevenselementstypen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In gegevensverzamelingstags zijn gegevenselementen in feite aliassen van gegevens op een pagina. Deze gegevens zijn te vinden in parameters van queryreeksen, cookies, DOM-elementen of andere locaties. Een gegevenselement kan door regels worden van verwijzingen voorzien en als abstractie voor de toegang tot van deze stukken van gegevens dienst doen.

Gegevenselementen worden verstrekt door uitbreidingen, en laten gebruikers toe om gegevenselementen te vormen om tot stukken van gegevens op een bepaalde manier toegang te hebben. Een extensie kan bijvoorbeeld een gegevenstype ‘lokaal opslagitem’ leveren waarin de gebruiker een naam voor een lokaal opslagitem kan opgeven. Wanneer het gegevenselement door een regel van verwijzingen wordt voorzien, zou de uitbreiding de waarde van het lokale opslagpunt kunnen omhoog kijken door de lokale naam van het opslagpunt te gebruiken die de gebruiker had verstrekt toen het vormen van het gegevenselement.

In dit document wordt beschreven hoe u gegevenselematypen voor een webextensie in Adobe Experience Platform definieert.

>[!IMPORTANT]
>
>Als u een randuitbreiding ontwikkelt, zie de gids op [gegevenselemetypen voor randextensies](../edge/data-element-types.md) in plaats daarvan.
>
>In dit document wordt ook aangenomen dat u bekend bent met bibliotheekmodules en hoe deze in webextensies zijn geïntegreerd. Als u een inleiding nodig hebt, raadpleegt u het overzicht over [Opmaak van de module Bibliotheek](./format.md) voordat u terugkeert naar deze handleiding.

Gegevenselementen bestaan gewoonlijk uit de volgende elementen:

1. A [weergave](./views.md) getoond binnen UI van het Experience Platform en de Inzameling UI van Gegevens die gebruikers toestaat om montages voor het gegevenselement te wijzigen.
2. Een bibliotheekmodule die in de tagruntimebibliotheek wordt uitgestraald om de instellingen te interpreteren en gegevens op te halen.

Overweeg een situatie waarin u gebruikers wilt toestaan om gegevens op te halen uit een lokaal opslagitem met de naam `productName`. Uw module kan als volgt kijken:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Als u de naam van het lokale opslagitem configureerbaar wilt maken voor de Adobe Experience Platform-gebruiker, kunt u toestaan dat de gebruiker een naam invoert en de naam vervolgens in de `settings` object. Het object kan er ongeveer als volgt uitzien:

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

Houd er rekening mee dat gebruikers de optie hebben om een standaardwaarde voor elk gegevenselement te configureren. Als de bibliotheekmodule voor gegevenselementen een waarde retourneert van `undefined` of `null`, wordt deze automatisch vervangen door de standaardwaarde die de gebruiker voor het gegevenselement heeft geconfigureerd.

## Contextafhankelijke gebeurtenisgegevens

Als het gegevenselement als resultaat van een regel wordt teruggewonnen die (bijvoorbeeld, gegevenselementen worden gebruikt in de voorwaarden en de acties van de regel), zal een tweede argument worden overgegaan tot uw module die contextuele informatie betreffende de gebeurtenis bevat die de regel in brand stak. Het kan in bepaalde gevallen nuttig zijn en kan als volgt worden benaderd:

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
