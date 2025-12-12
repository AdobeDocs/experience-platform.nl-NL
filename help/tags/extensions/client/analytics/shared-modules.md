---
title: Gedeelde modules voor de extensie Adobe Analytics
description: Leer meer over de gedeelde bibliotheekmodules die worden geleverd door de Adobe Analytics-tagextensie in Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Gedeelde modules voor de extensie Adobe Analytics

De [&#x200B; uitbreiding van Adobe Analytics &#x200B;](./overview.md) verstrekt twee verschillende [&#x200B; gedeelde modules &#x200B;](../../../extension-dev/web/shared.md) die u in uw ervaringstoepassing kunt integreren. Deze modules worden behandeld in de onderstaande secties.

## [!DNL get-tracker]

Voordat Adobe Analytics bakens verzendt, moet het het tracker-object initialiseren. Het initialisatieproces begint door [&#x200B; AppMeasurement &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL) te laden, die door een spoorboekvoorwerp te creëren wordt gevolgd.

U kunt als volgt toegang krijgen tot het tracker-object nadat het volledig is geïnitialiseerd met de gedeelde module `get-tracker` :

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Controleren of Adobe Analytics is geïnstalleerd

Het is mogelijk dat Adobe Analytics niet is geïnstalleerd of opgenomen in dezelfde tagbibliotheek als uw extensie. Daarom wordt u ten zeerste aangeraden deze kwestie in uw code te controleren en deze op de juiste manier af te handelen. De volgende JavaScript is een voorbeeld van hoe u dit kunt implementeren:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Als `getTracker` `undefined` is, bestaat de Adobe Analytics-extensie niet in de tagbibliotheek. U kunt het geregistreerde bericht aanpassen om nauwkeurig te wijzen op welke functionaliteit kan worden verloren als Adobe Analytics niet geïnstalleerd is.


## [!DNL augment-tracker]

Nadat het tracker-object is geïnitialiseerd, bestaat de volgende stap in het proces uit versterking. Met deze stap kan uw extensie de tracker verfraaien met wat nodig is voordat er variabelen zijn toegepast vanuit de Adobe Analytics-extensieconfiguratie of voordat er bakens zijn verzonden.

Bovendien heeft uw extensie de mogelijkheid om het initialisatieproces van de tracker te pauzeren terwijl uw extensie een eigen asynchrone taak uitvoert, zoals het ophalen van gegevens of JavaScript van een server.

U kunt de module `augment-tracker` als volgt implementeren:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

De functie die in `augmentTracker()` wordt doorgegeven, wordt aangeroepen zodra de augmentatiefase van het initialisatieproces van de tracker is bereikt.

Als uw extensie een asynchrone taak moet voltooien voordat de tracker wordt uitgebreid, kunt u als volgt een promise van uw functie retourneren:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Door een belofte terug te keren, signaleert uw uitbreiding aan Adobe Analytics dat het het volgaarinitialiseringsproces zou moeten pauzeren tot de belofte wordt opgelost.

>[!WARNING]
>
>Wees voorzichtig wanneer u het initialisatieproces van de tracker onderbreekt, aangezien dit kan leiden tot vertraging bij het verzenden van bakens en daarom niet-verzamelde gegevens kan opleveren (bijvoorbeeld als de gebruiker weg van de pagina navigeert voordat de baken wordt verzonden).
