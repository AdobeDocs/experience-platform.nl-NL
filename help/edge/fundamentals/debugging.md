---
title: Foutopsporing
seo-title: Foutopsporing in Adobe Experience Platform Web SDK
description: Leer hoe te om het zuiveren van SDK van het Web van het Experience Platform van een knevel te voorzien
seo-description: Leer hoe te om het zuiveren van SDK van het Web van het Experience Platform van een knevel te voorzien
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: f63c897dd1a8a8ad9ef7ac025bf05b22265ea95a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# Foutopsporing

Wanneer het zuiveren wordt toegelaten, voert SDK berichten aan de browser console uit die in het zuiveren van uw implementatie en het begrijpen van kunnen nuttig zijn hoe SDK zich gedraagt. Het zuiveren resulteert ook in een server-zijsynchrone bevestiging van de gegevens die tegen het schema worden verzameld u hebt gevormd.

Foutopsporing is standaard uitgeschakeld, maar u kunt dit op drie verschillende manieren in- en uitschakelen:

* `configure` command
* `setDebug` command
* querytekenreeks, parameter

## Foutopsporing schakelen met de opdracht Configureren

Wanneer het vormen van SDK gebruikend het `configure` bevel, laat het zuiveren door de `debugEnabled` optie aan te plaatsen toe `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Hierdoor wordt foutopsporing ingeschakeld voor alle gebruikers van de webpagina in plaats van alleen voor uw persoonlijke browser.

## Foutopsporing schakelen met de opdracht Foutopsporing

Foutopsporing als volgt in-/uitschakelen met een aparte `debug` opdracht:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Als u liever geen code op uw webpagina wijzigt of als u niet wilt dat logboekberichten voor alle gebruikers van uw website worden gemaakt, is dit vooral handig omdat u de `debug` opdracht op elk gewenst moment in de JavaScript-console van uw browser kunt uitvoeren.

## Foutopsporing in-/uitschakelen met een parameter voor een queryreeks

U kunt foutopsporing in-/uitschakelen door een parameter voor de `alloy_debug` queryreeks als volgt in te stellen `true` of `false` :

```HTTP
http://example.com/?alloy_debug=true
```

Net als bij de `debug` opdracht is dit vooral handig als u geen code op uw webpagina wilt wijzigen of als u niet wilt dat logboekberichten voor alle gebruikers van uw website worden gegenereerd. U kunt namelijk de parameter voor de queryreeks instellen wanneer u de webpagina in uw browser laadt.

## Prioriteit en duur

Wanneer het zuiveren door het `debug` bevel of de parameter van het vraagkoord wordt geplaatst, treedt het om het even welke `debug` optie met voeten die in het `configure` bevel wordt geplaatst. In deze twee gevallen blijft foutopsporing ook ingeschakeld gedurende de sessie. Met andere woorden, als u het zuiveren gebruikend zuivert bevel of de parameter van het vraagkoord toelaat, blijft het toegelaten tot één van het volgende:

* Het einde van uw sessie
* U voert het `debug` bevel in werking
* U stelt de parameter voor de queryreeks opnieuw in

## Bibliotheekgegevens ophalen

Het is vaak handig om toegang te krijgen tot enkele details achter de bibliotheek die u op uw website hebt geladen. Hiervoor voert u de `getLibraryInfo` opdracht als volgt uit:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Het opgegeven `libraryInfo` object bevat momenteel de volgende eigenschappen:

* `version` Dit is de versie van de geladen bibliotheek. Als de versie van de bibliotheek die wordt geladen bijvoorbeeld 1,0,0 was, zou de waarde `1.0.0`zijn.
