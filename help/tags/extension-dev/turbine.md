---
title: Variabele turbinevrij
description: Leer meer over het turbineobject, een gratis variabele die specifieke informatie en hulpprogramma's voor de Adobe Experience Platform-tagruntime biedt.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Variabele zonder turbinemotor

Het `turbine` -object is een &#39;vrije variabele&#39; binnen het bereik van de bibliotheekmodules van uw extensie. Deze biedt informatie en hulpprogramma&#39;s die specifiek zijn voor de Adobe Experience Platform-tagruntime en is altijd beschikbaar voor bibliotheekmodules zonder `require()` te gebruiken.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` is een object dat constructiegegevens bevat over de huidige tagruntimebibliotheek.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `turbineVersion` | De [ Turbine ](https://www.npmjs.com/package/@adobe/reactor-turbine) versie die binnen de huidige bibliotheek wordt gebruikt. |
| `turbineBuildDate` | ISO 8601 datum toen de versie van [ Turbine ](https://www.npmjs.com/package/@adobe/reactor-turbine) binnen de container werd gebruikt werd gebouwd. |
| `buildDate` | De ISO 8601-datum waarop de huidige bibliotheek is gemaakt. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` is een object dat informatie bevat over de omgeving waarin de bibliotheek wordt geïmplementeerd.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de omgeving. |
| `stage` | De omgeving waarvoor deze bibliotheek is gemaakt. Mogelijke waarden zijn `development` , `staging` en `production` . |

{style="table-layout:auto"}

## `debugEnabled`

Een booleaanse waarde die aangeeft of foutopsporing voor tags momenteel is ingeschakeld.

Als u eenvoudig probeert om berichten te registreren, is het onwaarschijnlijk u dit zult moeten gebruiken. Meld in plaats daarvan altijd berichten met `turbine.logger` om ervoor te zorgen dat uw berichten alleen naar de console worden afgedrukt wanneer foutopsporing voor tags is ingeschakeld.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Retourneert de waarde van een gegevenselement.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Keert het montagesobject terug dat het laatst van de [ mening van de uitbreidingsconfiguratie ](./configuration.md) werd bewaard.

Waarden binnen de geretourneerde instellingen komen mogelijk uit gegevenselementen. Daarom kan het aanroepen van `getExtensionSettings()` op verschillende momenten verschillende resultaten opleveren als de waarden van de gegevenselementen zijn gewijzigd. Als u de meest actuele waarden wilt ophalen, moet u zo lang mogelijk wachten voordat u `getExtensionSettings()` aanroept.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

Het [ hostedLibFiles ](./manifest.md) bezit kan binnen uitbreidingsmanifest worden bepaald om diverse dossiers samen met de markering runtime bibliotheek te ontvangen. Deze module retourneert de URL waar het opgegeven bibliotheekbestand wordt gehost.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Hiermee wordt een module opgehaald die via een andere extensie is gedeeld. Als er geen overeenkomende module wordt gevonden, wordt `undefined` geretourneerd. Zie [ het Uitvoeren Gedeelde Modules ](./web/shared.md) voor meer informatie betreffende gedeelde modules.

## `logger`

```js
turbine.logger.error('Error!');
```

Het logboeknut wordt gebruikt om berichten aan de console te registreren. De berichten zullen slechts in de console tonen als het zuiveren door de gebruiker wordt aangezet. De geadviseerde manier om het zuiveren aan te zetten is [ Adobe Experience Platform Debugger ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) te gebruiken. Als alternatief kan de gebruiker de volgende opdracht `_satellite.setDebug(true)` uitvoeren in de browserontwikkelaarsconsole. Het logger heeft de volgende methodes:

* `logger.log(message: string)`: meldt een bericht aan de console.
* `logger.info(message: string)`: meldt een informatief bericht aan de console.
* `logger.warn(message: string)`: meldt een waarschuwingsbericht aan de console.
* `logger.error(message: string)`: meldt een foutbericht aan de console.
* `logger.debug(message: string)`: meldt een foutopsporingsbericht aan de console. (Alleen zichtbaar wanneer logboekregistratie voor `verbose` is ingeschakeld in uw browserconsole.)
* `logger.deprecation(message: string)`: meldt een waarschuwingsbericht aan de console of foutopsporing van tags al dan niet is ingeschakeld door de gebruiker.

## `onDebugChanged`

Door een callback functie in `turbine.onDebugChanged` door te geven, zullen de markeringen uw callback roepen wanneer het zuiveren wordt geschakeld. Tags geven een Booleaanse waarde door aan de callback-functie die waar is als foutopsporing is ingeschakeld of onwaar als foutopsporing is uitgeschakeld.

Als u eenvoudig probeert om berichten te registreren, is het onwaarschijnlijk u dit zult moeten gebruiken. In plaats daarvan logt u altijd berichten met `turbine.logger` en tags in om ervoor te zorgen dat uw berichten alleen naar de console worden afgedrukt wanneer foutopsporing voor tags is ingeschakeld.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Een object met de volgende instellingen die door de gebruiker zijn gedefinieerd voor de eigenschap van de huidige tagruntimebibliotheek:

* `propertySettings.domains: Array<String>`

  Een array van domeinen waarop de eigenschap van toepassing is.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  Extensieontwikkelaars dienen zich niet bezig te houden met deze instelling.
