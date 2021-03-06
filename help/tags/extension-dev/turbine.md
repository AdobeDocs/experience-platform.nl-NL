---
title: Variabele turbinevrij
description: Leer meer over het turbineobject, een gratis variabele die specifieke informatie en hulpprogramma's voor de Adobe Experience Platform-tagruntime biedt.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Variabele zonder turbinemotor

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Het `turbine` voorwerp is een &quot;vrije variabele&quot;binnen het werkingsgebied van de de bibliotheekmodules van uw uitbreiding. Deze biedt informatie en hulpprogramma&#39;s die specifiek zijn voor de Adobe Experience Platform-tagruntime en is altijd beschikbaar voor bibliotheekmodules zonder `require()` te gebruiken.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` is een object met constructiegegevens over de huidige tagruntimebibliotheek.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `turbineVersion` | De [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-versie die in de huidige bibliotheek wordt gebruikt. |
| `turbineBuildDate` | De ISO 8601-datum waarop de in de container gebruikte versie van [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) is gemaakt. |
| `buildDate` | De ISO 8601-datum waarop de huidige bibliotheek is gemaakt. |

{style=&quot;table-layout:auto&quot;}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` is een object dat informatie bevat over de omgeving waarin de bibliotheek is geïmplementeerd.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de omgeving. |
| `stage` | De omgeving waarvoor deze bibliotheek is gemaakt. Mogelijke waarden zijn `development`, `staging` en `production`. |

{style=&quot;table-layout:auto&quot;}

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

Retourneert het instellingsobject dat het laatst is opgeslagen in de weergave [extensieconfiguratie](./configuration.md).

Waarden binnen de geretourneerde instellingen komen mogelijk uit gegevenselementen. Daarom kan het aanroepen van `getExtensionSettings()` op verschillende momenten verschillende resultaten opleveren als de waarden van de gegevenselementen zijn gewijzigd. Om de meest bijgewerkte waarden te krijgen, gelieve zo lang mogelijk te wachten alvorens `getExtensionSettings()` te roepen.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

De eigenschap [hostedLibFiles](./manifest.md) kan binnen de extensiemanifest worden gedefinieerd om verschillende bestanden te hosten samen met de tagruntime-bibliotheek. Deze module retourneert de URL waar het opgegeven bibliotheekbestand wordt gehost.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Hiermee wordt een module opgehaald die via een andere extensie is gedeeld. Als er geen overeenkomende module wordt gevonden, wordt `undefined` geretourneerd. Zie [Gedeelde modules implementeren](./web/shared.md) voor meer informatie over gedeelde modules.

## `logger`

```js
turbine.logger.error('Error!');
```

Het logboeknut wordt gebruikt om berichten aan de console te registreren. De berichten zullen slechts in de console tonen als het zuiveren door de gebruiker wordt aangezet. De geadviseerde manier om het zuiveren aan te zetten is [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda) te gebruiken. Als alternatief, kan de gebruiker het volgende bevel `_satellite.setDebug(true)` binnen de browser ontwikkelaarsconsole in werking stellen. Het logger heeft de volgende methodes:

* `logger.log(message: string)`: Logs a message to the console.
* `logger.info(message: string)`: Logs an informational message to the console.
* `logger.warn(message: string)`: Logs a warning message to the console.
* `logger.error(message: string)`: Logs an error message to the console.
* `logger.debug(message: string)`: Logs a zuivert bericht aan de console. (Alleen zichtbaar wanneer `verbose` logboekregistratie is ingeschakeld in uw browserconsole.)
* `logger.deprecation(message: string)`: Logs een waarschuwingsbericht aan de console al dan niet de markering het zuiveren door de gebruiker wordt toegelaten.

## `onDebugChanged`

Door een callback functie in `turbine.onDebugChanged` over te gaan, zullen de markeringen uw callback roepen wanneer het zuiveren wordt geschakeld. Tags geven een Booleaanse waarde door aan de callback-functie die waar is als foutopsporing is ingeschakeld of onwaar als foutopsporing is uitgeschakeld.

Als u eenvoudig probeert om berichten te registreren, is het onwaarschijnlijk u dit zult moeten gebruiken. Logberichten die `turbine.logger` gebruiken en tags zorgen er in plaats daarvan voor dat uw berichten alleen naar de console worden afgedrukt wanneer foutopsporing van tags is ingeschakeld.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Een object met de volgende instellingen die door de gebruiker zijn gedefinieerd voor de eigenschap van de huidige tagruntimebibliotheek:

* `propertySettings.domains: Array<String>`

   Een array van domeinen waarop de eigenschap van toepassing is.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Extensieontwikkelaars dienen zich niet bezig te houden met deze instelling.
