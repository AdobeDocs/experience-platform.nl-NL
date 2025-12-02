---
title: track()
description: Trigger een directe vraagregel.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# `track()`

De `_satellite.track()` methode staat u toe om a [ Directe vraagregel ](/help/tags/extensions/client/core/overview.md#direct-call-event) teweeg te brengen.

>[!IMPORTANT]
>
>Adobe overweegt `_satellite.track()` de methode van de a **erfenisimplementatie**. Terwijl het nog volledig wordt gesteund, adviseert Adobe sterk het gebruiken van modernere implementatiepraktijken, zoals de [ Laag van Gegevens van de Cliënt van Adobe ](/help/tags/extensions/client/client-data-layer/overview.md), die de geadviseerde benadering voor nieuwe implementaties is.
>
>Als u verkiest om `_satellite.track()` op uw plaats te gebruiken, **bescherming elke vraag** zodat uw plaats niet strak aan de markeringsbibliotheek wordt gekoppeld. Als de eigenschap tag niet wordt bewaakt, leidt het verwijderen van de eigenschap tag in de toekomst tot fouten in alle verwijzingen naar het object `_satellite` .

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Wanneer u `_satellite.track()` roept gebruikend het herkenningsteken dat in de markeringen UI wordt gevormd, wordt die regel onmiddellijk teweeggebracht. Het aanroepen van deze methode werkt alleen als de regelgebeurtenis. De voorwaarden van de regel gelden nog steeds voordat de handelingen van de regel worden uitgevoerd. De veelvoudige directe vraagregels kunnen het zelfde herkenningsteken gebruiken, toestaand u om al die regels in één keer teweeg te brengen gebruikend één enkele `_satellite.track()` vraag. Elke getriggerde regel controleert nog steeds de eigen voorwaarden voordat actie wordt ondernomen, zelfs als meerdere regels dezelfde id hebben.

## Beschikbare velden

De methode `_satellite.track()` ondersteunt twee argumenten:

| Naam | Type | Vereist | Beschrijving |
|---|---|---|---|
| **`identifier`** | `string` | Ja | De directe herkenningsteken van de vraagregel. U plaatst dit herkenningsteken wanneer het vormen van de regel in de markeringen UI. |
| **`detail`** | `unknown` | Nee | Een optionele lading die gewenste informatie bevat. Wanneer u een regel configureert, kunt u de payload openen met `event.detail` (aangepaste code) of `%event.detail%` (tekstvelden die gegevenselementnotatie ondersteunen). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
