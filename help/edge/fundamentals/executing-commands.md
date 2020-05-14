---
title: Opdrachten uitvoeren
seo-title: Opdrachten van Adobe Experience Platform Web SDK uitvoeren
description: Leer hoe u de opdrachten van Experience Platform Web SDK uitvoert
seo-description: Leer hoe u de opdrachten van Experience Platform Web SDK uitvoert
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Opdrachten uitvoeren

Nadat de basiscode op uw webpagina is geïmplementeerd, kunt u beginnen met het uitvoeren van opdrachten met de SDK. U hoeft niet te wachten tot het externe bestand \(`alloy.js`\) van de server is geladen voordat u opdrachten uitvoert. Als het laden van de SDK nog niet is voltooid, worden opdrachten zo snel mogelijk in de wachtrij geplaatst en verwerkt door de SDK.

Opdrachten worden uitgevoerd met de volgende syntaxis.

```javascript
alloy("commandName", options);
```

Het `commandName` vertelt de SDK wat te doen, terwijl `options` zijn de parameters en de gegevens u in een bevel wilt overgaan. Omdat de beschikbare opties van het bevel afhangen, gelieve de documentatie voor meer details over elk bevel te raadplegen.

## Een nota over beloften

[Beloften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) zijn van fundamenteel belang voor de manier waarop de SDK communiceert met de code op uw webpagina. Een promise is een algemene programmeerstructuur en is niet specifiek voor deze SDK of zelfs JavaScript. Een belofte doet dienst als volmacht voor een waarde die niet gekend is wanneer de belofte wordt gecreeerd. Zodra de waarde gekend is, wordt de belofte &quot;opgelost&quot;met de waarde. De functies van de manager kunnen met een belofte worden geassocieerd, zodat u kunt worden op de hoogte gebracht wanneer de belofte is opgelost of wanneer een fout in het proces is voorgekomen om de belofte op te lossen. Lees voor meer informatie over beloften [deze zelfstudie](https://javascript.info/promise-basics) of een van de andere bronnen op het web.

## Voltooien of mislukken

Elke keer dat een opdracht wordt uitgevoerd, wordt een belofte geretourneerd. De belofte vertegenwoordigt de uiteindelijke voltooiing van het bevel. In het onderstaande voorbeeld kunt u methoden gebruiken `then` en `catch` gebruiken om te bepalen wanneer de opdracht is geslaagd of mislukt.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Als het weten wanneer het bevel slaagt niet belangrijk voor u is, kunt u de `then` vraag verwijderen.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Eveneens, als het weten wanneer het bevel niet belangrijk voor u is, kunt u de `catch` vraag verwijderen.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

### Responsobjecten

Alle beloftes die door opdrachten worden geretourneerd, worden opgelost met een `result` object. Het resultaatobject bevat gegevens die afhankelijk zijn van de opdracht en de toestemming van de gebruiker. Bibliotheekinfo wordt bijvoorbeeld doorgegeven als een eigenschap van het resultaatobject in de volgende opdracht.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(results.libraryInfo.version);
});
```

### Toestemming

Indien een gebruiker voor een bepaald doel geen toestemming heeft gegeven, wordt de belofte nog steeds opgelost; het reactieobject bevat echter alleen de informatie die kan worden verstrekt in de context van wat de gebruiker heeft toegestaan .
