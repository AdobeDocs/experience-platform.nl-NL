---
title: Opdrachten voor Adobe Experience Platform Web SDK uitvoeren
description: Leer hoe te om de bevelen van SDK van het Web van het Experience Platform uit te voeren
keywords: Voer bevelen uit;commandName;Promises;getLibraryInfo;response voorwerpen;toestemming;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Opdrachten uitvoeren


Nadat de basiscode op uw webpagina is geïmplementeerd, kunt u beginnen met het uitvoeren van opdrachten met de SDK. U hoeft niet te wachten op het externe bestand (`alloy.js`) die vanaf de server moet worden geladen voordat opdrachten worden uitgevoerd. Als het laden van de SDK nog niet is voltooid, worden opdrachten zo snel mogelijk in de wachtrij geplaatst en verwerkt door de SDK.

Opdrachten worden uitgevoerd met de volgende syntaxis.

```javascript
alloy("commandName", options);
```

De `commandName` vertelt de SDK wat te doen, terwijl `options` Dit zijn de parameters en de gegevens die u in een opdracht wilt doorgeven. Omdat de beschikbare opties van het bevel afhangen, gelieve de documentatie voor meer details over elk bevel te raadplegen.

## Een nota over beloften

[Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) zijn fundamenteel voor hoe SDK met de code op uw webpagina communiceert. Een promise is een algemene programmeerstructuur en is niet specifiek voor deze SDK of zelfs JavaScript. Een belofte doet dienst als volmacht voor een waarde die niet gekend is wanneer de belofte wordt gecreeerd. Zodra de waarde gekend is, wordt de belofte &quot;opgelost&quot;met de waarde. De functies van de manager kunnen met een belofte worden geassocieerd, zodat u kunt worden op de hoogte gebracht wanneer de belofte is opgelost of wanneer een fout in het proces is voorgekomen om de belofte op te lossen. Voor meer informatie over beloften, lees [deze zelfstudie](https://javascript.info/promise-basics) of een van de andere bronnen op het web.

## Voltooien of mislukken {#handling-success-or-failure}

Elke keer dat een opdracht wordt uitgevoerd, wordt een belofte geretourneerd. De belofte vertegenwoordigt de uiteindelijke voltooiing van het bevel. In het onderstaande voorbeeld kunt u `then` en `catch` methoden om te bepalen wanneer de opdracht is uitgevoerd of mislukt.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Als het niet belangrijk is om te weten wanneer de opdracht slaagt, verwijdert u de opdracht `then` vraag.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Op dezelfde manier, als het weten wanneer het bevel voor u niet belangrijk is, kunt u verwijderen `catch` vraag.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Responsobjecten

Alle beloftes die door opdrachten worden geretourneerd, worden opgelost met een `result` object. Het resultaatobject bevat gegevens die afhankelijk zijn van de opdracht en de toestemming van de gebruiker. Bibliotheekinfo wordt bijvoorbeeld doorgegeven als een eigenschap van het resultaatobject in de volgende opdracht.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Toestemming

Indien een gebruiker voor een bepaald doel geen toestemming heeft gegeven, wordt de belofte nog steeds opgelost; het reactieobject bevat echter alleen de informatie die kan worden verstrekt in de context van wat de gebruiker heeft toegestaan .
