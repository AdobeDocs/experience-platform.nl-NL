---
title: Verwijzing naar satellietobject
description: Leer meer over het client-side _satelliet object en de verschillende functies die u ermee kunt uitvoeren in tags.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `_satellite` objectverwijzing

Het `_satellite` -object stelt verschillende ondersteunde ingangspunten beschikbaar die u helpen te communiceren met de tagbibliotheek die op uw site is gepubliceerd. Alle tagimplementaties geven `_satellite` weer als de loader-tag correct is geïmplementeerd. Er zijn verschillende hoofdgebruikscenario&#39;s voor dit object:

* Gebruik in uw tagbibliotheek in aangepaste codeblokken, zodat u volledige toegang hebt tot de tagbibliotheek zelf.
* Fouten opsporen in uw geïmplementeerde implementatie binnen een omgeving (ontwikkeling, staging of productie)
* Directe implementatie op uw website, waardoor u volledige controle hebt over het moment waarop gebeurtenissen of tagregels worden geactiveerd. Voor nieuwe implementaties, adviseert Adobe het gebruiken van een flexibelere strategie zoals de [ Laag van Gegevens van de Cliënt van Adobe ](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Als u `_satellite` van uw plaatscode (bijvoorbeeld, `_satellite.track()`) roept, **beschermt elke vraag** zodat uw plaats niet strak aan de markeringsbibliotheek wordt gekoppeld.
>
>Wanneer u `_satellite` gebruikt in de aangepaste code van een tag-eigenschap of lokaal in uw browserconsole, hoeft u dit niet te controleren.

## Algemene gebruiksvoorbeelden

```js
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
