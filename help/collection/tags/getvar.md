---
title: getVar()
description: Retourneert een waarde van een data-element of een waarde die is ingesteld met setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# `getVar()`

De `_satellite.getVar()` methode keert de huidige waarde van het element van a [&#x200B; Gegevens &#x200B;](/help/tags/ui/managing-resources/data-elements.md) of een waarde terug die [`_satellite.setVar()`](setvar.md) wordt geplaatst. Als een gegevenselement en een `setVar()` -waarde dezelfde naam hebben, heeft het gegevenselement voorrang. Wanneer u een tekenreeks-id aanroept die nog niet bestaat, retourneert de methode `undefined` . De evaluatie is synchroon.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

De geretourneerde waarde en het type zijn afhankelijk van het type gegevenselement waarnaar u verwijst. Als u bijvoorbeeld `getVar()` aanroept waarmee een tekenreeksvariabele wordt opgehaald, wordt het type geretourneerd `string` . Als u `getVar()` aanroept die een veranderlijk gegevenselement van het Web SDK terugkeert, dan is het teruggekeerde type een `object` die alle eigenschappen bevat die in die variabele worden geplaatst.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Beschikbare velden

De methode `getVar()` ondersteunt twee argumenten. In de meeste gevallen is het tweede optionele argument niet opgenomen.

| Naam | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| **`name`** | `string` | Ja | De naam van het gegevenselement dat u wilt ophalen. Namen van gegevenselementen zijn hoofdlettergevoelig. |
| **`event`** | `object` | Nee | Gebeurteniscontext van de activeringsregel. Slechts gebruikt in geavanceerde gebruiksgevallen door gegevenselementen die [&#x200B; douanecode &#x200B;](/help/tags/ui/managing-resources/data-elements.md#custom-code) gebruiken of douaneversies. Wanneer een regel wordt geactiveerd door een gebeurtenis (zoals een klik, het verzenden van een formulier of een aangepaste JavaScript-verzending), wordt het bijbehorende gebeurtenisobject hier opgenomen. Gegevenselementen kunnen deze informatie gebruiken om contextafhankelijke waarden te retourneren, zoals de details van het aangeklikte element of eigenschappen van een aangepaste gebeurtenis. |
