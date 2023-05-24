---
title: Context in Edge-uitbreidingsmodules
description: Leer over het contextvoorwerp en de rol het in interactie met bibliotheekmodules in markeringsuitbreidingen van randeigenschappen speelt.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 1%

---

# Context in Edge-uitbreidingsmodules

>[!NOTE]
>
> Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Alle bibliotheekmodules in randextensies worden geleverd met een `context` -object wanneer deze worden uitgevoerd. Dit document behandelt de eigenschappen die door `context` -object en de rol die ze spelen in bibliotheekmodules.

## Context verzoek Adobe (boog)

De `arc` eigenschap is een object dat informatie bevat over de gebeurtenis die de regel activeert. In de onderstaande secties worden de verschillende subeigenschappen in dit object besproken.

### [!DNL event]

De `event` object vertegenwoordigt de gebeurtenis die de regel heeft geactiveerd en bevat de volgende waarden:

```js
logger.log(context.arc.event);
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm` | Het XDM-object van de gebeurtenis. |
| `data` | De aangepaste gegevenslaag. |

### [!DNL request]

niet worden verward met een verzoek van het clientapparaat; `request` is een enigszins gewijzigd object dat afkomstig is van Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

De `request` object heeft twee eigenschappen op hoofdniveau: `body` en `head`. De `body` eigenschap bevat XDM-informatie (Experience Data Model) en kan worden gecontroleerd in Adobe Experience Platform Debugger wanneer u navigeert naar **[!UICONTROL Launch]** en selecteert u de **[!UICONTROL Edge Trace]** tab.

### [!DNL ruleStash] {#rulestash}

`ruleStash` is een object dat elk resultaat van actiemodules zal verzamelen.

```js
logger.log(context.arc.ruleStash);
```

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam heeft `send-beacon`alle resultaten van `send-beacon` acties worden opgeslagen op de `ruleStash['send-beacon']` naamruimte.

De naamruimte is uniek voor elke extensie en heeft de waarde `undefined` aan het begin.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Neem bijvoorbeeld een `transform` extensie met twee acties: `generate-fullname` en `generate-fulladdress`. Deze twee acties worden dan toegevoegd aan een regel.

Indien het resultaat van de `generate-fullname` handeling is `Firstname Lastname`Vervolgens ziet de regelstash er als volgt uit nadat de handeling is voltooid:

```js
{
  transform: 'Firstname Lastname'
}
```

Indien het resultaat van de `generate-address` handeling is `3900 Adobe Way`Vervolgens ziet de regelstash er als volgt uit nadat de handeling is voltooid:

```js
{
  transform: '3900 Adobe Way'
}
```

U ziet dat &quot;FirstName LastName&quot; niet langer bestaat binnen de regelstash omdat de optie `generate-address` actie heeft er een nieuwe waarde aan toegevoegd .

Als u `ruleStash` om de resultaten van beide handelingen op te slaan in het dialoogvenster `transform` naamruimte, kunt u uw actiemodule schrijven, net als in het volgende voorbeeld:

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

De eerste keer dat deze handeling wordt uitgevoerd, `ruleStash` begint als `undefined` en wordt daarom geïnitialiseerd als een leeg object. De volgende keer dat de handeling wordt uitgevoerd, ontvangt deze `ruleStash` die werd geretourneerd toen de handeling eerder werd aangeroepen. Een object gebruiken als `ruleStash` kunt u nieuwe gegevens toevoegen zonder gegevens te verliezen die eerder zijn ingesteld door andere handelingen uit onze extensie.

>[!NOTE]
>
>Zorg ervoor dat u altijd de volledige extensieregel retourneert wanneer u deze strategie gebruikt. Als u in plaats daarvan alleen een waarde retourneert, worden eventuele andere eigenschappen die u hebt ingesteld, overschreven.

## Hulpmiddelen

De `utils` Deze eigenschap vertegenwoordigt een object dat hulpprogramma&#39;s bevat die specifiek zijn voor de tagruntime.

### [!DNL logger]

De `logger` Het nut staat u toe om berichten te registreren die tijdens het zuiveren zittingen wanneer het gebruiken zullen worden getoond [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

De registreermachine heeft de volgende methodes, waar `message` is het bericht u wilt registreren:

| Methode | Beschrijving |
| --- | --- |
| `log(message)` | Logs a message to the console. |
| `info(message)` | Logs an informational message to the console. |
| `warn(message)` | Logs a warning message to the console. |
| `error(message)` | Logs an error message to the console. |
| `debug(message)` | Logs a zuivert bericht aan de console. Dit is alleen zichtbaar wanneer `verbose` het registreren wordt toegelaten binnen uw browser console. |

### [!DNL fetch]

Dit hulpprogramma implementeert de [Ophalen-API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). U kunt de functie gebruiken om verzoeken aan derdeeindpunten te doen.

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
| `turbineVersion` | De [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) in de huidige bibliotheek wordt gebruikt. |
| `turbineBuildDate` | De ISO 8601-datum waarop de versie van [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) in de container is gebruikt. |
| `buildDate` | De ISO 8601-datum waarop de huidige bibliotheek is gemaakt. |
| `environment` | De omgeving waarvoor deze bibliotheek is gemaakt. Mogelijke waarden zijn `development`, `staging`, en `production.` |

Hier volgt een voorbeeld `getBuildInfo` object om de geretourneerde waarden aan te tonen:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Dit hulpprogramma retourneert de `settings` object dat het laatst is opgeslagen in het menu [extensieconfiguratie](../configuration.md) weergeven.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Dit hulpprogramma retourneert de `settings` object dat het laatst is opgeslagen in de bijbehorende bibliotheekmodule-weergave.

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
