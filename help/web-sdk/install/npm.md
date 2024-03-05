---
title: De SDK van het web installeren met behulp van het NPM-pakket
description: Gebruik een NPM-pakket om de Web SDK-bibliotheek te installeren en ernaar te verwijzen.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# De SDK van het web installeren met behulp van het NPM-pakket

Adobe Experience Platform Web SDK is beschikbaar als een [NPM-pakket](https://www.npmjs.com). Door het NPM-pakket te installeren, hebt u controle over het ontwikkelproces voor de JavaScript-bibliotheek van Adobe Experience Platform Web SDK. Het NPM-pakket stelt EcmaScript versie 5-modules of EcmaScript versie 2015 (ES6)-modules beschikbaar die in de browser moeten worden uitgevoerd.

```bash
npm install @adobe/alloy
```

Het NPM-pakket van de Adobe Experience Platform Web SDK stelt een `createInstance` functie. De naamoptie die aan de functie wordt doorgegeven, bepaalt het voorvoegsel dat wordt gebruikt bij het vastleggen. Hieronder staan voorbeelden van het gebruik van het pakket.

## Het pakket gebruiken als een ECMAScript 2015 (ES6)-module

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Het pakket NPM baseert zich op modules CommonJS; daarom, wanneer het gebruiken van een bundelaar, zorg ervoor dat de bundelaar modules CommonJS steunt. Sommige bundels, zoals [Rollup](https://rollupjs.org)vereist een [insteekmodule](https://www.npmjs.com/package/@rollup/plugin-commonjs) die ondersteuning biedt voor CommonJS.

## Het pakket gebruiken als een ECMAScript 5-module

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
