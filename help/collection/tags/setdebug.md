---
title: setDebug()
description: Foutopsporing op uw site inschakelen via de browserconsole.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

De `_satellite.setDebug()` methode staat u toe om [ het Zuiveren ](../use-cases/debugging.md) op uw plaats toe te laten of onbruikbaar te maken. Deze methode is bedoeld om lokaal in uw browser console te lopen; Adobe adviseert tegen het roepen van deze methode binnen markeringsregels.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: Laat [ het Zuiveren ](../use-cases/debugging.md) toe. Berichten die door de tagbibliotheek (inclusief [`_satellite.logger`](logger.md)) worden gegenereerd, zijn zichtbaar in uw browserconsole.
* **`_satellite.setDebug(false);`**: schakelt foutopsporing uit. Console-berichten die door de tagbibliotheek worden gegenereerd, zijn niet zichtbaar.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>Berichten die met JavaScript native `console.log()` zijn geschreven, zijn altijd zichtbaar voor iedereen die DevTools heeft geopend. Adobe raadt u aan [`_satellite.logger`](logger.md) waar mogelijk te gebruiken.

## persistentie van de foutopsporingsmodus

Wanneer het roepen van deze methode, zuivert wijze gebruikt het volgende werkingsgebied:

* **Browser zitting**: zuivert wijze blijft over paginaladading. Deze blijft ingeschakeld totdat u de browsersessie beëindigt of expliciet uitschakelt.
* **Oorsprong-scoped**: zuivert wijze voortduurt slechts voor de zelfde plaats (domein + haven + protocol).
* **per browser profiel**: zuivert wijze is niet dwars-profiel.

Andere vormen van [ het Zuiveren ](../use-cases/debugging.md) kunnen beïnvloeden en beschrijven zuivert wijze gebruikend de browser consolemethode.
