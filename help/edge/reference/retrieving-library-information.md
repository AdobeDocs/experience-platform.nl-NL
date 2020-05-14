---
title: Bibliotheekgegevens ophalen
seo-title: Bibliotheekgegevens ophalen met Adobe Experience Platform Web SDK
description: Leer hoe u informatie ophaalt over de bibliotheek die op de website is geladen
seo-description: Leer hoe u automatisch informatie ophaalt over de bibliotheek die door de Adobe Experience Cloud SDK op de website is geladen
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Bibliotheekgegevens ophalen

Het is vaak handig om toegang te krijgen tot enkele details achter de bibliotheek die u op uw website hebt geladen. Hiervoor voert u de `getLibraryInfo` opdracht als volgt uit:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Het opgegeven `libraryInfo` object bevat momenteel de volgende eigenschappen:

* `version` Dit is de versie van de geladen bibliotheek. Als de versie van de bibliotheek die wordt geladen bijvoorbeeld 1,0,0 was, zou de waarde `1.0.0`zijn.