---
title: Bibliotheekgegevens ophalen
seo-title: Bibliotheekgegevens ophalen met Adobe Experience Platform Web SDK
description: Leer hoe u informatie ophaalt over de bibliotheek die op de website is geladen
seo-description: Leer hoe u automatisch informatie ophaalt over de bibliotheek die door de Adobe Experience Cloud SDK op de website is geladen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bèta) Bibliotheekgegevens ophalen

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Het is vaak handig om toegang te krijgen tot enkele details achter de bibliotheek die u op uw website hebt geladen. Hiervoor voert u de `getLibraryInfo` opdracht als volgt uit:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Het opgegeven `libraryInfo` object bevat momenteel de volgende eigenschappen:

* `version` Dit is de versie van de geladen bibliotheek. Als de versie van de bibliotheek die wordt geladen bijvoorbeeld 1,0,0 was, zou de waarde `1.0.0`zijn.