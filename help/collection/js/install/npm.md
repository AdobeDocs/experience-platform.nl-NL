---
title: De Web SDK installeren met het NPM-pakket
description: Gebruik een NPM-pakket om de Web SDK-bibliotheek te installeren en ernaar te verwijzen.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: b1574940b3afbd98cd60a079fdf7b10153e8e9d7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# De Web SDK installeren met het NPM-pakket

SDK van het Web van Adobe Experience Platform is beschikbaar als [ NPM pakket ](https://www.npmjs.com). Door het NPM-pakket te installeren, hebt u controle over het constructieproces voor de Adobe Experience Platform Web SDK JavaScript-bibliotheek. Het NPM-pakket stelt EcmaScript versie 5-modules of EcmaScript versie 2015 (ES6)-modules beschikbaar die in de browser moeten worden uitgevoerd.

```bash
npm install @adobe/alloy
```

Het NPM-pakket van de Adobe Experience Platform Web SDK stelt een `createInstance` functie beschikbaar. De naamoptie die aan de functie wordt doorgegeven, bepaalt het voorvoegsel dat wordt gebruikt bij het vastleggen. Hieronder staan voorbeelden van het gebruik van het pakket.

## Het pakket gebruiken als een ECMAScript 2015 (ES6)-module

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Het pakket NPM baseert zich op modules CommonJS; daarom, wanneer het gebruiken van een bundelaar, zorg ervoor dat de bundelaar modules CommonJS steunt. Sommige bundels, zoals [ Rollup ](https://rollupjs.org), vereisen a [ stop ](https://www.npmjs.com/package/@rollup/plugin-commonjs) die steun CommonJS verleent.

## Het pakket gebruiken als een ECMAScript 5-module

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```
