---
title: setDebug
description: Schakel de foutopsporingsinstelling van de Web SDK in of uit.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Met de opdracht `setDebug` kunt u de foutopsporingsmodus in de SDK van het web activeren of afsluiten. Het is één van verscheidene opties beschikbaar voor [ het zuiveren ](../use-cases/debugging.md). Adobe adviseert het toelaten van zuivert wijze binnen ontwikkelomgevingen of enkel op uw lokale machine binnen productiemilieu&#39;s.

## Foutopsporing instellen met de extensie van de Web SDK-tag

De tagextensie biedt geen mogelijkheid om foutopsporingsopties in te schakelen binnen de gebruikersinterface. U kunt de aangepaste code-editor gebruiken met de syntaxis van JavaScript of de JavaScript-code invoeren in de browserconsole terwijl u zich op uw site bevindt.

## Foutopsporing instellen met de Web SDK JavaScript-bibliotheek

Voer het `setDebug` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. De enige optie in het configuratieobject is `enabled` . Dit is een Booleaanse optie die bepaalt of de foutopsporingsmodus is ingeschakeld.

```js
alloy("setDebug", {"enabled": true});
```
