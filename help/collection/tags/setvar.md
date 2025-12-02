---
title: setVar()
description: Stelt een waarde in die u later kunt ophalen met getVar().
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

Met de methode `_satellite.setVar()` kunt u een of meer aangepaste naam-/waardeparen instellen waarnaar later door [`_satellite.getVar()`](getvar.md) kan worden verwezen.

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Hoewel de methode `getVar()` zowel gegevenselementen als waarden kan ophalen die zijn ingesteld door `setVar()` , zijn deze twee entiteitstypen gescheiden. Als u `setVar()` gebruikt om een waarde in te stellen met dezelfde naam als een gegevenselement in de interface voor tags, wordt deze waarde niet overschreven.

## Persistentie en bereik

`setVar()` -waarden leven alleen in het paginageheugen:

* **Huidige pagina slechts**: De waarden blijven bestaan tot de pagina wordt leeggemaakt. In toepassingen van één pagina, blijven zij tot volledig herladen of u overschrijft/ontruimt hen.
* **Geen browser opslag**: Niets wordt geschreven aan koekjes, lokale opslag, of zittingsopslag.

## Verwijzen naar waarden die zijn ingesteld met `setVar()`

U kunt waarden in aangepaste code ophalen met `getVar()` :

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

U kunt ook naar deze variabelen verwijzen in de interface met tags in velden die gegevenselementnotatie ondersteunen:

```text
%Ad location%
```

>[!NOTE]
>
>Als een waarde die is ingesteld met `setVar()` dezelfde naam gebruikt als een gegevenselement en u in de gegevenselementnotatie naar die naam verwijst, heeft het gegevenselement voorrang.

## Voorbeelden

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
