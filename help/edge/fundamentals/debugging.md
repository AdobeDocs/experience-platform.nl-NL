---
title: Foutopsporing in de SDK van Adobe Experience Platform Web
description: Leer hoe te om het zuiveren mogelijkheden in de SDK van het Web van het Experience Platform van een knevel te voorzien.
keywords: foutopsporing in de web-SDK;foutopsporing;configureren;configureren, opdracht;foutopsporing, opdracht;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Foutopsporing

Wanneer het zuiveren wordt toegelaten, voert SDK berichten aan de browser console uit die in het zuiveren van uw implementatie en het begrijpen van kunnen nuttig zijn hoe SDK zich gedraagt.

Foutopsporing is standaard uitgeschakeld, maar u kunt deze op vier verschillende manieren in- en uitschakelen:

* `configure` command
* `setDebug` command
* querytekenreeks, parameter
* Foutopsporing inschakelen in Adobe Experience Platform Debugger inschakelen in-/uitschakelen. Adobe Experience Platform is een krachtig hulpmiddel waarmee u uw webpagina&#39;s kunt controleren en waarmee u problemen met de implementatie van uw Experience Cloud-producten kunt opsporen. Adobe Experience Platform Debugger is beschikbaar als beide [Chroom](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) en [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-experience-platform-dbg/) extensie. Foutopsporing kan worden ingeschakeld op het tabblad Configuratie van de sectie AEP Web SDK.

![](../assets/enable-debugging.png)

## Foutopsporing schakelen met de opdracht Configureren

Bij het configureren van de SDK wordt de `configure` bevel, laat het zuiveren door te plaatsen toe `debugEnabled` optie voor `true`.

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

Foutopsporing in-/uitschakelen met een aparte `debug` als volgt:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Als u liever geen code op uw webpagina wijzigt of als u niet wilt dat logboekberichten voor alle gebruikers van uw website worden geproduceerd, is dit vooral handig omdat u de optie `debug` in de JavaScript-console van uw browser.

## Foutopsporing in-/uitschakelen met een parameter voor een queryreeks

Foutopsporing in-/uitschakelen door een `alloy_debug` querytekenreeks-parameter voor `true` of `false` als volgt:

```HTTP
http://example.com/?alloy_debug=true
```

Vergelijkbaar met de `debug` als u liever geen code op uw webpagina wijzigt of als u niet wilt dat logboekberichten voor alle gebruikers van uw website worden gemaakt, is dit vooral handig omdat u de parameter van de queryreeks kunt instellen wanneer u de webpagina in uw browser laadt.

## Prioriteit en duur

Wanneer foutopsporing wordt ingesteld via de `debug` opdracht of querytekenreeks, overschrijft deze elke `debug` in het dialoogvenster `configure` gebruiken. In deze twee gevallen blijft foutopsporing ook ingeschakeld gedurende de sessie. Met andere woorden, als u het zuiveren gebruikend zuivert bevel of de parameter van het vraagkoord toelaat, blijft het toegelaten tot één van het volgende:

* Het einde van uw sessie
* U voert de `debug` command
* U stelt de parameter voor de queryreeks opnieuw in

## Bibliotheekgegevens ophalen

Het is vaak handig om toegang te krijgen tot enkele details achter de bibliotheek die u op uw website hebt geladen. Om dit te doen, voer uit `getLibraryInfo` als volgt:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Momenteel worden `libraryInfo` object bevat de volgende eigenschappen:

* `version`: Dit is de versie van de geladen bibliotheek. Als de versie van de bibliotheek die wordt geladen bijvoorbeeld 1,0,0 was, zou de waarde `1.0.0`. Wanneer de bibliotheek wordt uitgevoerd binnen de tagextensie (genaamd &quot;AEP Web SDK&quot;), is de versie de bibliotheekversie en wordt de versie van de tagextensie gekoppeld aan een plusteken (+). Als de versie van de bibliotheek bijvoorbeeld 1.0.0 was en de versie van de tagextensie 1.2.0, zou de waarde `1.0.0+1.2.0`.
* `commands`: Dit zijn alle beschikbare opdrachten die door de geladen bibliotheek worden ondersteund.
* `configs`: Dit zijn alle huidige configuraties in de geladen bibliotheek.
