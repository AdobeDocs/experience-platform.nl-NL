---
title: getLibraryInfo
description: Haal informatie rond de huidige de bibliotheekversie van SDK van het Web op.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

De `getLibraryInfo` bevel voorziet u van informatie rond de versie van de bibliotheek van SDK van het Web momenteel gebruikt. U kunt dit bevel gebruiken om te volgen welke versies van het Web SDK die u aan verschillende Web-eigenschappen opstelt.

## Bibliotheekinformatie met de webSDK-tagextensie

De markeringsuitbreiding verstrekt geen interface om dit bevel te verzenden. Gebruik de aangepaste code-editor die de syntaxis van de JavaScript-bibliotheek volgt.

Als u deze opdracht uitvoert met de tagextensie, worden zowel de versie van de tagextensie als de versie van de bibliotheek opgenomen, samengevoegd met een `+` symbool. De bibliotheekversie van SDK van het Web wordt eerst vermeld, die door de versie van de markeringsuitbreiding wordt gevolgd.

## Bibliotheekinformatie met de Web SDK JavaScript-bibliotheek

Voer de `getLibraryInfo` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. Deze opdracht wordt meestal gekoppeld aan een JavaScript-belofte waarmee u de objecten die erin worden gevuld, kunt ophalen.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Object Response

Als u besluit [reacties verwerken](command-responses.md) met deze opdracht zijn de volgende eigenschappen beschikbaar in het reactieobject:

* **`libraryInfo.commands`**: Een array met opdrachten die door deze versie van de SDK van het web worden ondersteund.
* **`libraryInfo.configs`**: Een array met configuratie-instellingen die door deze versie van de SDK van het web wordt ondersteund.
* **`libraryInfo.version`**: De versie van de Web SDK-bibliotheek.
