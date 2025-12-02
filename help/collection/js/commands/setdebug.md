---
title: setDebug
description: Schakel de foutopsporingsinstelling voor Web SDK in of uit.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

Met de opdracht `setDebug` kunt u de foutopsporingsmodus in Web SDK in- of uitschakelen. Het is één van verscheidene opties beschikbaar voor [&#x200B; het zuiveren &#x200B;](../../use-cases/debugging.md). Adobe raadt u aan de foutopsporingsmodus in ontwikkelomgevingen of alleen op uw lokale computer in productieomgevingen in te schakelen.

Voer het `setDebug` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. De enige optie in het configuratieobject is `enabled` . Dit is een Booleaanse optie die bepaalt of de foutopsporingsmodus is ingeschakeld.

```js
alloy("setDebug", {"enabled": true});
```

## Foutopsporing instellen met de webtagextensie SDK

Roep [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) aan in de browserconsole op een pagina waarop een tagbibliotheek is geïmplementeerd. De Web SDK-tagextensie biedt niet de mogelijkheid om foutopsporingsopties in te schakelen binnen de gebruikersinterface van de tags zelf.
