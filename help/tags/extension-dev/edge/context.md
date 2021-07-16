---
title: Context in Edge-uitbreidingsmodules
description: Leer over het contextvoorwerp en de rol het in interactie met bibliotheekmodules in markeringsuitbreidingen van randeigenschappen speelt.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Context in Edge-uitbreidingsmodules

>[!NOTE]
>
> Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Alle bibliotheekmodules in randuitbreidingen worden verstrekt een `context` voorwerp wanneer zij worden uitgevoerd. Dit document behandelt de eigenschappen die door het `context` voorwerp en de rol worden verstrekt zij in bibliotheekmodules spelen.

## Context verzoek Adobe (boog)

De eigenschap `arc` is een object dat informatie bevat over de gebeurtenis die de regel activeert. In de onderstaande secties worden de verschillende subeigenschappen in dit object besproken.

### [!DNL event]

Het object `event` vertegenwoordigt de gebeurtenis die de regel heeft geactiveerd en bevat de volgende waarden:

```js
logger.log(context.arc.event);
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm` | Het XDM-object van de gebeurtenis. |
| `data` | De aangepaste gegevenslaag. |

### [!DNL request]

`request` is een enigszins aangepast object dat afkomstig is van Adobe Experience Platform Edge Network om niet te worden verward met een aanvraag van het clientapparaat.

```js
logger.log(context.arc.request)
```

Het object `request` heeft twee eigenschappen op hoofdniveau: `body` en `head`. De eigenschap `body` bevat XDM-gegevens (Experience Data Model) en kan in Adobe Experience Platform Debugger worden geïnspecteerd wanneer u naar **[!UICONTROL Launch]** navigeert en het tabblad **[!UICONTROL Edge Trace]** selecteert.

### [!DNL ruleStash] {#rulestash}

`ruleStash` is een object dat elk resultaat van actiemodules zal verzamelen.

```js
logger.log(context.arc.ruleStash);
```

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam `send-beacon` heeft, worden alle resultaten van `send-beacon`-handelingen opgeslagen in de naamruimte `ruleStash['send-beacon']`.

De naamruimte is uniek voor elke extensie en heeft aan het begin de waarde `undefined`.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Neem bijvoorbeeld een extensie `transform` die twee handelingen bevat: `generate-fullname` en `generate-fulladdress`. Deze twee acties worden dan toegevoegd aan een regel.

Als het resultaat van de `generate-fullname` actie `Firstname Lastname` is, dan zal de regelstash als volgt verschijnen nadat de actie wordt voltooid:

```js
{
  transform: 'Firstname Lastname'
}
```

Als het resultaat van de `generate-address` actie `3900 Adobe Way` is, dan zal de regelstash als volgt verschijnen nadat de actie wordt voltooid:

```js
{
  transform: '3900 Adobe Way'
}
```

U ziet dat &quot;FirstName LastName&quot; niet meer bestaat binnen de regelstash omdat de handeling `generate-address` deze met een nieuwe waarde heeft overschreven.

Als u `ruleStash` de resultaten van beide acties binnen `transform` namespace wilt opslaan, kunt u uw actiemodule gelijkend op het volgende voorbeeld schrijven:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

De eerste keer dat deze handeling wordt uitgevoerd, begint `ruleStash` als `undefined` en wordt daarom geïnitialiseerd als een leeg object. De volgende keer dat de handeling wordt uitgevoerd, ontvangt deze `ruleStash` die is geretourneerd toen de handeling eerder werd aangeroepen. Door een object als `ruleStash` te gebruiken, kunt u nieuwe gegevens toevoegen zonder dat gegevens verloren gaan die eerder zijn ingesteld door andere handelingen van onze extensie.

>[!NOTE]
>
>Zorg ervoor dat u altijd de volledige extensieregel retourneert wanneer u deze strategie gebruikt. Als u in plaats daarvan alleen een waarde retourneert, worden eventuele andere eigenschappen die u hebt ingesteld, overschreven.

## Hulpmiddelen

De eigenschap `utils` vertegenwoordigt een object dat hulpprogramma&#39;s bevat die specifiek zijn voor de tagruntime.

### [!DNL logger]

Met het hulpprogramma `logger` kunt u berichten registreren die tijdens foutopsporingssessies worden weergegeven wanneer u [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) gebruikt.

```js
context.utils.logger.error('Error!');
```

Het logger heeft de volgende methodes, waar `message` het bericht is u wilt registreren:

| Methode | Beschrijving |
| --- | --- |
| `log(message)` | Logs a message to the console. |
| `info(message)` | Logs an informational message to the console. |
| `warn(message)` | Logs a warning message to the console. |
| `error(message)` | Logs an error message to the console. |
| `debug(message)` | Logs a zuivert bericht aan de console. Dit is zichtbaar slechts wanneer `verbose` het registreren binnen uw browser console wordt toegelaten. |

### [!DNL fetch]

Dit hulpprogramma implementeert de [Fetch-API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). U kunt de functie gebruiken om verzoeken aan derdeeindpunten te doen.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Dit hulpprogramma retourneert een object dat informatie bevat over de build van de huidige tagruntimebibliotheek.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

Het object bevat de volgende waarden:

| Eigenschap | Beschrijving |
| --- | --- |
| `turbineVersion` | De [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge)-versie die in de huidige bibliotheek wordt gebruikt. |
| `turbineBuildDate` | De ISO 8601-datum waarop de in de container gebruikte versie van [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) is gemaakt. |
| `buildDate` | De ISO 8601-datum waarop de huidige bibliotheek is gemaakt. |
| `environment` | De omgeving waarvoor deze bibliotheek is gemaakt. Mogelijke waarden zijn `development`, `staging` en `production.` |

In het volgende voorbeeld ziet u een `getBuildInfo`-object om de geretourneerde waarden aan te tonen:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Dit nut keert het `settings` voorwerp terug dat het laatst van [uitbreidingsconfiguratie](../configuration.md) mening werd bewaard.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Dit nut keert het `settings` voorwerp terug dat het laatst van de overeenkomstige mening van de bibliotheekmodule werd bewaard.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Dit nut keert een voorwerp terug dat informatie over de regel bevat die de module teweegbrengt.

```js
logger.log(context.utils.getRule());
```

Het object bevat de volgende waarden:

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De regel-id. |
| `name` | De regelnaam. |
