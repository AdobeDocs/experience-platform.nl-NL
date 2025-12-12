---
title: Context in Edge Extension Modules
description: Leer over het contextvoorwerp en de rol het in interactie met bibliotheekmodules in markeringsuitbreidingen van randeigenschappen speelt.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# Context in Edge-uitbreidingsmodules

Alle bibliotheekmodules in randextensies krijgen een `context` -object wanneer ze worden uitgevoerd. In dit document worden de eigenschappen beschreven die door het `context` -object worden geboden en de rol die ze spelen in bibliotheekmodules.

## Adobe Request-context (boog)

De eigenschap `arc` is een object dat informatie bevat over de gebeurtenis die de regel activeert. In de onderstaande secties worden de verschillende subeigenschappen in dit object besproken.

### [!DNL event]

Het `event` -object vertegenwoordigt de gebeurtenis die de regel heeft geactiveerd en bevat de volgende waarden:

```js
logger.log(context.arc.event);
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm` | Het XDM-object van de gebeurtenis. |
| `data` | De aangepaste gegevenslaag. |

### [!DNL request]

Om niet te worden verward met een aanvraag van het clientapparaat, is `request` een enigszins gewijzigd object dat afkomstig is van Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

Het `request` -object heeft twee eigenschappen op hoofdniveau: `body` en `head` . De eigenschap `body` bevat XDM-gegevens (Experience Data Model) en kan in Adobe Experience Platform Debugger worden geïnspecteerd wanneer u naar **[!UICONTROL Launch]** navigeert en het tabblad **[!UICONTROL Edge Trace]** selecteert.

### [!DNL ruleStash] {#rulestash}

`ruleStash` is een object dat elk resultaat van actiemodules verzamelt.

```js
logger.log(context.arc.ruleStash);
```

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam `send-beacon` heeft, worden alle resultaten van `send-beacon` -handelingen opgeslagen in de naamruimte `ruleStash['send-beacon']` .

De naamruimte is uniek voor elke extensie en heeft de waarde `undefined` aan het begin.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Neem bijvoorbeeld een extensie `transform` die twee handelingen bevat: `generate-fullname` en `generate-fulladdress` . Deze twee acties worden dan toegevoegd aan een regel.

Als het resultaat van de handeling `generate-fullname` `Firstname Lastname` is, wordt de regelstreep als volgt weergegeven nadat de handeling is voltooid:

```js
{
  transform: 'Firstname Lastname'
}
```

Als het resultaat van de handeling `generate-address` `3900 Adobe Way` is, wordt de regelstreep als volgt weergegeven nadat de handeling is voltooid:

```js
{
  transform: '3900 Adobe Way'
}
```

U ziet dat &quot;FirstName LastName&quot; niet meer bestaat binnen de regelstash omdat de handeling `generate-address` deze met een nieuwe waarde heeft overschreven.

Als u wilt dat `ruleStash` de resultaten van beide handelingen opslaat in de naamruimte `transform` , kunt u een actiemodule schrijven, vergelijkbaar met het volgende voorbeeld:

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

De eerste keer dat deze handeling wordt uitgevoerd, begint `ruleStash` als `undefined` en wordt daarom geïnitialiseerd als een leeg object. De volgende keer dat de handeling wordt uitgevoerd, ontvangt deze `ruleStash` die werd geretourneerd toen de handeling eerder werd aangeroepen. Als u een object gebruikt als `ruleStash` , kunt u nieuwe gegevens toevoegen zonder dat de gegevens verloren gaan die eerder zijn ingesteld door andere handelingen uit onze extensie.

>[!NOTE]
>
>Zorg ervoor dat u altijd de volledige extensieregel retourneert wanneer u deze strategie gebruikt. Als u in plaats daarvan alleen een waarde retourneert, worden eventuele andere eigenschappen die u hebt ingesteld, overschreven.

## Hulpmiddelen

De eigenschap `utils` vertegenwoordigt een object dat hulpprogramma&#39;s bevat die specifiek zijn voor de tagruntime.

### [!DNL logger]

Het `logger` nut staat u toe om berichten te registreren die tijdens het zuiveren zittingen wanneer het gebruiken van [&#x200B; Adobe Experience Platform Debugger &#x200B;](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) zullen worden getoond.

```js
context.utils.logger.error('Error!');
```

Het logger heeft de volgende methodes, waar `message` het bericht is u wilt registreren:

| Methode | Beschrijving |
| --- | --- |
| `log(message)` | Logs a message to the console. |
| `info(message)` | Logs an informational message to the console. |
| `warn(message)` | Logs a warning message aan de console. |
| `error(message)` | Logs an error message to the console. |
| `debug(message)` | Logs a zuivert bericht aan de console. Dit is alleen zichtbaar wanneer `verbose` logboekregistratie is ingeschakeld in uw browserconsole. |

### [!DNL fetch]

Dit nut voert [&#x200B; Fetch API &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) uit. U kunt de functie gebruiken om verzoeken aan derdeeindpunten te doen.

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
| `turbineVersion` | De [&#x200B; Turbine &#x200B;](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) versie die binnen de huidige bibliotheek wordt gebruikt. |
| `turbineBuildDate` | ISO 8601 datum toen de versie van [&#x200B; Turbine &#x200B;](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) binnen de container werd gebruikt werd gebouwd. |
| `buildDate` | De ISO 8601-datum waarop de huidige bibliotheek is gemaakt. |
| `environment` | De omgeving waarvoor deze bibliotheek is gemaakt. Mogelijke waarden zijn `development` , `staging` en `production.` |

In het volgende voorbeeld wordt een `getBuildInfo` -object getoond om de geretourneerde waarden aan te tonen:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Dit nut keert het `settings` voorwerp terug dat het laatst van de [&#x200B; mening van de uitbreidingsconfiguratie &#x200B;](../configuration.md) werd bewaard.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Dit hulpprogramma retourneert het `settings` -object dat het laatst is opgeslagen in de overeenkomende bibliotheekmoduleweergave.

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
