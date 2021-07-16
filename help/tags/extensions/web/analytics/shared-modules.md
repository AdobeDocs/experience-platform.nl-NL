---
title: Gedeelde modules voor de extensie Adobe Analytics
description: Leer meer over de gedeelde bibliotheekmodules die worden geleverd door de Adobe Analytics-tagextensie in Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Gedeelde modules voor de extensie Adobe Analytics

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De [Adobe Analytics-extensie](./overview.md) biedt twee verschillende [gedeelde modules](../../../extension-dev/web/shared.md) die u kunt integreren in uw ervaringstoepassing. Deze modules worden behandeld in de onderstaande secties.

## [!DNL get-tracker]

Voordat Adobe Analytics bakens verzendt, moet het het tracker-object initialiseren. Het initialisatieproces begint met het laden van [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html), gevolgd door het maken van een tracker-object.

U kunt tot het tracker voorwerp toegang hebben nadat het volledig is geïnitialiseerd door `get-tracker` als volgt te gebruiken gedeelde module:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Controleren of Adobe Analytics is geïnstalleerd

Het is mogelijk dat Adobe Analytics niet is geïnstalleerd of opgenomen in dezelfde tagbibliotheek als uw extensie. Daarom wordt u ten zeerste aangeraden deze kwestie in uw code te controleren en deze op de juiste manier af te handelen. Het volgende JavaScript is een voorbeeld van hoe u dit kunt implementeren:

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

Als `getTracker` `undefined` is, bestaat de extensie Adobe Analytics niet in de tagbibliotheek. U kunt het geregistreerde bericht aanpassen om nauwkeurig te wijzen op welke functionaliteit kan worden verloren als Adobe Analytics niet geïnstalleerd is.


## [!DNL augment-tracker]

Nadat het tracker-object is geïnitialiseerd, bestaat de volgende stap in het proces uit augmentatie. Met deze stap kan uw extensie de tracker verfraaien met wat nodig is voordat er variabelen zijn toegepast vanuit de Adobe Analytics-extensieconfiguratie of voordat er bakens zijn verzonden.

Bovendien heeft uw extensie de mogelijkheid om het initialisatieproces van de tracker te pauzeren terwijl uw extensie een eigen asynchrone taak uitvoert, zoals het ophalen van gegevens of JavaScript van een server.

U kunt de `augment-tracker` module als zo uitvoeren:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

De functie die in `augmentTracker()` wordt overgegaan zal worden geroepen zodra de verhogingsfase van het trackerinitialisatieproces wordt bereikt.

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
