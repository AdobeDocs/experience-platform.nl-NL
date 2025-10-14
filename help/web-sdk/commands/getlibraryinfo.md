---
title: getLibraryInfo
description: Haal informatie rond de huidige de bibliotheekversie van SDK van het Web op.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

De opdracht `getLibraryInfo` biedt u informatie over de versie van de Web SDK-bibliotheek die momenteel wordt gebruikt. U kunt dit bevel gebruiken om te volgen welke versies van het Web SDK die u aan verschillende Web-eigenschappen opstelt.

## Bibliotheekinformatie met de webSDK-tagextensie

De markeringsuitbreiding verstrekt geen interface om dit bevel te verzenden. Gebruik de aangepaste code-editor volgens de syntaxis van de JavaScript-bibliotheek.

Als u deze opdracht uitvoert met de tagextensie, worden zowel de versie van de tagextensie als de versie van de bibliotheek opgenomen, samengevoegd met een `+` -symbool. De bibliotheekversie van SDK van het Web wordt eerst vermeld, die door de versie van de markeringsuitbreiding wordt gevolgd.

## Bibliotheekinformatie met de Web SDK JavaScript-bibliotheek

Voer het `getLibraryInfo` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Deze opdracht wordt meestal gecombineerd met een JavaScript-belofte waarmee u de objecten die erin worden gevuld, kunt ophalen.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Object Response

Als u besluit om [&#x200B; reacties &#x200B;](command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`libraryInfo.commands`**: Een array met opdrachten die door deze versie van de Web SDK worden ondersteund.
* **`libraryInfo.configs`**: Een array met configuratie-instellingen die door deze versie van de Web SDK wordt ondersteund.
* **`libraryInfo.version`**: De versie van de Web SDK-bibliotheek.
