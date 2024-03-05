---
title: setDebug
description: Schakel de foutopsporingsinstelling van de Web SDK in of uit.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

De `setDebug` staat u toe om het zuiveren wijze in te gaan of weg in het Web SDK. U kunt kiezen uit verschillende opties voor [foutopsporing](../use-cases/debugging.md). Adobe adviseert het toelaten van zuivert wijze binnen ontwikkelomgevingen of enkel op uw lokale machine binnen productiemilieu&#39;s.

## Foutopsporing instellen met de extensie van de Web SDK-tag

De tagextensie biedt geen mogelijkheid om foutopsporingsopties in te schakelen binnen de gebruikersinterface. U kunt de aangepaste code-editor gebruiken met behulp van JavaScript-syntaxis of de JavaScript-code invoeren in de browserconsole terwijl u zich op uw site bevindt.

## Foutopsporing instellen met de Web SDK JavaScript-bibliotheek

Voer de `setDebug` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. De enige optie in het configuratieobject is `enabled`Dit is een Booleaanse waarde die bepaalt of de foutopsporingsmodus is ingeschakeld.

```js
alloy("setDebug", {"enabled": true});
```
