---
title: Gedeelde Modules in webextensies
description: Leer hoe u gedeelde bibliotheekmodules voor webextensies in Adobe Experience Platform definieert.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Gedeelde modules in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een gedeelde module is een mechanisme waardoor u met andere uitbreidingen kunt communiceren. In implementaties JavaScript, worden alle gedeelde modules geconcretiseerd gebruikend de [`getSharedModule`](../turbine.md#shared) methode die door de `turbine` vrije variabele wordt verstrekt.

Wanneer u uw eigen tagextensie ontwikkelt, kunt u gedeelde modules definiëren die u wilt voorzien van deze extensie. U kunt bijvoorbeeld een module maken die een gebruikers-id asynchroon laadt en vervolgens de gebruikers-id deelt met een andere extensie via een [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise):

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

In [extension manifest](../manifest.md) moet u een naam voor deze gedeelde module verstrekken. Als u het `user-id-promise` noemt, kon een verschillende uitbreiding tot deze gedeelde module dan als volgt toegang hebben:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Gedeelde modules kunnen om het even wat zijn u typisch van een module CommonJS (zoals functies, voorwerpen, koorden, aantallen, of booleans) zou kunnen uitvoeren.
