---
title: Haken voor Adobe Experience Platform Web SDK controleren
description: Leer hoe u de controlemakken van Adobe Experience Platform Web SDK gebruikt om fouten in uw implementatie op te sporen en Web SDK-logboeken vast te leggen.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 9b2ecedfafbafed042eba73a034cb9b9e95af579
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---

# Houten voor Web SDK controleren

De Adobe Experience Platform Web SDK bevat controleluks die u kunt gebruiken om verschillende systeemgebeurtenissen te controleren. Deze hulpmiddelen zijn nuttig om uw eigen het zuiveren hulpmiddelen te ontwikkelen en de logboeken van SDK van het Web te vangen.

Het Web SDK brengt de controlerende functies teweeg ongeacht of u [&#x200B; het zuiveren &#x200B;](commands/configure/debugenabled.md) hebt toegelaten.

## `onInstanceCreated` {#onInstanceCreated}

Deze callback functie wordt teweeggebracht wanneer u met succes een nieuwe instantie van SDK van het Web hebt gecreeerd. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.instance` | Functie | De instantiefunctie die wordt gebruikt om de bevelen van SDK van het Web te roepen. |

## `onInstanceConfigured` {#onInstanceConfigured}

Deze callbackfunctie wordt geactiveerd door de Web SDK wanneer de opdracht [`configure`](commands/configure/overview.md) correct is omgezet. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.config` | Object | Een voorwerp dat de configuratie bevat u voor uw instantie van SDK van het Web gebruikte. Dit zijn de opties die aan de opdracht [`configure`](commands/configure/overview.md) worden doorgegeven en waarbij alle standaardwaarden worden toegevoegd. |

## `onBeforeCommand` {#onBeforeCommand}

Deze callback functie wordt teweeggebracht door SDK van het Web alvorens een ander bevel wordt uitgevoerd. U kunt deze functie gebruiken om de configuratieopties van een specifiek bevel terug te winnen. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.commandName` | String | De naam van het bevel van SDK van het Web alvorens deze functie wordt uitgevoerd. |
| `data.options` | Object | Een object dat de opties bevat die aan de opdracht Web SDK zijn doorgegeven. |

## `onCommandResolved` {#onCommandResolved}

Deze callback functie wordt teweeggebracht wanneer het oplossen van bevelbeloften. U kunt deze functie gebruiken om de bevelopties en het resultaat te zien. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.commandName` | String | De naam van het uitgevoerde bevel van SDK van het Web. |
| `data.options` | Object | Een object dat de opties bevat die aan de opdracht Web SDK zijn doorgegeven. |
| `data.result` | Object | Een object dat het resultaat bevat van de opdracht Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Deze callback functie wordt teweeggebracht alvorens een bevelbelofte wordt verworpen en het bevat informatie over de reden waarom het bevel werd verworpen. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.commandName` | String | De naam van het uitgevoerde bevel van SDK van het Web. |
| `data.options` | Object | Een object dat de opties bevat die aan de opdracht Web SDK zijn doorgegeven. |
| `data.error` | Object | Een voorwerp dat het foutenbericht bevat dat van de browser netwerkvraag (`fetch` in de meeste gevallen) is teruggekeerd, samen met de reden waarom het bevel werd verworpen. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Deze callback functie wordt teweeggebracht alvorens een netwerkverzoek wordt uitgevoerd. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.requestId` | String | De `requestId` die door Web SDK wordt gegenereerd om foutopsporing in te schakelen. |
| `data.url` | String | De aangevraagde URL. |
| `data.payload` | Object | Het payload-object van de netwerkaanvraag dat wordt omgezet in JSON-indeling en in de hoofdtekst van de aanvraag wordt verzonden via een `POST` -methode. |

## `onNetworkResponse` {#onNetworkResponse}

Deze callback functie wordt teweeggebracht wanneer browser een reactie ontvangt. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.requestId` | String | De `requestId` die door Web SDK wordt gegenereerd om foutopsporing in te schakelen. |
| `data.url` | String | De aangevraagde URL. |
| `data.payload` | Object | Het payload-object dat wordt omgezet in JSON-indeling en in de hoofdtekst van de aanvraag wordt verzonden via een `POST` -methode. |
| `data.body` | String | De hoofdtekst van de reactie in tekenreeksindeling. |
| `data.parsedBody` | Object | Een object dat de geparseerde responstekst bevat. Als een fout optreedt tijdens het parseren van de hoofdtekst van de reactie, is deze parameter ongedefinieerd. |
| `data.status` | String | De antwoordcode in geheel-getalnotatie. |
| `data.retriesAttempted` | Geheel | Het aantal pogingen dat is gedaan om het verzoek te verzenden. Nul betekent dat het verzoek succesvol was bij de eerste poging. |

## `onNetworkError` {#onNetworkError}

Deze callback functie wordt teweeggebracht wanneer het netwerkverzoek ontbrak. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.requestId` | String | De `requestId` die door Web SDK wordt gegenereerd om foutopsporing in te schakelen. |
| `data.url` | String | De aangevraagde URL. |
| `data.payload` | Object | Het payload-object dat wordt omgezet in JSON-indeling en in de hoofdtekst van de aanvraag wordt verzonden via een `POST` -methode. |
| `data.error` | Object | Een voorwerp dat het foutenbericht bevat dat van de browser netwerkvraag (`fetch` in de meeste gevallen) is teruggekeerd, samen met de reden waarom het bevel werd verworpen. |

## `onBeforeLog` {#onBeforeLog}

Deze callback functie wordt teweeggebracht alvorens het Web SDK om het even wat aan de console registreert. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.componentName` | String | De naam van de component die het logboekbericht produceerde. |
| `data.level` | String | Het registrerenniveau. Ondersteunde niveaus: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Tekenreeksarray | De argumenten van het logboekbericht. |


## `onContentRendering` {#onContentRendering}

Deze callbackfunctie wordt geactiveerd door de component `personalization` in verschillende stadia van rendering. De lading kan verschillen, afhankelijk van de `status` parameter. Zie het voorbeeld hieronder voor meer informatie over de functieparameters.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.componentName` | String | De naam van de component die het logboekbericht produceerde. |
| `data.payload` | Object | Het payload-object dat wordt omgezet in JSON-indeling en in de hoofdtekst van de aanvraag wordt verzonden via een `POST` -methode. |
| `data.status` | String | De component `personalization` informeert de Web SDK over de status van rendering.  Ondersteunde waarden: <ul><li>`rendering-started`: Geeft aan dat de Web SDK op het punt staat voorstellingen te renderen. Voordat de Web SDK een beslissingsbereik of een weergave begint te renderen, kunt u in het `data` -object de voorstellingen zien die door de `personalization` -component en de bereiknaam worden gerenderd.</li><li>`no-offers`: Geeft aan dat er geen payload is ontvangen voor de aangevraagde parameters.</li> <li>`rendering-failed`: geeft aan dat Web SDK geen voorstel heeft weergegeven.</li><li>`rendering-succeeded`: geeft aan dat rendering is voltooid voor een beslissingsbereik.</li> <li>`rendering-redirect`: geeft aan dat Web SDK een omleidingsvoorstel zal renderen.</li></ul> |

## `onContentHiding` {#onContentHiding}

Deze callback-functie wordt geactiveerd wanneer een vooraf verborgen stijl wordt toegepast of verwijderd.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parameter | Type | Beschrijving |
|---------|----------|----------|
| `data.instanceName` | String | De naam van de globale variabele waar de instantie van SDK van het Web wordt opgeslagen. |
| `data.componentName` | String | De naam van de component die het logboekbericht produceerde. |
| `data.status` | String | De component `personalization` informeert de Web SDK over de status van rendering. Ondersteunde waarden: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Hoe te om controlehaken te specificeren wanneer het gebruiken van het pakket NPM {#specify-monitoring-npm}

Als u het Web SDK door het [&#x200B; NPM pakket &#x200B;](install/npm.md) gebruikt, kunt u controlehaken in de `createInstance` functie specificeren, zoals hieronder getoond.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Voorbeeld {#example}

De Web SDK zoekt naar een array met objecten in een algemene variabele met de naam `__alloyMonitors` .

Als u alle Web SDK-gebeurtenissen wilt vastleggen, moet u uw controlemakken definiëren voordat de Web SDK-code op uw pagina wordt geladen. Elke controlemethode vangt een gebeurtenis van SDK van het Web.

U kunt controlehaken *bepalen nadat* de code van SDK van het Web op uw pagina laadt, maar om het even welke haken die vóór paginading hebben teweeggebracht zullen *niet* worden gevangen.

Wanneer u het controlehaakvoorwerp bepaalt, moet u slechts de methodes bepalen die u speciale logica voor zou willen bepalen.
Als u bijvoorbeeld alleen om `onContentRendering` geeft, kunt u gewoon die methode definiëren. U hoeft niet alle controlehaken tegelijk te gebruiken.

U kunt meerdere controlehaakobjecten definiëren. Alle objecten met de opgegeven methode worden aangeroepen wanneer de corresponderende gebeurtenis wordt geactiveerd.

>[!TIP]
>
>Zie onder een voorbeeldpagina met alle controleluks geïmplementeerd.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
