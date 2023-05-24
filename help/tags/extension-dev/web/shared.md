---
title: Gedeelde Modules in webextensies
description: Leer hoe u gedeelde bibliotheekmodules voor webextensies in Adobe Experience Platform definieert.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Gedeelde modules in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een gedeelde module is een mechanisme waardoor u met andere uitbreidingen kunt communiceren. Zo kan Extension A bijvoorbeeld een stuk gegevens asynchroon laden en beschikbaar maken voor Extension B via een [beloven](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

In JavaScript-implementaties worden alle gedeelde modules geïnstantieerd met behulp van de [`getSharedModule`](../turbine.md#shared) door de `turbine` vrije variabele.

Gedeelde modules worden opgenomen in tagbibliotheken, zelfs als ze nooit worden aangeroepen vanuit andere extensies. Als u de bibliotheekgrootte niet onnodig wilt vergroten, moet u voorzichtig zijn met wat u als gedeelde module beschikbaar maakt.

Gedeelde modules hebben geen weergavecomponent.

Wanneer u uw eigen tagextensie ontwikkelt, kunt u gedeelde modules definiëren die u wilt voorzien van deze extensie. U kunt bijvoorbeeld een module maken die een gebruikers-id asynchroon laadt en vervolgens de gebruikers-id deelt met een andere extensie via een promise:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

In de [extensiemanifest](../manifest.md), moet u een naam opgeven voor deze gedeelde module. Als u deze naam geeft `user-id-promise`kan een andere extensie deze gedeelde module dan als volgt openen:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Gedeelde modules kunnen om het even wat zijn u typisch van een module CommonJS (zoals functies, voorwerpen, koorden, aantallen, of booleans) zou kunnen uitvoeren.
